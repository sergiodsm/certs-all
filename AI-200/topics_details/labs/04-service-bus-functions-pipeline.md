# Lab 04 — Service Bus → Azure Functions Pipeline

**Topics:** [08-service-bus-event-grid.md](../08-service-bus-event-grid.md), [09-azure-functions-serverless.md](../09-azure-functions-serverless.md)  
**Time:** ~45 minutes

---

## Goal

Design and (optionally deploy) an async pipeline: API enqueues embed jobs; Function or worker processes with idempotency and DLQ awareness.

---

## Architecture

```text
  HTTP POST /ingest
        │
        ▼
  Validate + enqueue Service Bus message
        │
        ▼
  embed-jobs queue
        │
        ▼
  Function (Service Bus trigger) OR Container App worker
        │
        ▼
  Upsert embedding to Cosmos/Postgres
```

---

## Message schema (versioned)

```json
{
  "schemaVersion": "1.0",
  "documentId": "doc-1001",
  "tenantId": "acme",
  "contentHash": "sha256:abc...",
  "correlationId": "req-uuid"
}
```

---

## Sender snippet

```python
from azure.servicebus import ServiceBusClient, ServiceBusMessage
from azure.identity import DefaultAzureCredential
import json

with ServiceBusClient("mysb.servicebus.windows.net", DefaultAzureCredential()) as client:
    with client.get_queue_sender("embed-jobs") as sender:
        sender.send_messages(ServiceBusMessage(json.dumps(payload)))
```

---

## Idempotent handler pseudocode

```python
def handle(payload):
    key = f"{payload['tenantId']}:{payload['documentId']}:{payload['contentHash']}"
    if processed.exists(key):
        return
    embed_and_store(payload)
    processed.mark(key)
```

---

## DLQ drill (conceptual)

1. Send message with invalid JSON.
2. After max deliveries, confirm message in **dead-letter** subqueue.
3. Document alert + manual replay procedure.

---

## Verify understanding

- [ ] Service Bus vs Event Grid for "process this job"
- [ ] Why `complete_message` only after successful persist
- [ ] Correlation ID propagated to OpenTelemetry spans

---

## Exam tie-in

"Poison message keeps retrying" → **dead-letter queue** + alert, not infinite retry.
