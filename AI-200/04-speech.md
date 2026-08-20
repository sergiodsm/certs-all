# Module 04 — Messaging & Eventing for Scalable AI Services

> **Exam domain:** Connect to and consume Azure services (**20–25%**)  
> **File:** `04-speech.md`

## In one sentence

Long-running AI work — embedding thousands of docs, reindexing, batch evaluation — belongs in **async pipelines** built with **Azure Service Bus**, **Azure Event Grid**, and **Azure Functions**, with idempotent consumers, dead-letter handling, and correlation IDs end to end.

## Why it exists

Synchronous APIs break under bulk embedding jobs and burst traffic. AI-200 tests **event-driven architecture**: when to queue vs publish events, how Functions triggers/bindings fit, and how to keep pipelines reliable when AI calls are slow or rate-limited.

## Service chooser

| Need | Prefer |
|------|--------|
| Ordered work queue, competing consumers, retry/DLQ | **Azure Service Bus** (queues, topics/subscriptions) |
| React to resource state changes, fan-out, lightweight events | **Azure Event Grid** (filters, custom events, retries) |
| Serverless handler for HTTP/timer/queue events | **Azure Functions** (triggers + bindings) |

```text
  Producer (API, Logic App, storage event)
              │
      ┌───────┴───────┐
      ▼               ▼
 Service Bus      Event Grid
 (work items)     (notifications)
      │               │
      └───────┬───────┘
              ▼
      Azure Functions / Container worker
              │
              ▼
   Embed · index · notify · evaluate
```

## Topics checklist

### Azure Service Bus
- [ ] **Queues** for point-to-point work; **topics/subscriptions** for fan-out
- [ ] **Dead-letter queue (DLQ)** for poison messages after max retries
- [ ] Message **sessions** when ordering per entity matters (know the tradeoff)

### Azure Event Grid
- [ ] **Event-driven workflows** with system/custom events
- [ ] **Filters** and **retry policies** for subscribers

### Azure Functions
- [ ] Build **serverless APIs** and workers with **triggers** (HTTP, timer, Service Bus, Event Grid)
- [ ] **Bindings** for inputs/outputs (storage, Cosmos DB, etc.)
- [ ] Configure and **deploy function apps** (settings, MI, scaling plan)

### Pipeline reliability
- [ ] **Correlation IDs** across producer → broker → consumer → AI call
- [ ] **Idempotent consumers** (dedup keys, upserts)
- [ ] **Backpressure** and concurrency limits to protect AI endpoints
- [ ] **Schema versioning** for event payloads
- [ ] Test failure paths: timeouts, malformed messages, consumer downtime

## Key concepts

### Idempotent consumer pattern

```text
  Message received (doc_id=v3)
       │
       ▼
  Check processing ledger / etag
       │
   Already done? ──yes──► Complete message (no-op)
       │
       no
       ▼
  Process + upsert + Complete
```

⚠️ **Exam trap:** Retrying AI embedding calls without dedup → duplicate vectors and double cost.

### Dead-letter workflow

After max delivery attempts, move message to **DLQ**, alert, inspect payload, fix root cause, **resubmit** or discard. Never infinite retry on poison messages.

### Functions in AI pipelines

Common triggers:

- **Service Bus** — process one document per message
- **Event Grid** — Blob created → start ingestion
- **HTTP** — lightweight API front door (often paired with queue for heavy work)

Configure app settings and **managed identity** for downstream Cosmos DB / storage access — not secrets in `local.settings.json` committed to git.

## Exam-style practice (10 questions + answers)

### Question 1
Why use messaging to compute embeddings for thousands of documents?

**Answer:**
**Decouples** ingestion from processing, smooths load, scales workers independently, and supports **retries/DLQ** on failure.

### Question 2
Consumer processes the same event twice. Safest pattern?

**Answer:**
**Idempotent consumer** — dedup key, upsert, processing ledger so replays don't duplicate side effects.

### Question 3
Message fails repeatedly after retries. What next?

**Answer:**
Send to **dead-letter queue**, alert, investigate payload/handler, fix and optionally resubmit.

### Question 4
Why version event payload schemas?

**Answer:**
Producers and consumers deploy independently; **versioning** prevents breaking changes from crashing consumers.

### Question 5
AI endpoint rate-limited during traffic spikes. How can messaging help?

**Answer:**
**Queue smoothing** + **limited consumer concurrency** / backpressure instead of unbounded synchronous calls.

### Question 6
Role of correlation IDs in AI pipelines?

**Answer:**
Link logs/traces across **API → queue → function → model call** for end-to-end troubleshooting.

### Question 7
Risk of blind retries on AI calls?

**Answer:**
**Repeated expensive work** and inconsistent state — combine retries with idempotency and checkpointing.

### Question 8
When can you skip strict message ordering?

**Answer:**
When processing is **idempotent** and **last-write-wins** is acceptable (e.g., re-embedding latest doc version).

### Question 9
Reindex after embedding model change — typical approach?

**Answer:**
Emit **reprocess/reindex events** (or batch job via queue), version new index, validate, then **cut over**.

### Question 10
How test an event-driven AI workflow?

**Answer:**
Simulate **consumer down**, timeouts, bad payloads, AI errors — verify retries, DLQ, and consistent final state.

## What's next

Module **05** packages and runs these backends on **Azure Container Registry**, **Container Apps**, and **AKS**.

## Deep dive (examples & labs)

- [Topic 08 — Service Bus & Event Grid](./topics_details/08-service-bus-event-grid.md)
- [Topic 09 — Azure Functions](./topics_details/09-azure-functions-serverless.md)
- [Lab 04 — Bus + Functions pipeline](./topics_details/labs/04-service-bus-functions-pipeline.md)
