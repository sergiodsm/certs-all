# Topic 08 — Service Bus & Event Grid

> **Domain C (20–25%)** — official skill C1  
> **Module:** [`../04-speech.md`](../04-speech.md)  
> **Lab:** [labs/04-service-bus-functions-pipeline.md](./labs/04-service-bus-functions-pipeline.md)

---

## In one sentence

**Azure Service Bus** queues durable **work** with retries and **dead-letter queues**; **Azure Event Grid** routes **events** for reactive workflows — together they decouple AI ingestion from slow embedding and reindex jobs.

---

## Why it exists on the exam

Bulk embedding and reindexing cannot run synchronously in HTTP request handlers. Messaging skills are explicit in domain C.

---

## Service Bus vs Event Grid

| | Service Bus | Event Grid |
|---|-------------|------------|
| **Pattern** | Commands / jobs | Notifications |
| **Delivery** | Pull (competing consumers) | Push to subscribers |
| **Ordering** | Sessions optional | No global order |
| **DLQ** | Built-in dead-letter subqueue | Subscriber retry + dead-letter endpoint |
| **AI example** | "Process doc X" job | "Blob created" → trigger pipeline |

```text
  Blob upload
       │
       ▼
  Event Grid ──► Function (lightweight: validate, enqueue)
       │
       ▼
  Service Bus queue "embed-jobs"
       │
       ▼
  Container App workers (KEDA scaled)
```

---

## Service Bus: send & receive (Python)

```python
from azure.identity import DefaultAzureCredential
from azure.servicebus import ServiceBusClient, ServiceBusMessage
import json

credential = DefaultAzureCredential()
with ServiceBusClient(
    fully_qualified_namespace="mysb.servicebus.windows.net",
    credential=credential,
) as client:
    sender = client.get_queue_sender("embed-jobs")
    with sender:
        msg = ServiceBusMessage(json.dumps({
            "documentId": "doc-1001",
            "tenantId": "acme",
            "correlationId": "req-abc-123",
        }))
        sender.send_messages(msg)
```

```python
receiver = client.get_queue_receiver("embed-jobs", max_wait_time=30)
with receiver:
    for msg in receiver:
        try:
            process(json.loads(str(msg)))
            receiver.complete_message(msg)
        except PermanentError:
            receiver.dead_letter_message(msg, reason="BadPayload")
        except TransientError:
            receiver.abandon_message(msg)  # retry until max → DLQ
```

### Topics & subscriptions

- **Topic** — fan-out (e.g., `document-events`)
- **Subscriptions** — embed-worker, notify-worker, audit-logger each get copy

### Dead-letter queue

After max delivery count, message moves to **$DeadLetterQueue**.  
**Ops:** Monitor DLQ depth, alert, inspect, fix, **resubmit**.

---

## Event Grid

```python
# Publishing custom event (conceptual)
event = {
    "id": "evt-001",
    "eventType": "Document.Ingested",
    "subject": "documents/acme/doc-1001",
    "eventTime": "2026-08-19T20:00:00Z",
    "data": {"documentId": "doc-1001", "tenantId": "acme"},
    "dataVersion": "1.0",
}
```

- **Filters** on event type/subject route to specific handlers.
- **Retry** with exponential backoff on subscriber failures.

---

## Idempotent consumer (required)

```python
def handle_job(payload):
    key = f"{payload['tenantId']}:{payload['documentId']}:{payload['version']}"
    if state.is_done(key):
        return
    embed_and_store(payload)
    state.mark_done(key)
```

---

## ⚠️ Exam traps

1. **Event Grid as job queue** — no competing consumer semantics like Service Bus.
2. **Ignoring DLQ** — poison messages block or retry forever.
3. **No correlation ID** in message — can't trace to original upload.
4. **Non-idempotent embed** on retry — duplicate vectors.

---

## Checkpoint questions

**Q1.** 50k documents to embed overnight. Pattern?  
<details><summary>Answer</summary>Enqueue to Service Bus; scale workers with KEDA.</details>

**Q2.** Message fails 10 times with bad schema. Where?  
<details><summary>Answer</summary>Dead-letter queue — alert and inspect.</details>

**Q3.** Blob created should trigger lightweight router only. Service?  
<details><summary>Answer</summary>Event Grid → Function enqueues heavy work to Service Bus.</details>

---

## Skills checklist (official C1)

- [ ] Service Bus: queues, topics, subscriptions, DLQ
- [ ] Event Grid: filters, custom events, retries

---

## Next topic

[09 — Azure Functions](./09-azure-functions-serverless.md)
