# Module 03 — Vector Databases & Retrieval (RAG)

> **Exam domain:** Retrieval patterns on Azure data services (extends **25–30%** data domain)  
> **File:** `03-vision-docs.md`

## In one sentence

**RAG** grounds model answers in your data: chunk documents, compute **embeddings**, store them in Cosmos DB / PostgreSQL / Redis, retrieve by **similarity + metadata filters**, and pass evidence to the model with **citations** — while handling updates, empty results, and injection risk.

## Why it exists

Vector storage alone isn't enough. AI-200 scenarios ask how you **design the retrieval pipeline** — chunking, same embedding model at index and query time, hybrid keyword+vector search, tenant isolation, and safe behavior when confidence is low.

## RAG pipeline

```text
  Source docs (Blob, DB, API)
           │
           ▼
    Chunk + metadata extract
           │
           ▼
    Embed (same model as query-time)
           │
           ▼
    Vector store (+ optional keyword index)
           │
  User query ──► embed query ──► top-k + filters ──► prompt with context ──► answer + citations
```

## Topics checklist

- [ ] Embeddings as semantic representations; **same model/parameters** at index and query
- [ ] **Chunking** size/overlap tradeoffs
- [ ] **Vector similarity search** with top-k and score thresholds
- [ ] **Metadata filtering** for multi-tenant and security boundaries
- [ ] **Hybrid retrieval** (keyword + vector) when exact terms/IDs matter
- [ ] **Citations / source mapping** for traceability
- [ ] Ingestion, **reindex**, and **delete** propagation
- [ ] Fallbacks for empty or low-confidence retrieval
- [ ] Offline **evaluation** before shipping pipeline changes
- [ ] **Prompt injection** via retrieved text — treat chunks as untrusted data

## Key concepts

### Chunking

| Setting | Too small | Too large |
|---------|-----------|-----------|
| Chunk size | Loses context | Dilutes relevance; hits token limits |
| Overlap | May miss boundary context | Higher storage/cost |

Rule of thumb: chunks should be **self-contained enough** to answer a focused question about one topic.

### Hybrid retrieval

Use **vector** for semantic match; add **keyword/BM25** (or Azure AI Search hybrid) when users query SKUs, error codes, or proper nouns that embeddings miss.

### Grounding reduces hallucination

Instruct the model to answer **from retrieved context only**; return "insufficient information" when evidence doesn't support an answer. Surface **citations** (document ID, chunk ID, title).

### Safe fallback matrix

| Condition | Backend behavior |
|-----------|-------------------|
| Zero results | Clarify query, broaden search, or honest "don't know" |
| Low similarity scores | Don't force an answer; optional human escalation |
| Stale index | Prefer sync jobs / change feed; monitor lag |

⚠️ **Exam trap:** Mismatch between embedding model at index time vs query time → irrelevant retrieval.

⚠️ **Exam trap:** Retrieved HTML/docs containing "ignore previous instructions" — **instruction/data separation** required.

## Exam-style practice (10 questions + answers)

### Question 1
Difference between an **embedding** and a **vector database/index**?

**Answer:**
An **embedding** is a numeric vector for content. A **vector store** persists embeddings and runs **similarity search** efficiently.

### Question 2
Retrieval returns irrelevant chunks. First backend checks?

**Answer:**
**Embedding model parity** (index vs query), **chunking** config, and metadata filters — not immediately blaming the LLM.

### Question 3
Why use chunk **overlap**?

**Answer:**
Preserves context across boundaries so queries matching edge content still retrieve complete thought units.

### Question 4
Users search by exact product SKU. When consider hybrid retrieval?

**Answer:**
When **exact term match** matters — combine keyword + vector for recall on IDs/SKUs and semantic paraphrases.

### Question 5
Metadata filters in multi-tenant apps?

**Answer:**
Constrain every query by **tenant/security scope** so retrieval never crosses tenant boundaries.

### Question 6
Vector search returns nothing useful. What should the backend do?

**Answer:**
**Safe fallback** — clarify, broaden, switch strategy, or state low confidence; don't let the model guess unchecked.

### Question 7
Why plan deletes in the retrieval pipeline?

**Answer:**
Otherwise you serve **removed or outdated** content — wrong answers and policy violations.

### Question 8
Requirement: explain where an answer came from.

**Answer:**
Return **citations** mapped to retrieved chunk/document IDs for audit and user trust.

### Question 9
Reduce hallucination in RAG?

**Answer:**
**Ground** on retrieved evidence; constrain answers to context; require citations where appropriate.

### Question 10
Practical test before shipping new chunking or embedding settings?

**Answer:**
**Offline evaluation set** — measure relevance/coverage/regressions vs baseline before production rollout.

## What's next

Module **04** covers async ingestion and processing with **Service Bus**, **Event Grid**, and **Azure Functions**.

## Deep dive (examples & labs)

- [Topic 05 — RAG & vector retrieval](./topics_details/05-rag-vector-retrieval.md)
- [Lab 03 — pgvector RAG](./topics_details/labs/03-postgresql-pgvector-rag.md)
