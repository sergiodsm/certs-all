# Azure AI Cloud Developer Associate: Messaging & Eventing for Scalable AI Services

AI apps often need asynchronous workflows: ingest documents, compute embeddings, reindex, run evaluations, or process user requests in the background. Azure messaging/eventing helps you scale and decouple these workloads while keeping reliability (retries, dead-lettering) and traceability (correlation IDs).

## What you should understand
- When synchronous request/response is not enough (latency, throughput, long-running work).
- How to design event-driven AI pipelines safely (idempotency, schema versioning, backpressure).
- How to connect messaging with monitoring for troubleshooting.

## Topics checklist
- [ ] Choose messaging/eventing for async workloads (decouple producers/consumers)
- [ ] Design event schemas (versioning, validation) to avoid breaking consumers
- [ ] Correlation IDs end-to-end for traceability
- [ ] Idempotent consumers (deduplication/upserts)
- [ ] Retry strategy + dead-letter handling for poison messages
- [ ] Backpressure/rate limiting concepts to protect downstream services
- [ ] Ordering considerations (when ordering matters vs when it doesn't)
- [ ] Safe retries for steps that call AI endpoints (avoid repeated side effects)
- [ ] Distinguish batch processing vs streaming event processing
- [ ] Test failure paths (timeouts, partial processing, consumer downtime)

## Exam-style practice (10 questions + answers)
### Question 1
You need to compute embeddings for thousands of documents. Why is messaging/eventing useful?

**Answer (model):**
It decouples ingestion from processing and lets you scale embedding computation asynchronously while smoothing load and handling failures with retries/dead-lettering.

### Question 2
Your consumer occasionally processes the same event twice. What’s the safest pattern?

**Answer (model):**
Make the consumer **idempotent**: use dedup keys, upsert semantics, and ensure repeated processing doesn’t duplicate outputs or double-apply side effects.

### Question 3
What should you do with a message that keeps failing after retries?

**Answer (model):**
Move it to a **dead-letter** path and alert/inspect it. That prevents infinite retry loops and keeps the pipeline healthy.

### Question 4
Why should event payload schemas be versioned?

**Answer (model):**
Because producers and consumers evolve at different times. Versioning prevents breaking changes from causing widespread consumer failures.

### Question 5
Your AI endpoint calls are being rate-limited by spikes. How can messaging help?

**Answer (model):**
Queue/workload smoothing reduces spikes, and consumer rate limiting/backpressure can be used to keep concurrency within safe bounds.

### Question 6
How do correlation IDs help in AI pipelines?

**Answer (model):**
They let you link logs/traces across producer, message broker, and consumer so you can trace a request end-to-end during troubleshooting.

### Question 7
What’s the key risk of retrying AI calls without careful design?

**Answer (model):**
You may repeat expensive work or trigger inconsistent results. Use idempotency/caching and handle partial failures so retries don’t create incorrect outputs.

### Question 8
When might you avoid strict ordering guarantees?

**Answer (model):**
When updates are idempotent and you only care about final state (e.g., “latest document version” wins). Avoiding strict ordering improves throughput.

### Question 9
You need to reindex after changing embeddings. Which pipeline approach is usually best?

**Answer (model):**
Trigger a reprocessing job via messaging/eventing (e.g., emit “reindex” events), keep it versioned, and validate before switching traffic.

### Question 10
How do you test an event-driven AI workflow for reliability?

**Answer (model):**
Simulate failures: consumer downtime, timeouts, malformed messages, downstream AI errors. Verify retries, dead-letter behavior, and that outputs remain consistent.

