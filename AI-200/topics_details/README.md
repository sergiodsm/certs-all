# AI-200 Complementary Study Guide

**Exam:** AI-200 — Developing AI Cloud Solutions on Azure  
**Companion to:** [`../AI-200-topics.md`](../AI-200-topics.md) and [`../AI-200-INSTRUCTOR.md`](../AI-200-INSTRUCTOR.md)

This folder is a **professor-style guide**: explanations, Python examples, labs, and exam traps that the module summaries alone do not teach. Use **both** the root modules and these files together.

| Resource | Role |
|----------|------|
| `../AI-200-topics.md` | Index, exam weights, readiness checklist |
| `../01`–`06` modules | Condensed topics + 10 practice Q&A each |
| `./topics_details/` (here) | Deep dives, code, labs, scenarios |
| `../AI-200-INSTRUCTOR.md` | Prompt for AI-guided tutoring |

> Skills measured as of **April 15, 2026**. Re-check: [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200).

---

## How to use this guide

1. Read [00-exam-roadmap.md](./00-exam-roadmap.md) and pick a timeline.
2. Study topics **01 → 12** in order (or start at your weakest official domain).
3. Complete labs in [`labs/`](./labs/) — scenario questions reward hands-on reasoning.
4. Memorize [service-chooser.md](./reference/service-chooser.md) and [exam-traps.md](./reference/exam-traps.md).
5. Walk [scenarios-walkthrough.md](./examples/scenarios-walkthrough.md) before scheduling the exam.

---

## Topic files (official syllabus order)

### Foundation

| # | File | Official skill |
|---|------|----------------|
| 0 | [00-exam-roadmap.md](./00-exam-roadmap.md) | Strategy, weights, timeline |
| 1 | [01-foundation-sdk-python.md](./01-foundation-sdk-python.md) | Python SDK, Entra ID, MI, retries, logging |

### Domain A — Data management for AI (25–30%)

| # | File | Official skill |
|---|------|----------------|
| 2 | [02-cosmos-db-nosql-ai.md](./02-cosmos-db-nosql-ai.md) | Cosmos DB SDK, RUs, vectors, change feed |
| 3 | [03-postgresql-pgvector-rag.md](./03-postgresql-pgvector-rag.md) | PostgreSQL, pgvector, RAG, sizing |
| 4 | [04-azure-managed-redis.md](./04-azure-managed-redis.md) | Cache, invalidation, Redis vector index |
| 5 | [05-rag-vector-retrieval.md](./05-rag-vector-retrieval.md) | Chunking, hybrid search, grounding, eval |

### Domain B — Containerized solutions (20–25%)

| # | File | Official skill |
|---|------|----------------|
| 6 | [06-acr-app-service-containers.md](./06-acr-app-service-containers.md) | ACR, ACR Tasks, App Service containers |
| 7 | [07-container-apps-keda-aks.md](./07-container-apps-keda-aks.md) | Container Apps, KEDA, AKS manifests |

### Domain C — Connect & consume services (20–25%)

| # | File | Official skill |
|---|------|----------------|
| 8 | [08-service-bus-event-grid.md](./08-service-bus-event-grid.md) | Service Bus, Event Grid, DLQ |
| 9 | [09-azure-functions-serverless.md](./09-azure-functions-serverless.md) | Triggers, bindings, deploy |

### Domain D — Secure, monitor, troubleshoot (20–25%)

| # | File | Official skill |
|---|------|----------------|
| 10 | [10-key-vault-app-configuration.md](./10-key-vault-app-configuration.md) | Key Vault rotation, App Configuration |
| 11 | [11-opentelemetry-kql-troubleshooting.md](./11-opentelemetry-kql-troubleshooting.md) | OpenTelemetry, KQL, triage |
| 12 | [12-responsible-ai-production.md](./12-responsible-ai-production.md) | PII, injection, versioning, eval |

---

## Labs

| Lab | Topic |
|-----|-------|
| [labs/01-local-azure-auth.md](./labs/01-local-azure-auth.md) | DefaultAzureCredential, RBAC, local vs cloud |
| [labs/02-cosmos-vector-change-feed.md](./labs/02-cosmos-vector-change-feed.md) | Cosmos queries, vectors, change feed |
| [labs/03-postgresql-pgvector-rag.md](./labs/03-postgresql-pgvector-rag.md) | Schema, pgvector search, metadata filter |
| [labs/04-service-bus-functions-pipeline.md](./labs/04-service-bus-functions-pipeline.md) | Queue → Function → embed worker |
| [labs/05-container-apps-deploy.md](./labs/05-container-apps-deploy.md) | ACR build, Container Apps + KEDA |
| [labs/06-keyvault-telemetry-kql.md](./labs/06-keyvault-telemetry-kql.md) | Secrets, OTel, KQL queries |

---

## Reference & examples

| File | Purpose |
|------|---------|
| [reference/service-chooser.md](./reference/service-chooser.md) | When to use which Azure service |
| [reference/exam-traps.md](./reference/exam-traps.md) | High-frequency wrong answers |
| [reference/glossary.md](./reference/glossary.md) | Exam vocabulary |
| [reference/checklist.md](./reference/checklist.md) | Pre-exam mastery checklist |
| [examples/python-snippets.md](./examples/python-snippets.md) | Copy-paste SDK patterns |
| [examples/scenarios-walkthrough.md](./examples/scenarios-walkthrough.md) | End-to-end case study reasoning |

---

## Mental model

AI-200 tests whether you can build and **operate** an AI backend on Azure:

```text
  Auth (MI) → Data (Cosmos/Postgres/Redis) → RAG → Async (Bus/Grid/Functions)
       → Containers (ACR/Apps/AKS) → Secrets/Config → OTel/KQL → Safe AI
```

If you can walk that pipeline for a new document-ingestion feature under exam time pressure, you pass.
