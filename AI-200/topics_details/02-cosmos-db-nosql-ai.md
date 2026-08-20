# Topic 02 — Azure Cosmos DB for NoSQL (AI Workloads)

> **Domain A (25–30%)** — official skill A1  
> **Module:** [`../02-language-conversational.md`](../02-language-conversational.md)  
> **Lab:** [labs/02-cosmos-vector-change-feed.md](./labs/02-cosmos-vector-change-feed.md)

---

## In one sentence

**Cosmos DB for NoSQL** stores application and vector data globally; you connect with the **Python SDK**, tune **RUs** via indexing and **consistency**, run **vector similarity search**, and keep AI indexes fresh with the **change feed**.

---

## Why it exists on the exam

Cosmos DB is Microsoft's primary globally distributed NoSQL store with first-class **vector search** and **change feed** — both appear explicitly in the AI-200 skills outline.

---

## How it works in Azure

### Document model for AI

```json
{
  "id": "doc-1001-chunk-3",
  "partitionKey": "tenant-acme",
  "documentId": "doc-1001",
  "chunkIndex": 3,
  "text": "Refund policy allows returns within 30 days...",
  "embedding": [0.012, -0.034, "..."],
  "metadata": {
    "category": "policy",
    "updatedAt": "2026-08-01T12:00:00Z"
  }
}
```

**Partition key:** Choose for even distribution and query scope (often `tenantId` or `documentId`).

### SDK: query with parameters

```python
query = """
SELECT c.id, c.text, c.metadata
FROM c
WHERE c.partitionKey = @tenant
  AND c.metadata.category = @category
"""
items = container.query_items(
    query=query,
    parameters=[
        {"name": "@tenant", "value": "tenant-acme"},
        {"name": "@category", "value": "policy"},
    ],
    partition_key="tenant-acme",
)
```

### Indexing policy & RUs

- **Include/exclude paths** in indexing policy — index only fields you filter/sort on.
- Unindexed filter paths → expensive scans → **high RU** charge.
- **Composite indexes** when filtering + ordering on multiple properties.

### Consistency levels (exam favorites)

| Level | Guarantee | AI use case |
|-------|-----------|-------------|
| **Strong** | Latest write globally | Rare; costly |
| **Session** | Read your writes in session | Default for many apps |
| **Bounded staleness** | Max lag window | Acceptable for analytics |
| **Eventual** | Lowest read cost | Read-heavy, stale OK |

⚠️ "User must immediately see their uploaded doc in search" → need **session** or stronger for that user's reads.

### Vector similarity search

Conceptual flow (exact API evolves — verify GA docs):

1. Store `embedding` vector on documents.
2. Create **vector index** policy on embedding path.
3. Query with `VectorDistance` or SDK vector query API for top-k neighbors.

```python
# Illustrative — confirm syntax on Microsoft Learn for your SDK version
vector_query = {
    "vector": query_embedding,
    "k": 5,
    "fields": "embedding",
}
# Execute via Cosmos DB vector search API / query
```

**Exam point:** Same embedding model/dimensions at index and query time.

### Change feed processor

```text
  Cosmos DB container
        │
        ▼ (ordered per partition)
  Change feed
        │
        ▼
  Processor (Function / Container worker)
        │
        ├── new/updated → re-embed → upsert vector index
        └── deleted → remove from derived store
```

```python
# Pattern: azure-cosmos ChangeFeedProcessor (conceptual)
# Lease container stores processor state for scale-out
```

**Why:** Avoids nightly full reindex; processes only deltas.

---

## When to use / avoid

| Choose Cosmos DB | Consider PostgreSQL instead |
|------------------|----------------------------|
| Global distribution, multi-region | Complex relational joins |
| Flexible JSON + vectors + change feed | Heavy SQL analytics |
| Massive scale, tunable consistency | Team already standardized on pgvector |

---

## ⚠️ Exam traps

1. **Wrong partition key** → hot partitions, throttling (429).
2. **Filtering on unindexed field** → RU explosion.
3. **Eventual consistency** when user expects read-your-write.
4. **Change feed ignored** → stale RAG answers after updates.
5. **Vector dimensions mismatch** → garbage similarity scores.

---

## Checkpoint questions

**Q1.** RU costs spike after adding metadata filter. First check?  
<details><summary>Answer</summary>Indexing policy — ensure filtered properties are indexed; check partition scope.</details>

**Q2.** Documents updated in Cosmos; search still returns old text. Missing piece?  
<details><summary>Answer</summary>Change feed (or sync job) to re-embed/reindex on update/delete.</details>

**Q3.** Multi-region app; user uploads doc and searches immediately. Consistency?  
<details><summary>Answer</summary>Session (or stronger) for that flow — not pure eventual.</details>

---

## Skills checklist (official A1)

- [ ] Connect with SDK; run parameterized queries
- [ ] Optimize RUs: indexing policy, consistency
- [ ] Store embeddings; vector similarity search
- [ ] Change feed processor for new/updated items

---

## Next topic

[03 — PostgreSQL + pgvector](./03-postgresql-pgvector-rag.md)
