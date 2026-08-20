# AI-200 Service Chooser

Quick decision guide for exam scenarios. When two options seem valid, pick the **simplest secure** option that matches the **official skill bullet**.

---

## Authentication

| Scenario | Choose |
|----------|--------|
| App runs on Azure calling Cosmos/Key Vault | **Managed identity** + RBAC |
| Local dev laptop | `DefaultAzureCredential` (`az login`) |
| Legacy lib requires connection string | Store in **Key Vault**; fetch at runtime |
| Quick hack with key in GitHub | ⚠️ Wrong answer on exam |

---

## Data stores for AI

| Scenario | Choose |
|----------|--------|
| Global NoSQL + change feed + vectors | **Cosmos DB for NoSQL** |
| SQL reports + pgvector + RAG filters | **Azure Database for PostgreSQL** |
| Hot FAQ cache + low-latency vector lookup | **Azure Managed Redis** |
| Authoritative full corpus + compliance audit | Postgres or Cosmos — **not Redis alone** |

---

## Messaging

| Scenario | Choose |
|----------|--------|
| "Process this embed job" queue | **Service Bus queue** |
| Fan-out: notify embed + audit + email workers | **Service Bus topic** |
| Blob was created → start pipeline | **Event Grid** → lightweight handler |
| Poison message after max retries | **Dead-letter queue** |
| Competing consumers, durable work | **Service Bus** — not Event Grid |

---

## Compute

| Scenario | Choose |
|----------|--------|
| Simple containerized REST API, slots | **App Service** |
| Scale to zero on queue depth | **Container Apps + KEDA** |
| Full Kubernetes, custom manifests | **AKS** |
| Validate upload + enqueue only | **Azure Functions** |
| 20-minute GPU batch embed | **Container Apps/AKS** — not Consumption Function |

---

## Config & secrets

| Scenario | Choose |
|----------|--------|
| API keys, passwords, certs | **Key Vault** (+ rotation) |
| Feature flags, model deployment name per env | **App Configuration** |
| Non-secret env-specific URL | App settings / App Configuration |

---

## Observability

| Scenario | Choose |
|----------|--------|
| Distributed trace across API → queue → worker | **OpenTelemetry** |
| p95 latency on model dependency | **KQL** on `dependencies` |
| Error spike by operation | **KQL** on `traces` / `requests` |

---

## RAG design

| Scenario | Choose |
|----------|--------|
| Exact SKU / error code queries | **Hybrid** keyword + vector |
| Multi-tenant isolation | **Metadata filter** on every query |
| Doc updated, search stale | **Change feed** / sync job / cache invalidation |
| Malicious text in retrieved doc | Instruction/data **separation** |

---

## Container build

| Scenario | Choose |
|----------|--------|
| CI build without local Docker | **ACR Tasks** |
| Immutable production deploy | Version tag `v1.2.3` — not `:latest` |
| Secret at runtime | Key Vault reference / MI — not Dockerfile `ENV`
