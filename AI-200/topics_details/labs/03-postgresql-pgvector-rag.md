# Lab 03 — PostgreSQL pgvector RAG

**Topics:** [03-postgresql-pgvector-rag.md](../03-postgresql-pgvector-rag.md), [05-rag-vector-retrieval.md](../05-rag-vector-retrieval.md)  
**Time:** ~60 minutes

---

## Goal

Create a minimal RAG schema, insert mock embeddings, run similarity search with tenant filter.

---

## 1. Schema (Azure Portal Query editor or psql)

```sql
CREATE EXTENSION IF NOT EXISTS vector;

CREATE TABLE document_chunks (
    id BIGSERIAL PRIMARY KEY,
    tenant_id TEXT NOT NULL,
    document_id TEXT NOT NULL,
    chunk_index INT NOT NULL,
    content TEXT NOT NULL,
    embedding vector(3),  -- tiny dim for lab only; production = model dims
    metadata JSONB DEFAULT '{}'::jsonb,
    UNIQUE (tenant_id, document_id, chunk_index)
);

INSERT INTO document_chunks (tenant_id, document_id, chunk_index, content, embedding, metadata) VALUES
('acme', 'doc-1', 0, 'Returns within 30 days', '[1,0,0]', '{"category":"policy"}'),
('acme', 'doc-1', 1, 'Shipping takes 5-7 days', '[0.9,0.1,0]', '{"category":"policy"}'),
('beta', 'doc-9', 0, 'Secret beta feature', '[0,1,0]', '{"category":"internal"}');
```

---

## 2. Similarity query with tenant filter

```sql
-- Query vector near "returns policy" → use [1,0,0] as mock query embedding
SELECT document_id, content,
       embedding <=> '[1,0,0]' AS distance
FROM document_chunks
WHERE tenant_id = 'acme'
ORDER BY embedding <=> '[1,0,0]'
LIMIT 3;
```

Confirm `beta` tenant rows **never appear** when filtering `tenant_id = 'acme'`.

---

## 3. Python retrieval function

```python
import psycopg

def retrieve(conn, tenant_id: str, query_vector: list[float], k: int = 3):
    sql = """
        SELECT document_id, chunk_index, content
        FROM document_chunks
        WHERE tenant_id = %s
        ORDER BY embedding <=> %s::vector
        LIMIT %s
    """
    with conn.cursor() as cur:
        cur.execute(sql, (tenant_id, query_vector, k))
        return cur.fetchall()
```

---

## 4. RAG prompt assembly

Combine top chunks into a grounded prompt (see [05-rag-vector-retrieval.md](../05-rag-vector-retrieval.md)).

---

## Verify understanding

- [ ] Why `WHERE tenant_id` is mandatory in multi-tenant RAG
- [ ] `<=>` operator matches cosine index type
- [ ] Production dimensions must match embedding model output size

---

## Exam tie-in

"Semantic search with department metadata filter on PostgreSQL" → **pgvector + JSONB metadata + SQL WHERE**.
