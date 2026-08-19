# Azure AI Cloud Developer Associate: Generative AI (Azure OpenAI) & RAG

## Topics checklist
### Generative AI
- [ ] Chat-based prompting vs completion-based prompting
- [ ] Prompt engineering fundamentals (instructions, constraints, role/system messages)
- [ ] Few-shot prompting and examples (when helpful, when harmful)
- [ ] Token/context window concepts (truncation, summarization strategies)
- [ ] Function/tool calling (structured outputs, tool invocation patterns)
- [ ] Retrieval grounding concepts (reducing hallucinations with evidence)
- [ ] Prompt orchestration & workflows (e.g., using Prompt Flow-style pipelines for repeatable runs)
- [ ] Latency and cost drivers (tokens, response length, number of calls)

### RAG (Retrieval-Augmented Generation)
- [ ] Chunking strategy basics (chunk size/overlap tradeoffs)
- [ ] Embeddings fundamentals (what embeddings are; choosing an embeddings approach)
- [ ] Building an Azure AI Search index for RAG
- [ ] Vector search basics (vector fields, similarity, and query-time embedding)
- [ ] Hybrid search concepts (keyword + vector) and when to use it
- [ ] Semantic ranking/reranking concepts (improving retrieval quality)
- [ ] Query rewriting / conversational query enrichment patterns
- [ ] Returning answers with citations (at least conceptually: mapping answer->sources)
- [ ] Managing ingestion pipelines (updates, deletions, re-indexing strategy)
- [ ] Handling retrieval failures (empty results, low confidence, fallback behavior)

## Exam-style practice (with answers)
### Question 1
Your chatbot confidently answers a question, but the answer is not supported by your knowledge base. What’s the most direct design improvement to reduce this failure?

**Answer (model):**
Strengthen **retrieval grounding**: implement or improve **RAG** so the model answers using retrieved evidence, and return (or internally enforce) **citations/sources**. Then add retrieval filtering/ranking (hybrid search, semantic ranking, reranking) so the right evidence is retrieved more reliably.

### Question 2
Why might you choose **hybrid search** (keyword + vector) instead of only vector search for RAG?

**Answer (model):**
Because hybrid search can improve recall and relevance: keywords help with exact terms/IDs/names, while vectors capture semantic similarity. Together they usually outperform either approach alone in messy real-world corpora.

