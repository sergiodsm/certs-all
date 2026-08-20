# Azure AI Cloud Developer Associate (AI-200) — Study Index

Developer-focused study materials for **Exam AI-200: Developing AI Cloud Solutions on Azure**.

> **Start here:** [topics_details/README.md](./topics_details/README.md) — full guide with explanations, examples, and labs  
> **AI tutor:** [AI-200-INSTRUCTOR.md](./AI-200-INSTRUCTOR.md)

---

## Exam at a glance

| Detail | Value |
|--------|-------|
| Exam | AI-200 — Developing AI Cloud Solutions on Azure |
| Passing score | 700 / 1000 |
| Duration | 120 minutes |
| Study guide | [Microsoft Learn](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200) (April 15, 2026) |

---

## Two-layer study system

| Layer | Files | Use for |
|-------|-------|---------|
| **Quick modules** | `01`–`06` below | Review, drill 10 Q&A per domain |
| **Deep dive** | [`topics_details/`](./topics_details/) | Learn, examples, labs, exam traps |

---

## Official domains → modules → deep dives

| Weight | Domain | Module (summary + Q&A) | Topic files |
|--------|--------|-------------------------|-------------|
| Cross-cutting | SDK, Python, auth | [01-fundamentals](./01-fundamentals.md) | [01-foundation-sdk-python](./topics_details/01-foundation-sdk-python.md) |
| **25–30%** | Data management for AI | [02-data](./02-language-conversational.md) · [03-RAG](./03-vision-docs.md) | [02 Cosmos](./topics_details/02-cosmos-db-nosql-ai.md) · [03 Postgres](./topics_details/03-postgresql-pgvector-rag.md) · [04 Redis](./topics_details/04-azure-managed-redis.md) · [05 RAG](./topics_details/05-rag-vector-retrieval.md) |
| **20–25%** | Containers | [05-containers](./05-generative-rag.md) | [06 ACR/App Service](./topics_details/06-acr-app-service-containers.md) · [07 Apps/KEDA/AKS](./topics_details/07-container-apps-keda-aks.md) |
| **20–25%** | Messaging & Functions | [04-messaging](./04-speech.md) | [08 Bus/Grid](./topics_details/08-service-bus-event-grid.md) · [09 Functions](./topics_details/09-azure-functions-serverless.md) |
| **20–25%** | Security & monitoring | [06-ops](./06-evaluation-responsible-deployment.md) | [10 Key Vault/App Config](./topics_details/10-key-vault-app-configuration.md) · [11 OTel/KQL](./topics_details/11-opentelemetry-kql-troubleshooting.md) · [12 Responsible AI](./topics_details/12-responsible-ai-production.md) |

---

## Suggested study flow

1. Read [exam roadmap](./topics_details/00-exam-roadmap.md)
2. Study topic files **01 → 12** in order
3. Complete [labs](./topics_details/labs/) (minimum 4)
4. Review modules **01 → 06** for quick Q&A drill
5. [Scenarios walkthrough](./topics_details/examples/scenarios-walkthrough.md) + [exam traps](./topics_details/reference/exam-traps.md)
6. Mock session with [AI-200-INSTRUCTOR.md](./AI-200-INSTRUCTOR.md)

---

## Labs

| Lab | Skills |
|-----|--------|
| [01 Local auth](./topics_details/labs/01-local-azure-auth.md) | DefaultAzureCredential, RBAC |
| [02 Cosmos](./topics_details/labs/02-cosmos-vector-change-feed.md) | Queries, RUs, change feed |
| [03 pgvector RAG](./topics_details/labs/03-postgresql-pgvector-rag.md) | Schema, tenant filter |
| [04 Bus + Functions](./topics_details/labs/04-service-bus-functions-pipeline.md) | Async pipeline, DLQ |
| [05 Container Apps](./topics_details/labs/05-container-apps-deploy.md) | ACR, KEDA |
| [06 Vault + KQL](./topics_details/labs/06-keyvault-telemetry-kql.md) | Secrets, telemetry |

---

## Reference

- [Service chooser](./topics_details/reference/service-chooser.md)
- [Exam traps](./topics_details/reference/exam-traps.md)
- [Glossary](./topics_details/reference/glossary.md)
- [Pre-exam checklist](./topics_details/reference/checklist.md)
- [Python snippets](./topics_details/examples/python-snippets.md)
