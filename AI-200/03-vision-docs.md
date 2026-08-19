# Azure AI Cloud Developer Associate: Vector Databases & Retrieval (RAG)

Vector databases power retrieval-based AI features by storing embeddings and returning the closest matches by similarity. In a cloud developer role, you must also design the retrieval pipeline: how you chunk data, compute embeddings, index it, query it, and handle retrieval failures safely.

## What you should understand
- Embeddings are numeric representations; vector DBs store them for similarity search.
- Retrieval pipelines must be updated when source data changes.
- Answers should be grounded: when possible, use retrieved sources rather than letting the model “guess”.

## Topics checklist
- [ ] What embeddings represent and why they enable semantic search
- [ ] Chunking strategy (size/overlap tradeoffs) for better retrieval
- [ ] Choosing query-time embedding behavior (same embedding model/params as indexing)
- [ ] Vector similarity search and query-time constraints (top-k, thresholds)
- [ ] Hybrid retrieval concepts (keyword + vector) when exact terms matter
- [ ] Metadata + filtering so retrieval respects tenant/security constraints
- [ ] Returning answers with traceability (citations / source mapping)
- [ ] Ingestion + reindex strategy (updates/deletes/backfills)
- [ ] Handling empty/low-confidence retrieval results (fallback behavior)
- [ ] Measuring retrieval quality (offline tests, relevance/coverage)

## Exam-style practice (10 questions + answers)
### Question 1
What’s the difference between “embedding” and a “vector database”?

**Answer (model):**
An **embedding** is a numeric vector representation of content. A **vector database** (or index) stores embeddings and provides similarity search to retrieve relevant items efficiently.

### Question 2
Your retrieval returns irrelevant chunks. What’s a common backend-side thing to check first?

**Answer (model):**
Check the pipeline consistency: the **embedding model/parameters** used at indexing time vs query time, and the **chunking** configuration (size/overlap). Inconsistent embeddings or poor chunking often cause irrelevant results.

### Question 3
Why is chunk overlap sometimes used when preparing documents for embeddings?

**Answer (model):**
Overlap helps preserve context across chunk boundaries, improving recall for queries that match content near edges of chunks.

### Question 4
Your users ask for answers referencing specific names/IDs that may not match semantically. When would you consider hybrid retrieval?

**Answer (model):**
When keyword/term matches matter. Hybrid retrieval (keyword + vector) often improves recall and relevance for exact terms while keeping semantic similarity.

### Question 5
How do metadata filters help in a multi-tenant AI app?

**Answer (model):**
Metadata filtering constrains retrieval to the right tenant/security scope so the system doesn’t return data from other tenants.

### Question 6
What should your backend do when the vector search returns no results or low confidence?

**Answer (model):**
Apply a **safe fallback**: ask a clarifying question, broaden the query, switch retrieval strategy (if available), or return a “no confident answer” response rather than forcing the model to guess.

### Question 7
Why should you plan for deletes/updates of source documents in a retrieval pipeline?

**Answer (model):**
If you don’t, your retrieval can return content that has been removed or updated. That causes incorrect answers and can violate governance/policy.

### Question 8
Your system must explain where an answer came from. What does this typically require?

**Answer (model):**
You need retrieval traceability: map each answer to retrieved sources (document IDs/chunk IDs) and surface them as citations or references so it’s auditable.

### Question 9
How do you reduce hallucination risk in a retrieval-based system?

**Answer (model):**
Ground responses using retrieved evidence and enforce source use when possible (e.g., require citations or constrain the model to answer only from retrieved context).

### Question 10
What’s a practical way to test retrieval changes before you ship them?

**Answer (model):**
Use an offline evaluation set of representative queries and track retrieval metrics (relevance/coverage). Run regression tests before deploying new chunking/index/embedding settings.

