# Module 05 — Containerized Solutions on Azure (Deploy & Scale)

> **Exam domain:** Develop containerized solutions on Azure (**20–25%**)  
> **File:** `05-generative-rag.md`

## In one sentence

Ship your Python AI backend as **containers**: build and store images in **Azure Container Registry (ACR)**, run on **Azure App Service**, **Azure Container Apps**, or **AKS**, scale with **KEDA**, and troubleshoot via logs, events, and connectivity checks — with secrets outside the image.

## Why it exists

AI-200 replaces generic AZ-204 container trivia with **operational scenarios**: ACR tasks, revision management in Container Apps, KEDA event-driven scaling, AKS manifests, and inspecting production failures.

## Hosting options (exam map)

| Capability | Azure services |
|------------|----------------|
| Build/store/version images | **Azure Container Registry**, **ACR Tasks** |
| Simple container hosting + env/secrets | **Azure App Service** (containers) |
| Serverless containers, revisions, KEDA | **Azure Container Apps** |
| Full Kubernetes control | **Azure Kubernetes Service (AKS)** + manifests |

```text
  Code + Dockerfile
        │
        ▼
   ACR (build/push/tag)
        │
   ┌────┴────┬────────────┐
   ▼         ▼            ▼
App Service  Container Apps   AKS
             (+ KEDA scale)
```

## Topics checklist

### Container application hosting
- [ ] Build, store, version images in **ACR**
- [ ] Build/run with **ACR Tasks**
- [ ] Deploy to **App Service** with env vars and secrets (Key Vault references)

### Container-orchestrated solutions
- [ ] Deploy to **Container Apps** — environments, **revisions**, traffic splitting
- [ ] **KEDA** event-driven autoscaling (e.g., queue depth → replica count)
- [ ] Deploy/manage on **AKS** using **manifest files**
- [ ] Monitor/troubleshoot: container logs, events, **connectivity** (DNS, egress, private endpoints)

### Operations
- [ ] **Readiness/liveness** probes — don't route to starting instances
- [ ] **Graceful shutdown** for in-flight AI requests
- [ ] **Managed identity** for Azure resource access from containers
- [ ] Immutable deployments — roll forward/back via image tags/revisions
- [ ] Cost control: right-size CPU/memory, autoscale bounds, concurrency limits

## Key concepts

### Secrets and config

| Bad | Good |
|-----|------|
| API keys baked into image | **Managed identity** + Key Vault / App Configuration |
| Different images per env | Same image, different **runtime env/config** |

### Container Apps + KEDA

Scale replicas based on **custom metrics** — e.g., Service Bus queue length or HTTP concurrency — so embedding workers grow under load and shrink when idle.

⚠️ **Exam trap:** Scaling on CPU alone while work is **queue-backed** — KEDA on queue depth is the exam-aligned pattern.

### AKS troubleshooting flow

1. `kubectl get pods` / events — CrashLoopBackOff? Image pull errors?
2. Pod logs — application exceptions, auth failures to Cosmos DB
3. Service/network — can pod reach AI endpoint? DNS? NSG/firewall?
4. End-to-end trace — correlation ID from ingress to model call

### Health probes

- **Liveness** — restart if deadlocked
- **Readiness** — remove from load balancer until dependencies (token provider, config) are ready

## Exam-style practice (10 questions + answers)

### Question 1
Why avoid hard-coding secrets in container images?

**Answer:**
Images are copied and long-lived; secrets in layers **expand breach blast radius**. Use MI, Key Vault, or platform secret injection.

### Question 2
Purpose of a **readiness** probe?

**Answer:**
Signals when the instance can **accept traffic** — prevents routing to containers still starting or missing config.

### Question 3
Model endpoint unavailable at startup. Safe approach?

**Answer:**
Startup checks + **readiness** failure (not ready), retries/backoff; optionally degrade features — don't serve silently broken responses.

### Question 4
Roll out updated model integration without breaking clients?

**Answer:**
**Immutable revision/image** deploy, stable external API contract, validate new revision (traffic split/canary) before full cutover.

### Question 5
Why **graceful shutdown** for AI backends?

**Answer:**
Completes or cleanly cancels **in-flight requests** instead of dropping them mid-inference.

### Question 6
Rate limits during traffic spikes — container-level mitigations?

**Answer:**
Limit **per-instance concurrency**, queue heavy work, autoscale on **meaningful signals** (KEDA/queue depth), not unbounded fan-out.

### Question 7
Enable managed identity auth from a containerized workload?

**Answer:**
Assign **user-assigned or system MI** to the hosting resource (Container App, AKS pod identity/workload ID) and grant RBAC on target services.

### Question 8
Debug production timeouts in containers?

**Answer:**
**Structured logs + distributed traces**, correlation IDs, dependency latency breakdown (AI, DB, queue).

### Question 9
Why environment variables for dev/test/prod config?

**Answer:**
**One image, many environments** — change runtime settings without rebuilding.

### Question 10
Control costs for containerized AI services?

**Answer:**
Autoscale bounds, concurrency caps, caching, avoid retry storms, scale-to-zero where latency SLO allows (Container Apps + KEDA).

## What's next

Module **06** covers **Key Vault**, **App Configuration**, **OpenTelemetry**, **KQL**, and responsible AI operations.

## Deep dive (examples & labs)

- [Topic 06 — ACR & App Service](./topics_details/06-acr-app-service-containers.md)
- [Topic 07 — Container Apps, KEDA & AKS](./topics_details/07-container-apps-keda-aks.md)
- [Lab 05 — Container Apps deploy](./topics_details/labs/05-container-apps-deploy.md)
