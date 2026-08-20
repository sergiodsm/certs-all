# Python SDK Snippets (AI-200)

Copy-adapt patterns for labs and exam reasoning. Replace placeholders with your resources.

---

## Identity

```python
from azure.identity import DefaultAzureCredential
credential = DefaultAzureCredential()
```

---

## Cosmos DB

```python
from azure.cosmos import CosmosClient

client = CosmosClient("<account-url>", credential=DefaultAzureCredential())
container = client.get_database_client("aidb").get_container_client("chunks")

items = container.query_items(
    query="SELECT * FROM c WHERE c.tenantId = @t",
    parameters=[{"name": "@t", "value": "acme"}],
    partition_key="acme",
)
```

---

## Service Bus send

```python
from azure.servicebus import ServiceBusClient, ServiceBusMessage
import json

with ServiceBusClient("<namespace>.servicebus.windows.net", DefaultAzureCredential()) as client:
    with client.get_queue_sender("embed-jobs") as sender:
        sender.send_messages(ServiceBusMessage(json.dumps({"documentId": "d1"})))
```

---

## Key Vault

```python
from azure.keyvault.secrets import SecretClient

client = SecretClient("https://<vault>.vault.azure.net/", DefaultAzureCredential())
secret = client.get_secret("postgres-password").value
```

---

## App Configuration

```python
from azure.appconfiguration import AzureAppConfigurationClient

client = AzureAppConfigurationClient("https://<store>.azconfig.io", DefaultAzureCredential())
setting = client.get_configuration_setting(key="rag:top_k", label="production")
```

---

## PostgreSQL pgvector query

```python
# psycopg3
cur.execute(
    """
    SELECT content FROM document_chunks
    WHERE tenant_id = %s
    ORDER BY embedding <=> %s::vector LIMIT %s
    """,
    (tenant_id, query_vector, 5),
)
```

---

## OpenTelemetry span

```python
from opentelemetry import trace
tracer = trace.get_tracer("ai-api")

with tracer.start_as_current_span("llm.complete") as span:
    span.set_attribute("model.deployment", "gpt-4o")
    # call model
```

---

## Structured log (safe)

```python
import logging, json
logging.info(json.dumps({
    "correlation_id": cid,
    "step": "retrieve",
    "duration_ms": 42,
    "status": "ok",
}))
```

---

## Retry helper

```python
import time, random
from azure.core.exceptions import HttpResponseError

def with_retry(fn, retries=5):
    for i in range(retries):
        try:
            return fn()
        except HttpResponseError as e:
            if e.status_code not in (429, 500, 502, 503, 504):
                raise
            time.sleep(min(2**i + random.random(), 60))
    raise RuntimeError("retries exhausted")
```

---

## Idempotency ledger (pattern)

```python
def once(key: str, fn):
    if store.seen(key):
        return store.result(key)
    result = fn()
    store.save(key, result)
    return result
```

See topic files for full context on when to use each pattern.
