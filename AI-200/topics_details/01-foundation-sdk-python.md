# Topic 01 — Foundation: Python SDK, Entra ID & Backend Reliability

> **Cross-cutting** — required for every AI-200 domain  
> **Module:** [`../01-fundamentals.md`](../01-fundamentals.md)  
> **Lab:** [labs/01-local-azure-auth.md](./labs/01-local-azure-auth.md)

---

## In one sentence

Every Azure AI backend authenticates with **Microsoft Entra ID** (prefer **managed identity**), calls services through **Python SDKs**, and survives production with timeouts, retries, idempotency, and safe logging.

---

## Why it exists on the exam

Case studies assume you write integration code — not click-through portals. Wrong auth or retry logic breaks pipelines that span Cosmos DB, Service Bus, Container Apps, and Key Vault.

---

## How it works in Azure

### Authentication chain

```text
  Local dev                    In Azure (Container App / Function / AKS)
  ─────────                    ─────────────────────────────────────────
  Azure CLI login      ─┐      System-assigned or user-assigned MI
  VS Code credential    ├──►   DefaultAzureCredential()
  Environment vars      ─┘           │
                                     ▼
                              Entra ID token for resource scope
                                     │
                                     ▼
                              Cosmos DB · Storage · Key Vault · etc.
```

### Core packages

```bash
pip install azure-identity azure-cosmos azure-servicebus azure-keyvault-secrets opentelemetry-api opentelemetry-sdk
```

### Connect with managed identity

```python
from azure.identity import DefaultAzureCredential
from azure.cosmos import CosmosClient

credential = DefaultAzureCredential()
client = CosmosClient(
    url="https://<account>.documents.azure.com:443/",
    credential=credential,
)
database = client.get_database_client("ai-db")
container = database.get_container_client("documents")
```

**Local dev:** `az login` so `DefaultAzureCredential` picks up Azure CLI credentials.  
**In Azure:** assign MI to the hosting resource and grant RBAC (e.g., `Cosmos DB Built-in Data Contributor`).

### Retry pattern (transient errors)

```python
import time
import random
from azure.core.exceptions import HttpResponseError

def call_with_backoff(fn, max_retries=5):
    for attempt in range(max_retries):
        try:
            return fn()
        except HttpResponseError as ex:
            if ex.status_code not in (429, 500, 502, 503, 504):
                raise
            delay = min(2 ** attempt + random.uniform(0, 1), 60)
            time.sleep(delay)
    raise RuntimeError("Max retries exceeded")
```

### Idempotency for AI calls

```python
# Pseudocode: ledger keyed by (request_id) or (doc_id, content_hash)
def process_document(doc_id: str, content_hash: str, embed_fn):
    if ledger.exists(doc_id, content_hash):
        return ledger.get_result(doc_id, content_hash)
    embedding = embed_fn(doc_id)
    ledger.save(doc_id, content_hash, embedding)
    return embedding
```

### Safe structured logging

```python
import logging
import json

logger = logging.getLogger("ai-api")

def log_request(correlation_id: str, step: str, duration_ms: int, status: str):
    logger.info(json.dumps({
        "correlation_id": correlation_id,
        "step": step,
        "duration_ms": duration_ms,
        "status": status,
        # Do NOT log: prompt, user text, secrets
    }))
```

---

## When to use / avoid

| Pattern | Use when | Avoid when |
|---------|----------|------------|
| Managed identity | App runs on Azure with RBAC | Quick throwaway script with no Azure host |
| Connection string in Key Vault | Legacy SDK requires it | Hard-coding in app settings committed to git |
| Retry with backoff | 429/5xx transient | 400 validation errors (won't fix on retry) |
| Idempotency keys | Queues, duplicate HTTP posts | Truly unique one-off admin actions |

---

## ⚠️ Exam traps

1. **Keys in container images or repo** — always MI + Key Vault or platform secret injection.
2. **Retrying non-idempotent writes** without dedup — duplicates embeddings or double-charges.
3. **Logging full prompts** for "debugging" — PII/governance violation.
4. **Infinite retry on 429** — need backoff + concurrency limits.
5. **Same code, different env** — externalize config; don't rebuild images per environment.

---

## Checkpoint questions

**Q1.** Python API on Container Apps calls Cosmos DB. Best auth?  
<details><summary>Answer</summary>User-assigned or system MI + `DefaultAzureCredential`; RBAC on Cosmos DB data plane.</details>

**Q2.** Client sends duplicate POST with same `Idempotency-Key`. Expected behavior?  
<details><summary>Answer</summary>Return cached result; do not re-run embedding/inference.</details>

**Q3.** SDK returns HTTP 400 "invalid partition key". Retry?  
<details><summary>Answer</summary>No — fix the request; 4xx is not transient.</details>

---

## Skills checklist (official cross-cut)

- [ ] Azure SDKs from Python backend
- [ ] Entra ID / managed identity, least privilege
- [ ] Timeouts, exponential backoff, idempotency
- [ ] Schema validation, error mapping, correlation IDs
- [ ] Environment-specific configuration
- [ ] Safe logging (no PII/secrets)

---

## Next topic

[02 — Cosmos DB for NoSQL AI](./02-cosmos-db-nosql-ai.md)
