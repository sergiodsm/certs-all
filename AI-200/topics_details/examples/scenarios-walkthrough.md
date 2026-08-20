# End-to-End Scenario Walkthrough

Practice explaining these aloud under exam time pressure (~5 min each).

---

## Scenario 1 — Document Q&A for enterprise tenants

**Requirements:**

- Multi-tenant SaaS; tenants must never see each other's docs
- 50k documents; daily updates
- Answers must cite sources
- Deploy on Azure with Python backend

**Walkthrough:**

1. **Ingest:** Blob upload → **Event Grid** → **Function** validates + enqueues **Service Bus** message.
2. **Process:** **Container Apps** worker ( **KEDA** on queue depth) chunks, embeds, upserts **PostgreSQL pgvector** with `tenant_id` + metadata.
3. **Sync:** On update/delete, re-embed or remove chunks; **Redis** cache invalidation for hot FAQs.
4. **Query API:** HTTP on **Container Apps** or App Service; MI auth to Postgres; retrieve with **`WHERE tenant_id = ?`**; RAG prompt with citations.
5. **Security:** Secrets in **Key Vault**; config in **App Configuration**; no PII in logs.
6. **Ops:** **OpenTelemetry** spans; **KQL** alerts on error rate and p95 latency.

**Trap answers to reject:**

- Redis as only database
- No tenant filter "because embeddings are semantic"
- Synchronous embed of 50k docs in HTTP request

---

## Scenario 2 — Global product catalog search

**Requirements:**

- Multi-region users
- JSON product docs with vectors
- Near real-time index updates

**Walkthrough:**

1. **Store:** **Cosmos DB for NoSQL** with partition key `tenantId` or `region`.
2. **Vectors:** Embeddings on Cosmos; vector similarity search GA API.
3. **Updates:** **Change feed processor** → re-embed changed items.
4. **Consistency:** **Session** for seller portal upload-then-search.
5. **Scale:** Indexing policy tuned for filter fields; monitor **RUs**.

**Trap:** Full nightly reindex only — wrong when change feed is an option.

---

## Scenario 3 — Rate limiting and cost control

**Symptoms:** Model returns 429; costs spiked after launch.

**Walkthrough:**

1. **Immediate:** Backoff retries, reduce worker concurrency.
2. **Architecture:** Queue embed jobs (**Service Bus**); **KEDA** max replicas cap.
3. **Cache:** **Redis** embedding cache keyed by content hash.
4. **Observability:** KQL on `dependencies` for 429 count; alert.
5. **Idempotency:** Prevent duplicate embed on client retries.

---

## Scenario 4 — Quality regression after prompt change

**Symptoms:** Answers worse after Friday deploy; no infrastructure alert.

**Walkthrough:**

1. Traces: filter by `prompt_version` attribute — compare error/quality proxies.
2. Check paired changes: retrieval index version, embedding model, prompt template.
3. **Offline eval set** should have caught this — add gate before prod.
4. Rollback Container Apps **revision** or revert App Configuration flag.
5. Process fix: version all artifacts; canary 10% traffic.

**Trap:** "Scale up Cosmos RUs" — irrelevant if quality not latency.

---

## Scenario 5 — Security audit findings

**Findings:**

- API keys in git
- Full user queries in Application Insights
- Retrieved wiki pages can manipulate bot behavior

**Remediation map:**

| Finding | Fix |
|---------|-----|
| Keys in git | Rotate keys; **Key Vault** + MI; scan repo |
| Queries in logs | Redact/minimize; log correlation ID only |
| Wiki manipulation | RAG instruction separation; content safety; trusted sources |

---

## Scenario 6 — Case study question strategy

When a case study spans 3+ screens:

1. List **constraints** (tenant isolation, latency, cost, compliance).
2. Map each requirement to **one Azure service** from [service-chooser](../reference/service-chooser.md).
3. Eliminate options with known **traps** ([exam-traps](../reference/exam-traps.md)).
4. Pick **simplest secure** architecture — don't over-engineer AKS if Container Apps suffices.

---

## Self-test

Explain Scenario 1 in under 5 minutes without looking at notes. If you stumble on messaging or KEDA, review topics **08** and **07**.
