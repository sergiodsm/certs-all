# Module 01 — Azure SDK Integration & Python Backend Development

> **Exam domain:** Cross-cutting foundation for all AI-200 skills  
> **File:** `01-fundamentals.md`

## In one sentence

Your Python backend is the integration layer: it authenticates to Azure with **Entra ID / managed identity**, calls AI and data services through **SDKs or REST**, and handles failures, validation, and logging safely.

## Why it exists

AI-200 assumes you build **backend services**, not notebooks. Every domain (Cosmos DB, Service Bus, Container Apps, Key Vault) starts with the same questions: How does the app authenticate? How do you handle 429/5xx? What do you log — and what must you never log?

## Mental model

```text
  Client / Event / Function trigger
              │
              ▼
     Python API (FastAPI, Flask, etc.)
              │
    ┌─────────┼─────────┐
    ▼         ▼         ▼
 Entra ID   Azure SDK   Validation /
 (MI/token)  calls      error mapping
              │
              ▼
   Cosmos DB · PostgreSQL · Redis · Service Bus · Model endpoints
```

## Topics checklist

- [ ] Call Azure services from Python using official **Azure SDKs** (`azure-identity`, service-specific clients)
- [ ] Authenticate with **managed identity** and least-privilege RBAC (avoid long-lived keys in code)
- [ ] Map provider errors to consistent HTTP/API responses with **correlation IDs**
- [ ] Configure **timeouts**, **retries with exponential backoff + jitter**, and idempotency for duplicate requests
- [ ] Validate request/response schemas before and after model or data calls
- [ ] Externalize config per environment (dev/test/prod) — URLs, deployment names, feature flags
- [ ] Log structured telemetry **without** prompts, secrets, or raw PII
- [ ] Plan for **429 rate limits**, partial failures in multi-step workflows, and API/model versioning

## Key concepts

### Authentication: managed identity first

```python
from azure.identity import DefaultAzureCredential
from azure.cosmos import CosmosClient

credential = DefaultAzureCredential()
# SDK uses credential chain: MI in Azure, Azure CLI locally, etc.
client = CosmosClient(url, credential=credential)
```

⚠️ **Exam trap:** Storing connection strings or API keys in source control or container images. Prefer MI + RBAC scoped to the resource.

### Retries and rate limits

| Signal | Typical action |
|--------|----------------|
| HTTP 429 | Back off (respect `Retry-After` if present), reduce concurrency, cache |
| HTTP 5xx / timeout | Limited retries with jitter; fail gracefully to caller |
| Validation 4xx | Do not retry; fix input or return clear client error |

### Multi-step AI workflows

Split retrieve → embed → infer → persist into steps with **explicit error boundaries**. Each step gets its own timeout/retry policy and trace span so you can see which step failed in production.

### Safe logging

Log: correlation ID, latency, service name, status code, deployment/version IDs.  
Do **not** log: full prompts, user content, secrets, unredacted PII.

## Exam-style practice (10 questions + answers)

### Question 1
You're deploying a Python API that calls Azure AI and Cosmos DB. What's the preferred way to authenticate without storing secrets in code?

**Answer:**
Use **Entra ID** with **managed identity** (via `DefaultAzureCredential` or workload identity). Grant the identity only the RBAC roles needed on each resource.

### Question 2
Why treat "endpoint" and "deployment/model version" as separate concepts?

**Answer:**
The **endpoint** is the stable API surface your app calls. The **deployment** is the model/config behind it. You can swap deployments without changing client code if the contract stays stable.

### Question 3
Your backend gets intermittent timeouts calling a model. Best first improvement?

**Answer:**
Set explicit **timeouts**, add **retry with exponential backoff + jitter** for transient errors, and return a controlled fallback or error — not unbounded blocking.

### Question 4
Why validate model response shape before using it downstream?

**Answer:**
Outputs can be malformed or incomplete. Validation prevents crashes and lets you retry or fall back instead of propagating bad data.

### Question 5
Common logging mistake with AI requests — and how to avoid it?

**Answer:**
Logging raw prompts/outputs that may contain **PII or secrets**. Redact, minimize fields, enforce retention and access controls.

### Question 6
Duplicate client requests hit your API. How should backend AI calls behave?

**Answer:**
Design for **idempotency**: request IDs, deduplication, cached results for identical inputs — avoid repeated side effects and wasted tokens.

### Question 7
Most important reliability principle in a multi-step AI workflow?

**Answer:**
**Error boundaries per step** — independent timeouts/retries, consistent error responses, and tracing to identify the failing step.

### Question 8
Hard-coded service URLs and model parameters — what's better for lifecycle management?

**Answer:**
**External configuration** (environment variables, Azure App Configuration) per environment so the same code deploys everywhere.

### Question 9
How handle HTTP 429 from an AI endpoint?

**Answer:**
**Exponential backoff + jitter**, lower concurrency, caching where valid. Repeated 429 signals need capacity or throttling changes.

### Question 10
Good practice for mapping Azure SDK exceptions to your API?

**Answer:**
Central **error mapper**: transient → retryable response; client errors → 4xx; include correlation ID; never expose internal secrets.

## What's next

Module **02** covers the Azure data services where embeddings and application data live (Cosmos DB, PostgreSQL, Redis).

## Deep dive (examples & labs)

- [Topic 01 — Foundation SDK & Python](./topics_details/01-foundation-sdk-python.md)
- [Lab 01 — Local Azure auth](./topics_details/labs/01-local-azure-auth.md)
