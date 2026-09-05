# Domain 5 practice — Implement information extraction solutions

**Exam:** AI-103 · Developing AI Apps and Agents on Azure  
**Weight:** 10–15% · Skills measured as of **April 16, 2026**  
**Coverage:** Study guide [`../study-guides/05-information-extraction.md`](../study-guides/05-information-extraction.md)

**How to use:** Cover the **Correct / Why** blocks and answer closed-book first. Unofficial study aids — not Microsoft exam dumps.

---

### Q1. Multimodal ingestion
A knowledge base includes PDFs, images, and training videos that must be searchable for grounding. What should you do first?

- A. Ingest and index documents, images, audio, and video into a retrieval pipeline
- B. Ignore non-text files permanently
- C. Only increase LLM temperature
- D. Only configure TTS voices

**Correct:** A  
**Why correct:** Ingestion/indexing of multimodal content is the foundation of grounding pipelines.  
**Why distractors fail:** B drops required content; C/D don’t index media.  
**Mapped skill:** 5.1 Ingest and index documents, images, audio, video  

---

### Q2. Hybrid search
Users ask conceptual questions and also search exact SKU codes. Which search configuration is most appropriate?

- A. Hybrid search combining vector/semantic similarity with keyword/exact matching
- B. Vector-only with no keyword path
- C. Keyword-only with no semantic capability when paraphrases dominate
- D. No index; paste entire catalogs into every prompt

**Correct:** A  
**Why correct:** Hybrid covers meaning and exact identifiers.  
**Why distractors fail:** B misses SKUs; C misses paraphrases; D doesn’t scale.  
**Mapped skill:** 5.1 Configure semantic, hybrid, and vector search  

---

### Q3. Enrichment skills
At index time you need OCR plus domain-specific tagging via an internal API. What pattern fits?

- A. Built-in enrichment skills plus a custom skill calling your API
- B. Only client-side CSS changes
- C. Only deleting the index nightly without enrichment
- D. Only raising rate limits on an unrelated storage account

**Correct:** A  
**Why correct:** Enrichment uses built-in and custom skills for text/images/layout and custom logic.  
**Why distractors fail:** B/C/D don’t enrich content.  
**Mapped skill:** 5.1 Enrichment with custom or built-in skills  

---

### Q4. RAG with scanned PDFs
Scanned policy PDFs yield empty chunks in RAG. What is missing?

- A. OCR as part of the RAG ingestion flow
- B. Higher video bitrate
- C. Disabling all embeddings
- D. Removing chunk metadata on purpose

**Correct:** A  
**Why correct:** Scanned documents require OCR during ingestion for RAG.  
**Why distractors fail:** B/C/D don’t extract text from scans.  
**Mapped skill:** 5.1 Configure RAG ingestion including OCR  

---

### Q5. Agent tool wiring
How should an agent reliably query the enterprise index?

- A. Connect retrieval pipelines directly as workflow steps or agent tools
- B. Ask the agent to guess document contents without retrieval
- C. Email PDFs to the model vendor for each turn
- D. Hardcode one stale paragraph in the system prompt forever

**Correct:** A  
**Why correct:** Retrieval should be connected to workflows and agent tools.  
**Why distractors fail:** B/C/D are unreliable or non-scalable.  
**Mapped skill:** 5.1 Connect retrieval to workflows and agent tools  

---

### Q6. Document field extraction (multi-select)
**Select 2.** Extracting invoice totals from complex scanned forms typically requires:

- A. OCR
- B. Layout analysis and field extraction
- C. Only TTS of the filename
- D. Only image watermark branding with no text extraction

**Correct:** A, B  
**Why correct:** Multimodal document pipelines combine OCR, layout, and field extraction.  
**Why distractors fail:** C/D don’t extract invoice fields.  
**Mapped skill:** 5.2 Multimodal pipelines: OCR, layout, field extraction  

---

### Q7. Content Understanding for RAG
You need clean, grounded document representations for agents rather than noisy raw OCR. What should you use?

- A. Content Understanding to produce clean grounded representations for agents/RAG
- B. Unvalidated binary blobs injected into prompts
- C. Random string truncation only
- D. Disable citations and sources

**Correct:** A  
**Why correct:** Content Understanding produces clean grounded representations for downstream agents/RAG.  
**Why distractors fail:** B/C/D reduce quality and trust.  
**Mapped skill:** 5.2 Clean grounded representations via Content Understanding  

---

### Q8. Analyzer outputs
Downstream reasoning works best with structured sections and markdown headings from manuals. What should analyzers produce?

- A. Structured or markdown outputs for downstream reasoning
- B. Only encrypted audio with no text form
- C. Only pixel noise
- D. Only empty JSON arrays always

**Correct:** A  
**Why correct:** Analyzers generating structured/markdown outputs are in the skills list.  
**Why distractors fail:** B/C/D aren’t usable reasoning inputs.  
**Mapped skill:** 5.2 Analyzers for structured or markdown outputs  

---

### Q9. Semantic search role
When is configuring semantic search most helpful?

- A. When you need better relevance ranking/understanding of natural-language queries over candidates
- B. When you only need to resize images
- C. When you only configure TTS locale
- D. When you want to remove all indexes

**Correct:** A  
**Why correct:** Semantic search improves relevance for natural-language queries.  
**Why distractors fail:** B/C/D are unrelated.  
**Mapped skill:** 5.1 Configure semantic search for grounding  

---

### Q10. End-to-end scenario
Build grounding for an agent over scanned contracts and manuals: ingest with OCR/enrichment, hybrid search, Content Understanding cleanup, and search-as-tool. Which statement is true?

- A. This matches retrieval/grounding pipelines plus document extraction skills in AI-103
- B. Only a larger LLM without indexing fully replaces this architecture for private corpora
- C. Safety filters alone create a search index
- D. Video generation replaces document field extraction

**Correct:** A  
**Why correct:** The described stack maps to sections 5.1 and 5.2.  
**Why distractors fail:** B ignores grounding needs; C/D confuse unrelated capabilities.  
**Mapped skill:** 5.1–5.2 End-to-end information extraction & grounding  

---

## Answer key

| Q | Answer |
|---|--------|
| 1 | A |
| 2 | A |
| 3 | A |
| 4 | A |
| 5 | A |
| 6 | A, B |
| 7 | A |
| 8 | A |
| 9 | A |
| 10 | A |

**Readiness:** Aim ≥8/10. Review [`../study-guides/05-information-extraction.md`](../study-guides/05-information-extraction.md) for misses.
