# Topic 03 — Azure Database for PostgreSQL + pgvector (RAG)

> **Domain A (25–30%)** — official skill A2  
> **Modules:** [`../02-language-conversational.md`](../02-language-conversational.md), [`../03-vision-docs.md`](../03-vision-docs.md)  
> **Lab:** [labs/03-postgresql-pgvector-rag.md](./labs/03-postgresql-pgvector-rag.md)

---

## In one sentence

**Azure Database for PostgreSQL** with the **pgvector** extension stores embeddings in relational tables, runs **similarity search with metadata filters** for **RAG**, and requires deliberate **schema, index, and sizing** choices for vector latency.

---

## Why it exists on the exam

Many enterprises already run PostgreSQL. AI-200 tests whether you can model vector workloads **in SQL**, tune pgvector indexes, and implement production RAG — not just NoSQL patterns.

---

## How it works in Azure

### Enable pgvector

```sql
CREATE EXTENSION IF NOT EXISTS vector;
```

### Schema for RAG chunks

```sql
CREATE TABLE document_chunks (
    id            BIGSERIAL PRIMARY KEY,
    tenant_id     TEXT NOT NULL,
    document_id   TEXT NOT NULL,
    chunk_index   INT NOT NULL,
    content       TEXT NOT NULL,
    embedding     vector(1536),  -- match your model dimensions
    metadata      JSONB,
    updated_at    TIMESTAMPTZ DEFAULT now(),
    UNIQUE (tenant_id, document_id, chunk_index)
);

CREATE INDEX idx_chunks_tenant ON document_chunks (tenant_id);
CREATE INDEX idx_chunks_embedding ON document_chunks
    USING hnsw (embedding vector_cosine_ops);
```

**Index types:** **HNSW** (faster query, more memory) vs **IVFFlat** (build faster, needs `lists` tuning). Exam: know you must choose and size appropriately.

### Similarity search with metadata filter (RAG)

```sql
-- query_embedding: pass as parameter from Python
SELECT id, document_id, content,
       1 - (embedding <=> :query_embedding) AS similarity
FROM document_chunks
WHERE tenant_id = :tenant_id
  AND metadata->>'category' = :category
ORDER BY embedding <=> :query_embedding
LIMIT 5;
```

Operators: `<=>` cosine distance, `<->` L2, `<#>` inner product — **use the same metric you indexed**.

### Python: connect with MI or password

```python
import psycopg
from azure.identity import DefaultAzureCredential

# Many teams use password from Key Vault; MI via AAD auth where supported
conn = psycopg.connect(
    host="myserver.postgres.database.azure.com",
    dbname="aidb",
    user="myadmin",
    password="<from-key-vault>",
    sslmode="require",
)
```

### Connection optimization

```python
# Use a pool (psycopg_pool, SQLAlchemy) — don't open per request
from psycopg_pool import ConnectionPool

pool = ConnectionPool(conninfo="...", min_size=2, max_size=20)
```

- Right-size **compute tier** and **memory** — HNSW indexes are RAM-heavy.
- Use **read replicas** for heavy retrieval if write load is separate.

### Sizing vector workloads

| Factor | Impact |
|--------|--------|
| Dimensions (1536 vs 3072) | Storage + index RAM |
| Row count | Query latency; consider partitioning by tenant |
| HNSW params (`m`, `ef_construction`) | Recall vs speed |
| Concurrent queries | Connection pool + CPU |

---

## RAG pipeline with PostgreSQL

```text
  Ingest doc → chunk → embed → UPSERT document_chunks
  User query → embed query → SQL top-k + tenant filter → LLM prompt + citations
```

```python
def retrieve_context(tenant_id: str, query_embedding, k=5):
    sql = """
        SELECT document_id, chunk_index, content
        FROM document_chunks
        WHERE tenant_id = %s
        ORDER BY embedding <=> %s::vector
        LIMIT %s
    """
    with pool.connection() as conn:
        return conn.execute(sql, (tenant_id, query_embedding, k)).fetchall()
```

---

## When to use / avoid

| PostgreSQL + pgvector | Cosmos DB vectors |
|-----------------------|-------------------|
| Relational metadata, joins, ACID | Global distribution, change feed native |
| Existing Postgres ops team | Document-native flexible schema |
| Complex SQL filters | Multi-region write patterns |

---

## ⚠️ Exam traps

1. **Index metric mismatch** — cosine index but L2 query operator.
2. **No tenant filter** in SQL — cross-tenant data leak in RAG.
3. **Undersized memory** — HNSW performance collapses.
4. **No connection pooling** — latency and connection exhaustion under load.
5. **Re-embedding without version column** — can't roll back index changes.

---

## Checkpoint questions

**Q1.** Need RAG with `tenant_id` + `department` filters and SQL reporting. Best store?  
<details><summary>Answer</summary>PostgreSQL + pgvector with JSONB metadata and composite indexes.</details>

**Q2.** Vector queries slow after 10M rows. Levers?  
<details><summary>Answer</summary>Partition by tenant, tune HNSW/IVFFlat, scale compute/memory, optimize pool.</details>

**Q3.** Improved embedding model (new dimensions). Migration?  
<details><summary>Answer</summary>Versioned re-embed column or table; rebuild index; cut over after validation.</details>

---

## Skills checklist (official A2)

- [ ] Connect/query via SDK/drivers
- [ ] Schema, data types, indexing strategies
- [ ] Reduce pgvector compute overhead; optimize latency
- [ ] Size compute, memory, storage for vectors
- [ ] Vector search + RAG with metadata filters
- [ ] Connection optimization

---

## Next topic

[04 — Azure Managed Redis](./04-azure-managed-redis.md)
