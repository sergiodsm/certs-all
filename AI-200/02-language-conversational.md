# Module 02 — Azure Data Management for AI Solutions

> **Exam domain:** Develop AI solutions by using Azure data management services (**25–30%**)  
> **File:** `02-language-conversational.md`

## In one sentence

AI backends need the right **data plane**: **Cosmos DB for NoSQL + vectors**, **Azure Database for PostgreSQL with pgvector**, and **Azure Managed Redis** for cache and low-latency vector search — each with indexing, consistency, and sizing choices that affect cost and latency.

## Why it exists

This is the **largest weighted domain** on AI-200. The exam tests whether you can connect with SDKs, tune queries/RUs, store embeddings, run similarity search, process change feeds, and size resources for vector workloads — not just "use a vector DB."

## Service map (exam focus)

| Service | AI-200 highlights |
|---------|-------------------|
| **Azure Cosmos DB for NoSQL** | SDK queries, indexing policies, consistency levels, RU optimization, **vector similarity search**, **change feed** for incremental sync |
| **Azure Database for PostgreSQL** | Schema design, **pgvector** indexes, semantic search, **RAG with metadata filters**, compute/memory for vectors, connection pooling |
| **Azure Managed Redis** | Cache TTL/invalidation, **vector indexing** for similarity search, low-latency retrieval |

## Topics checklist

### Cosmos DB for NoSQL
- [ ] Connect and query with the **Python SDK**
- [ ] Tune **indexing policies** and **consistency levels** for read cost vs freshness
- [ ] Store embeddings; run **vector similarity search**
- [ ] Implement **change feed processor** for new/updated items (keep indexes fresh)

### Azure Database for PostgreSQL
- [ ] Connect/query via SDK or drivers with secure auth
- [ ] Model tables, choose types, design **pgvector** indexes (IVFFlat/HNSW — know tradeoffs exist)
- [ ] Optimize vector query latency; right-size **compute, memory, storage**
- [ ] Implement **RAG** patterns with **metadata filtering**
- [ ] **Connection optimization** (pooling, limits) for throughput

### Azure Managed Redis
- [ ] Cache with expiration and **invalidation** strategy
- [ ] **Vector indexing** for similarity search at the edge of hot paths

### Cross-cutting data pipeline
- [ ] Incremental updates, backfills, and **delete propagation** to derived indexes
- [ ] PII minimization before storage/logging
- [ ] Data lineage/versioning for reproducibility

## Key concepts

### Cosmos DB: consistency vs cost

| Consistency | Use when |
|-------------|----------|
| Strong | Reads must reflect latest write globally (higher latency/cost) |
| Session | Default for many apps; consistent within a session |
| Eventual | Highest read throughput; stale reads acceptable |

⚠️ **Exam trap:** Using the wrong consistency for "must read my own write" scenarios.

### Change feed → AI index sync

When documents change in Cosmos DB, a **change feed processor** emits create/update/delete events so your embedding pipeline reprocesses only what changed — avoiding full reindex on every update.

### PostgreSQL + pgvector for RAG

Typical pattern:

1. Store document chunks + embedding column + **metadata** (tenant, doc type, ACL)
2. Query: embed user question → `ORDER BY embedding <=> query_vector LIMIT k` with **WHERE tenant_id = @t**
3. Pass top chunks to the model with citation metadata

Size **compute and memory** for vector dimensions and index type; monitor query latency as data grows.

### Redis: cache vs vector index

- **Cache:** Session results, embedding lookups, rate-limit counters — always define TTL and invalidation on source updates.
- **Vector index:** Hot, low-latency retrieval layer; not a substitute for authoritative document storage.

## Exam-style practice (10 questions + answers)

### Question 1
You're building an AI feature over documents in Cosmos DB. Most important first pipeline step?

**Answer:**
Define **ingestion → chunk → embed → index** with schema validation and metadata extraction before calling embedding or inference services.

### Question 2
Data changes daily. How avoid a stale retrieval index?

**Answer:**
**Incremental updates** via change feed or comparable sync, reprocess changed items only, and **remove** embeddings when source documents are deleted.

### Question 3
Org policy forbids raw PII in analytics. What do before indexing?

**Answer:**
**Detect and redact/minimize PII** early — before logs, embeddings, or retrieval stores.

### Question 4
Why store metadata alongside embeddings?

**Answer:**
Enables **filtering** (tenant, type, date), improves relevance, and supports **audit/citations** back to source documents.

### Question 5
Ingestion occasionally duplicates records. Safe mitigation?

**Answer:**
**Idempotent ingestion** with natural keys (document ID + version), upsert semantics, and dedup on replay.

### Question 6
You improve chunking strategy. How design the backfill?

**Answer:**
**Versioned reprocessing job**: regenerate derived artifacts under a new version, validate, then cut over traffic.

### Question 7
Pipeline fails halfway through a large batch. What must it support?

**Answer:**
**Checkpointing** and safe resume at document/chunk boundaries without corrupt or duplicate outputs.

### Question 8
Why validate schemas before sending data to AI services?

**Answer:**
Prevents wasted cost, confusing model errors, and broken downstream logic; failures surface at ingestion time.

### Question 9
Cosmos DB RU costs spike on vector queries. What levers exist?

**Answer:**
Review **indexing policy**, query patterns, partition key design, consistency level, and item size; optimize hot queries and consider dedicated vector index configuration.

### Question 10
When prefer Redis vector indexing vs PostgreSQL pgvector for a hot retrieval path?

**Answer:**
Redis when you need **extremely low latency** on a bounded, frequently accessed corpus with cache-style lifecycle; PostgreSQL when you need **relational metadata, complex filters, and authoritative storage** in one system. (Exam: know Redis implements vector indexing for similarity search — not only key-value cache.)

## What's next

Module **03** goes deeper on retrieval design: chunking, hybrid search, grounding, and evaluation — the RAG layer on top of these data services.

## Deep dive (examples & labs)

- [Topic 02 — Cosmos DB for NoSQL AI](./topics_details/02-cosmos-db-nosql-ai.md)
- [Topic 03 — PostgreSQL + pgvector](./topics_details/03-postgresql-pgvector-rag.md)
- [Topic 04 — Azure Managed Redis](./topics_details/04-azure-managed-redis.md)
- [Labs 02–03](./topics_details/labs/02-cosmos-vector-change-feed.md)
