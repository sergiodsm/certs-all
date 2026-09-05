# Section 5 — Implement information extraction solutions (10–15%)

> **Exam:** AI-103 · Developing AI Apps and Agents on Azure  
> **Mapped skills:** 5.1–5.2 · [Official study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-103)  
> **Mock test:** [`../practice/domain-5-questions.md`](../practice/domain-5-questions.md)

## In one sentence

You ingest multimodal content into searchable indexes, enrich and ground it for RAG/agents, and extract structured fields from documents with OCR, layout, and Content Understanding.

## Why it matters on the exam

This domain connects **Azure AI Search-style pipelines** to agents. Know search modes (semantic / hybrid / vector), enrichment skills, OCR in RAG ingestion, and Content Understanding analyzers for structured/markdown outputs.

## Mental model

```text
  Documents / images / audio / video
              │
              ▼
     Ingest → enrich (skills) → index (keyword + vector)
              │
              ▼
     Retrieve (semantic / hybrid / vector) → ground agents & RAG
              │
              ▼
     Document extraction: OCR + layout + fields
     Content Understanding → clean grounded text / markdown / JSON
```

## Topics checklist

### 5.1 Retrieval and grounding pipelines

- [ ] Ingest and index documents, images, audio, video
- [ ] Configure **semantic**, **hybrid**, and **vector** search
- [ ] Enrichment with custom or built-in skills (text, images, layout)
- [ ] RAG ingestion including documents + **OCR**
- [ ] Connect retrieval to workflows and **agent tools**

### 5.2 Extract content from documents

- [ ] Multimodal extraction: OCR + layout analysis + field extraction
- [ ] Clean grounded representations for agents/RAG via Content Understanding
- [ ] Analyzers for structured or **markdown** outputs for downstream reasoning

---

## Key concepts

### Search modes for grounding

| Mode | Strength |
|------|----------|
| Vector | Meaning similarity |
| Keyword | Exact tokens, filters, facets |
| Hybrid | Combine both — common enterprise default |
| Semantic | Ranking/understanding query intent over candidates |

⚠️ **Exam trap:** “Only vector search” when the query needs SKUs, invoice IDs, or hybrid filters.

### Enrichment skills

- Built-in skills: OCR, key phrases, language detection, image analysis, layout, etc.
- Custom skills: call your own API/function for domain enrichment.
- Enrichment runs at **index time** so query time stays fast and consistent.

### RAG ingestion with OCR

```text
  PDF/image → OCR / layout → chunk → embed → index → retrieve → generate
```

- Scanned PDFs fail silently without OCR.
- Preserve structure (headings, tables) when possible for better chunking and citations.
- Monitor ingestion quality: failed documents, empty OCR, stale indexes.

### Connecting retrieval to agents

- Expose search as an **agent tool** (function) with query parameters and filters.
- Or bind retrieval inside a workflow step before generation.
- Return chunk text + metadata (source, page, score) for grounded answers.

### Document extraction & Content Understanding

| Capability | Output |
|------------|--------|
| OCR | Text from images/scans |
| Layout analysis | Reading order, tables, regions |
| Field extraction | Key-value / structured fields |
| Content Understanding analyzers | Clean text, markdown, structured JSON for agents/RAG |

Use Content Understanding when you need **grounded, clean representations** — not just raw OCR dumps — for downstream reasoning.

## Common mistakes

- Indexing raw binary without enrichment/OCR.
- Chunking without layout awareness (tables shredded into nonsense).
- Building RAG without wiring search as a tool/workflow step for agents.
- Asking the LLM to “read the PDF” live at scale instead of ingesting once.

## Study focus order

1. Ingest → enrich → index → hybrid/semantic/vector retrieve (5.1)  
2. OCR in RAG pipelines (5.1)  
3. Layout + field extraction + Content Understanding outputs (5.2)

## Check your understanding

You must ground an agent on scanned invoices and product manuals. Sketch ingestion, enrichment, search type, and how the agent calls retrieval.
