# Topic 09 — Azure Functions (Serverless AI Workers)

> **Domain C (20–25%)** — official skill C2  
> **Module:** [`../04-speech.md`](../04-speech.md)  
> **Lab:** [labs/04-service-bus-functions-pipeline.md](./labs/04-service-bus-functions-pipeline.md)

---

## In one sentence

**Azure Functions** run event-driven code with **triggers** (HTTP, Service Bus, Event Grid, timer) and **bindings** (Cosmos DB, Storage) — ideal for lightweight steps in AI pipelines; heavy embedding may run on Container Apps instead.

---

## Why it exists on the exam

Domain C2 explicitly covers serverless APIs, triggers/bindings, and function app deployment/configuration.

---

## Common triggers for AI pipelines

| Trigger | AI use case |
|---------|-------------|
| **HTTP** | Thin API gateway; enqueue long work |
| **Service Bus** | Process one document per message |
| **Event Grid** | React to blob/upload events |
| **Timer** | Nightly eval jobs, cache warm-up |

---

## Example: Service Bus trigger (Python v2 model)

```python
import azure.functions as func
import json
import logging

app = func.FunctionApp()

@app.service_bus_queue_trigger(
    arg_name="msg",
    queue_name="embed-jobs",
    connection="ServiceBusConnection",  # use MI in production
)
def embed_worker(msg: func.ServiceBusMessage):
    payload = json.loads(msg.get_body().decode("utf-8"))
    correlation_id = payload.get("correlationId", "unknown")
    logging.info("Processing doc %s", payload["documentId"], extra={"correlation_id": correlation_id})
    # embed_and_upsert(payload)
```

### HTTP trigger API

```python
@app.route(route="ask", methods=["POST"], auth_level=func.AuthLevel.FUNCTION)
def ask(req: func.HttpRequest) -> func.HttpResponse:
    body = req.get_json()
    # retrieve + call model OR enqueue to Service Bus for async
    return func.HttpResponse(json.dumps({"status": "queued"}), mimetype="application/json")
```

### Output binding (Storage blob)

```python
@app.service_bus_queue_trigger(arg_name="msg", queue_name="embed-jobs", connection="ServiceBusConnection")
@app.blob_output(arg_name="outputblob", path="embeddings/{documentId}.json", connection="AzureWebJobsStorage")
def process_and_store(msg: func.ServiceBusMessage, outputblob: func.Out[str]):
    outputblob.set(json.dumps({"vector": [0.1, 0.2]}))
```

---

## Configuration & deploy

```bash
# Create function app (Linux, Python)
az functionapp create --resource-group rg-ai --consumption-plan-location eastus \
  --runtime python --runtime-version 3.12 --functions-version 4 \
  --name ai-func-prod --storage-account staifunc --os-type Linux

# Deploy (from project folder)
func azure functionapp publish ai-func-prod
```

### Settings (never commit secrets)

```bash
az functionapp config appsettings set --name ai-func-prod --resource-group rg-ai \
  --settings COSMOS_URL=https://....documents.azure.com:443/
```

Enable **managed identity** and replace connection strings with RBAC + `DefaultAzureCredential` in code where possible.

---

## Functions vs Container Apps for AI

| Functions | Container Apps |
|-----------|----------------|
| Short jobs (< few min on Consumption) | Long embed batches, custom deps |
| Built-in bindings | Any container, KEDA |
| Per-execution billing | Always-on option |

**Exam pattern:** Function validates + enqueues; Container App worker embeds.

---

## ⚠️ Exam traps

1. **Long GPU embed in Consumption Function** — timeout; use queue + worker tier.
2. **Connection strings in `local.settings.json` committed to git**.
3. **No dead-letter handling** on Service Bus trigger failures.
4. **Confusing trigger vs binding** — trigger starts function; binding is I/O helper.

---

## Checkpoint questions

**Q1.** Blob upload → validate metadata → queue embed job. Components?  
<details><summary>Answer</summary>Event Grid trigger Function → Service Bus output/enqueue.</details>

**Q2.** Configure Function to read from `embed-jobs` queue.  
<details><summary>Answer</summary>Service Bus **queue trigger**.</details>

**Q3.** 15-minute embedding job on Consumption plan. Problem?  
<details><summary>Answer</summary>Timeout limits — move heavy work to Container Apps/AKS or Premium plan.</details>

---

## Skills checklist (official C2)

- [ ] Serverless APIs; triggers and bindings
- [ ] Configure and deploy function apps

---

## Next topic

[10 — Key Vault & App Configuration](./10-key-vault-app-configuration.md)
