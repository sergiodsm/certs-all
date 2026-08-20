# AI-200 Exam Traps

High-frequency wrong answers. Read before exam day.

---

## Security & auth

1. **Connection strings in code/images** — wrong; use MI + Key Vault.
2. **Key Vault Contributor for app** — over-privileged; use **Secrets User**.
3. **Logging full prompts for debugging** — PII/governance fail in scenarios.

---

## Data & RAG

4. **Different embedding model at query vs index** — irrelevant retrieval.
5. **No tenant filter in vector query** — data leak; always filter in multi-tenant.
6. **Redis as only source of truth** — wrong for durable compliance storage.
7. **Cache without invalidation** — stale answers after doc update.
8. **Eventual consistency** when user must read own upload immediately.
9. **Ignoring change feed** — stale index after Cosmos updates.

---

## Messaging

10. **Event Grid as work queue** — use Service Bus for durable jobs.
11. **No dead-letter handling** — infinite retry on poison messages.
12. **Retry without idempotency** — duplicate embeddings/cost.

---

## Containers

13. **CPU autoscale only** for queue workers — **KEDA on queue depth**.
14. **Secrets in Dockerfile ENV** — visible in layers.
15. **No readiness probe** — traffic to broken starting instances.
16. **`:latest` in production** — can't rollback safely.

---

## Functions

17. **15-minute embed on Consumption plan** — timeout; use worker tier.
18. **Trigger vs binding confusion** — trigger starts execution; binding is I/O.

---

## Monitoring

19. **App Insights SDK only** when question specifies **OpenTelemetry**.
20. **KQL on wrong table** — `dependencies` for latency, `requests` for HTTP outcomes.

---

## Responsible AI

21. **Retrieved HTML as system instructions** — prompt injection failure.
22. **Production metrics only** — need **offline eval** for regression.
23. **Ship prompt change without version ID** — can't troubleshoot quality drop.

---

## General exam strategy

24. **Most complex service** — exam often wants simplest secure pattern.
25. **AZ-204-only trivia** — Cognitive Services speech/vision are not primary AI-200 domains unless scenario explicitly needs them.

---

## If you remember only five

1. **Managed identity** beats keys.  
2. **Service Bus + DLQ + idempotency** for async AI work.  
3. **KEDA** scales queue workers.  
4. **OpenTelemetry + KQL** for triage.  
5. **Tenant filter + same embedding model** for RAG.
