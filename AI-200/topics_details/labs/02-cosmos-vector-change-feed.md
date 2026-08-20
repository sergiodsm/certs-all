# Lab 02 — Cosmos DB: Query, Vectors & Change Feed

**Topics:** [02-cosmos-db-nosql-ai.md](../02-cosmos-db-nosql-ai.md)  
**Time:** ~45 minutes

---

## Goal

Practice SDK queries, understand partition keys/RUs, and sketch a change-feed-driven reindex for RAG.

---

## Exercise A — Parameterized query

```python
from azure.identity import DefaultAzureCredential
from azure.cosmos import CosmosClient

client = CosmosClient("<url>", credential=DefaultAzureCredential())
container = client.get_database_client("aidb").get_container_client("chunks")

query = """
SELECT c.id, c.documentId, c.text
FROM c
WHERE c.tenantId = @tenant AND c.documentId = @docId
"""
items = list(container.query_items(
    query=query,
    parameters=[
        {"name": "@tenant", "value": "tenant-demo"},
        {"name": "@docId", "value": "doc-001"},
    ],
    partition_key="tenant-demo",
))
print(len(items), "chunks")
```

**Question:** What happens if you omit `partition_key` on a partitioned container?

---

## Exercise B — Indexing & RU (portal)

1. Open Cosmos account → Data Explorer → insert sample JSON with `tenantId`, `text`, `embedding`.
2. Run query with filter on unindexed field — observe **RU charge** in metrics.
3. Add included path to indexing policy for that field — rerun and compare RU.

---

## Exercise C — Change feed design (on paper)

Draw pipeline:

```text
  UPSERT document in Cosmos
        → change feed processor
        → embed changed chunks
        → upsert vector store / same container embedding field
```

List what happens on **DELETE** (tombstone in change feed → remove vectors).

---

## Verify understanding

- [ ] When to use session vs eventual consistency for upload-then-search
- [ ] Why partition key = `tenantId` for multi-tenant SaaS
- [ ] How change feed avoids full nightly reindex

---

## Exam tie-in

Scenario: "Documents updated but RAG stale" → answer **change feed processor**, not "lower consistency."
