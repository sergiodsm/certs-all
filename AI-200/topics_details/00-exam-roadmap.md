# AI-200 Exam Roadmap

**Exam:** AI-200 — Developing AI Cloud Solutions on Azure  
**Credential:** Microsoft Certified: Azure AI Cloud Developer Associate  
**Replaces:** AZ-204 (retiring July 31, 2026)

Official study guide: [Microsoft Learn — AI-200](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200) (skills measured as of April 15, 2026)

---

## Exam snapshot

| Item | Detail |
|------|--------|
| Duration | 120 minutes (proctored; may include interactive items) |
| Passing score | **700 / 1000** |
| Questions | ~40–60 (scenario MCQ, multi-select, case studies) |
| Language | English |
| Renewal | Annual — free assessment on Microsoft Learn |
| Practice assessment | Not currently available; use [exam sandbox](https://aka.ms/examdemo) |
| Primary language | **Python + Azure SDKs** |

---

## Skills at a glance (study priority)

| Weight | Domain | Topic files |
|--------|--------|-------------|
| **25–30%** | Azure data management for AI | [02](./02-cosmos-db-nosql-ai.md) · [03](./03-postgresql-pgvector-rag.md) · [04](./04-azure-managed-redis.md) · [05](./05-rag-vector-retrieval.md) |
| **20–25%** | Containerized solutions | [06](./06-acr-app-service-containers.md) · [07](./07-container-apps-keda-aks.md) |
| **20–25%** | Connect & consume Azure services | [08](./08-service-bus-event-grid.md) · [09](./09-azure-functions-serverless.md) |
| **20–25%** | Secure, monitor, troubleshoot | [10](./10-key-vault-app-configuration.md) · [11](./11-opentelemetry-kql-troubleshooting.md) · [12](./12-responsible-ai-production.md) |
| Cross-cutting | SDK, auth, reliability | [01](./01-foundation-sdk-python.md) |

---

## Recommended study timelines

### 4-week plan (10–15 hrs/week)

| Week | Focus | Deliverable |
|------|-------|-------------|
| 1 | [01 Foundation](./01-foundation-sdk-python.md) + [02 Cosmos DB](./02-cosmos-db-nosql-ai.md) | Lab 01 + Lab 02 |
| 2 | [03 PostgreSQL](./03-postgresql-pgvector-rag.md) + [05 RAG](./05-rag-vector-retrieval.md) | Lab 03 |
| 3 | [08 Messaging](./08-service-bus-event-grid.md) + [09 Functions](./09-azure-functions-serverless.md) | Lab 04 |
| 4 | [06–07 Containers](./06-acr-app-service-containers.md) + [10–11 Ops](./10-key-vault-app-configuration.md) | Labs 05–06 + [scenarios](../topics_details/examples/scenarios-walkthrough.md) |

### 2-week cram (20+ hrs/week)

1. Skim [01](./01-foundation-sdk-python.md) — auth + retries only if experienced
2. Deep dive **02 + 03 + 05** (largest weight)
3. **08 + 09** async patterns
4. **06 + 07** containers + KEDA
5. **10 + 11 + 12** + [exam-traps](./reference/exam-traps.md)

---

## How AI-200 differs from AZ-204

| AZ-204 emphasis | AI-200 emphasis |
|-----------------|-----------------|
| Broad Azure developer APIs | **AI data plane** (vectors, RAG, embeddings) |
| Application Insights as default | **OpenTelemetry** + **KQL** |
| General messaging | Messaging for **AI pipelines** (embed, reindex) |
| Containers (general) | Containers + **KEDA** for AI workloads |
| Less vector DB depth | **Cosmos DB, pgvector, Redis** vector features |

You still need developer fundamentals — they are assumed, not removed.

---

## Exam-day strategy

1. **Read the scenario fully** — AI-200 loves multi-step case studies (ingest → queue → embed → deploy → monitor).
2. **Name the Azure service** — if the question mentions DLQ, think Service Bus; revision traffic split → Container Apps; RU spikes → Cosmos indexing/consistency.
3. **Pick the simplest secure option** — managed identity beats keys; Key Vault beats env secrets in images.
4. **Watch "always/never" traps** — Redis is not only cache; Event Grid is not a work queue.
5. **Flag time** — data-management questions are dense; don't stall on one item.

---

## Readiness bar

Before scheduling:

- [ ] Score ≥8/10 on practice questions in each [topic file](./README.md)
- [ ] Complete at least **4 labs** end-to-end
- [ ] Can explain [service chooser](./reference/service-chooser.md) without notes
- [ ] Can write basic **KQL** for errors and p95 latency
- [ ] Walk [scenarios walkthrough](./examples/scenarios-walkthrough.md) aloud in under 30 minutes

---

## File map (this guide)

| Layer | Location |
|-------|----------|
| Quick modules + Q&A | `../01-fundamentals.md` … `../06-evaluation-responsible-deployment.md` |
| Deep dives + examples | `./` (this folder) |
| Instructor AI prompt | `../AI-200-INSTRUCTOR.md` |
| Index | `../AI-200-topics.md` |
