# AI-200 Pre-Exam Checklist

## Domain A — Data (25–30%)

- [ ] Cosmos DB: SDK query, partition key, indexing policy, consistency, RUs
- [ ] Cosmos DB: vector search + change feed processor
- [ ] PostgreSQL: pgvector schema, HNSW/IVFFlat concept, metadata SQL filters
- [ ] PostgreSQL: connection pooling, sizing for vector RAM
- [ ] Redis: TTL cache, invalidation, vector index purpose
- [ ] RAG: chunking, hybrid search, citations, fallbacks, eval

## Domain B — Containers (20–25%)

- [ ] ACR push + ACR Tasks cloud build
- [ ] App Service container + Key Vault app setting reference
- [ ] Container Apps revisions + traffic split
- [ ] KEDA scaler on Service Bus queue
- [ ] AKS manifest deploy + kubectl logs/describe

## Domain C — Messaging (20–25%)

- [ ] Service Bus queue vs topic/subscription
- [ ] Dead-letter queue handling
- [ ] Event Grid for blob/custom events
- [ ] Functions: HTTP + Service Bus triggers, bindings, deploy

## Domain D — Security & ops (20–25%)

- [ ] Key Vault secret retrieve + rotation concept
- [ ] App Configuration labels + feature flags
- [ ] OpenTelemetry spans for RAG steps
- [ ] KQL: errors, p95 dependency latency, join requests/deps
- [ ] PII redaction, prompt injection, version tagging

## Cross-cutting

- [ ] DefaultAzureCredential + MI RBAC
- [ ] Retry backoff on 429/5xx; no retry on 4xx
- [ ] Idempotency for queued AI work
- [ ] Safe logging (correlation ID, no raw prompts)

## Hands-on minimum

- [ ] Lab 01 auth
- [ ] Lab 03 pgvector OR Lab 02 Cosmos
- [ ] Lab 04 messaging pipeline
- [ ] Lab 05 or 06 containers/telemetry

## Day before

- [ ] Read [exam-traps.md](./exam-traps.md)
- [ ] Walk [scenarios-walkthrough.md](../examples/scenarios-walkthrough.md) once
- [ ] Sleep — scenario questions require clear thinking

## Readiness bar

≥ **8/10** on checkpoint questions in each topic file **01–12**, plus comfortable explaining [service-chooser.md](./service-chooser.md) from memory.
