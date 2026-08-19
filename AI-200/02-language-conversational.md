# Azure AI Cloud Developer Associate: Azure Data Management for AI Solutions

For AI apps, “data management” means everything around your data: where it lives, how it gets ingested, cleaned, versioned, secured, and prepared for model calls (including retrieval/indexing pipelines).

This is the part of AZ-204 that maps to AI: reliable backend data pipelines that feed your AI services.

## What you should understand
- Data ingestion and transformation workflows that support AI features.
- Data governance basics: PII handling, retention, and secure access patterns.
- How to design for updates/deletes/reprocessing (so your AI doesn’t use stale data).

## Topics checklist
- [ ] Plan data sources and ownership (batch vs streaming, expected update frequency)
- [ ] Build an ingestion/transformation pipeline (ETL/ELT-style thinking)
- [ ] Normalize data formats into model-ready inputs (schemas, validation)
- [ ] Handle incremental updates and backfills safely
- [ ] Support deletes/updates so retrieval doesn’t return removed content
- [ ] Store and use metadata needed for filtering/ranking
- [ ] Prepare text/image data for downstream AI steps (e.g., chunking for embeddings)
- [ ] PII/privacy patterns (minimize storage, redact before logging/indexing)
- [ ] Secure access to storage/DB (managed identity / RBAC)
- [ ] Data lineage/versioning so you can reproduce outputs

## Exam-style practice (10 questions + answers)
### Question 1
You’re building an AI feature over documents stored in Azure Blob Storage. What’s the most important first step in the data pipeline?

**Answer (model):**
Define the ingestion and transformation plan: document-to-model-ready steps, including schema/validation and metadata extraction, before you generate embeddings or call AI services.

### Question 2
Your data changes daily. How do you avoid the “stale index” problem for retrieval-based answers?

**Answer (model):**
Implement an update strategy: incremental ingestion + reprocessing of only changed content, and ensure your index/derived artifacts are updated (including handling deletions).

### Question 3
Your organization prohibits storing raw PII in analytics logs. What should you do before data reaches logs or index structures?

**Answer (model):**
Apply **PII minimization/redaction** early in the pipeline: detect and remove/replace sensitive fields before logging and before storing content used for retrieval (or store only non-sensitive derivatives).

### Question 4
Why is it useful to store metadata alongside AI embeddings/vector entries?

**Answer (model):**
Metadata enables filtering (e.g., by tenant, document type, date), improves answer relevance, and supports governance/auditing by linking retrieved content back to original sources.

### Question 5
You discover the ingestion pipeline occasionally duplicates records. What’s a backend-safe mitigation?

**Answer (model):**
Use idempotent ingestion: dedup keys (e.g., document ID + version), upsert semantics, and correlation IDs so reruns don’t create duplicates or double-charge downstream processing.

### Question 6
How do you design for “backfill” when you improve your chunking strategy?

**Answer (model):**
Treat it as a versioned reprocessing job: re-run transformation from a known input version, generate new derived artifacts under a new version, and then switch traffic only after validation.

### Question 7
Your AI pipeline fails halfway through processing a large dataset. What should the pipeline support?

**Answer (model):**
Checkpointing and retryability: the ability to resume safely (at chunk/document boundaries) without corrupting outputs or producing inconsistent duplicates.

### Question 8
Why should your backend validate data schemas before sending data to AI services?

**Answer (model):**
Validation prevents malformed inputs from causing wasted cost, confusing model errors, or broken downstream logic. It also improves observability because you can catch issues at ingestion time.

### Question 9
For large inputs, what’s a general approach to prepare them for embedding/retrieval pipelines?

**Answer (model):**
Chunk and batch: split inputs into appropriately sized units with overlap as needed, and process in controlled batches so latency, memory, and costs remain manageable.

### Question 10
How do you keep your AI app reproducible when models or prompts change?

**Answer (model):**
Version the artifacts: log which input data version produced which embeddings/index entries, and correlate them with the model/prompt/deployment version used for inference.

