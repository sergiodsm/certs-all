# Module 06 — Monitoring, Troubleshooting, Security & Responsible AI

> **Exam domain:** Secure, monitor, and troubleshoot Azure solutions (**20–25%**)  
> **File:** `06-evaluation-responsible-deployment.md`

## In one sentence

Production AI backends need **Key Vault** for secrets, **App Configuration** for settings, **OpenTelemetry** for distributed traces, **KQL** for log analysis — plus governance that treats models and retrieved text as **untrusted** and keeps PII out of telemetry.

## Why it exists

AI-200 bundles **security + observability** into ~25% of the exam. You must secure secrets, centralize config, trace multi-hop AI requests, query logs with KQL, and apply responsible-AI controls when prompts, retrieval, or models change.

## Operations stack

```text
  App (container/function)
       │
       ├──► Key Vault (secrets, rotation)
       ├──► App Configuration (feature flags, settings)
       └──► OpenTelemetry SDK ──► Azure Monitor / Log Analytics
                                      │
                                      ▼
                                 KQL queries
                                 (errors, latency, 429s)
```

## Topics checklist

### Implement secure Azure solutions
- [ ] **Azure Key Vault** — store/retrieve secrets, **rotation**
- [ ] **Azure App Configuration** — centralized settings, feature flags, refresh without redeploy

### Monitor and troubleshoot
- [ ] **OpenTelemetry SDKs** for distributed tracing (spans per pipeline step)
- [ ] **KQL** queries on logs/metrics — errors, latency percentiles, dependency failures
- [ ] Alerting on SLO breaches (error rate, p95 latency, DLQ depth)

### AI-specific operations
- [ ] Version **prompts**, **models/deployments**, and **index** artifacts
- [ ] **Offline evaluation** before prompt/retrieval/model changes
- [ ] **Online monitoring** — quality proxies, failure rates, safety filter triggers
- [ ] **Prompt injection** mitigation — retrieved content is data, not instructions
- [ ] **Content safety** — input/output filtering, escalation paths
- [ ] **PII** minimization in logs/traces; retention and RBAC on telemetry stores

## Key concepts

### Key Vault vs App Configuration

| Store | Use for |
|-------|---------|
| **Key Vault** | Secrets, keys, certificates — rotation, access policies/RBAC |
| **App Configuration** | Non-secret settings, labels per environment, feature toggles |

⚠️ **Exam trap:** Putting connection strings in App Configuration without Key Vault references when they are secrets.

### OpenTelemetry span model for AI requests

Typical spans: `http.request` → `retrieve` → `embed` → `llm.chat` → `persist`. Each records duration, status, and attributes (deployment ID, token count — not raw prompt text).

### Sample KQL patterns (conceptual)

```kusto
// Error spike on AI dependency
traces
| where timestamp > ago(1h)
| where cloud_RoleName == "ai-api"
| where success == false
| summarize count() by operation_Name, resultCode
```

```kusto
// p95 latency for model calls
dependencies
| where name contains "openai" or name contains "cognitive"
| summarize percentile(duration, 95) by bin(timestamp, 5m)
```

Know **KQL** basics: `where`, `summarize`, `join`, time ranges (`ago`), and filtering on `cloud_RoleName`, `operation_Name`, `success`.

### Responsible AI in backend systems

| Risk | Mitigation |
|------|------------|
| Prompt injection via RAG | System prompt isolation; delimit retrieved text; filter sources |
| Harmful outputs | Content safety APIs, output policies, human review thresholds |
| PII leakage | Redact at ingest and in logs; minimize retention |
| Quality regression | Offline eval + canary + version tags in traces |

## Exam-style practice (10 questions + answers)

### Question 1
Most useful telemetry for debugging one AI request in production?

**Answer:**
**Correlation/request ID**, timestamps, per-step status (retrieve, model, DB), error codes, **latency per step** — not full prompt text.

### Question 2
Why offline evaluation if you already monitor production?

**Answer:**
Production lacks **ground truth** and reflects biased traffic. Offline sets catch regressions **before** user impact.

### Question 3
Reduce risk of RAG following malicious instructions in retrieved docs?

**Answer:**
**Separate instructions from data**, delimit untrusted passages, filter sources, apply safety policies — never treat retrieval as system instructions.

### Question 4
Logs contain raw prompts with sensitive data. What to change?

**Answer:**
**Redact/minimize** logged content, strict access controls, defined **retention**, log IDs/hashes instead of raw text where possible.

### Question 5
Spike in model failures in monitoring. Safest production response?

**Answer:**
**Graceful degradation** — reduce concurrency, backoff, safer fallbacks, alert — prevent cascade to dependencies.

### Question 6
New prompt shipped; answers worsened. What should have been versioned?

**Answer:**
**Prompt template version**, model/deployment ID, retrieval/index version — correlated in traces to affected requests.

### Question 7
"Least privilege" for an AI backend identity?

**Answer:**
Grant only RBAC needed (e.g., Cosmos DB data plane read, specific Key Vault secret get) — no broad Owner/Contributor on subscription.

### Question 8
Measure retrieval change before full rollout?

**Answer:**
**Offline regression tests** on representative queries; compare relevance/grounding; canary if available.

### Question 9
When trigger human review?

**Answer:**
High-risk domains, policy-sensitive content, or **confidence/quality below threshold** when error cost is high.

### Question 10
Troubleshooting flow for containerized AI backend timeout?

**Answer:**
Follow **correlation ID** → ingress received? → container healthy? → dependency span (model/DB/queue) → network/auth errors on failing hop.

## Course complete

Review weak modules, run instructor **mock mode** via [`AI-200-INSTRUCTOR.md`](./AI-200-INSTRUCTOR.md), then schedule AI-200 when you consistently score ≥8/10 on each module's practice set.

## Deep dive (examples & labs)

- [Topic 10 — Key Vault & App Configuration](./topics_details/10-key-vault-app-configuration.md)
- [Topic 11 — OpenTelemetry & KQL](./topics_details/11-opentelemetry-kql-troubleshooting.md)
- [Topic 12 — Responsible AI in production](./topics_details/12-responsible-ai-production.md)
- [Lab 06 — Key Vault + KQL](./topics_details/labs/06-keyvault-telemetry-kql.md)
- [Exam traps](./topics_details/reference/exam-traps.md) · [Scenarios](./topics_details/examples/scenarios-walkthrough.md)
