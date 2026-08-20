# Topic 11 — OpenTelemetry, KQL & Troubleshooting

> **Domain D (20–25%)** — official skill D2  
> **Module:** [`../06-evaluation-responsible-deployment.md`](../06-evaluation-responsible-deployment.md)  
> **Lab:** [labs/06-keyvault-telemetry-kql.md](./labs/06-keyvault-telemetry-kql.md)

---

## In one sentence

Instrument AI backends with **OpenTelemetry** spans across retrieve/embed/LLM steps, export to **Azure Monitor**, and triage failures with **KQL** on logs, traces, and metrics.

---

## Why it exists on the exam

AZ-204 leaned on Application Insights SDK; AI-200 tests **vendor-neutral OpenTelemetry** plus hands-on **KQL** — a significant shift.

---

## OpenTelemetry in Python

```python
from opentelemetry import trace
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import BatchSpanProcessor
from opentelemetry.exporter.otlp.proto.http.trace_exporter import OTLPSpanExporter

provider = TracerProvider()
provider.add_span_processor(BatchSpanProcessor(OTLPSpanExporter()))
trace.set_tracer_provider(provider)
tracer = trace.get_tracer("ai-api")

def handle_question(correlation_id: str, question: str):
    with tracer.start_as_current_span("rag.request") as root:
        root.set_attribute("correlation_id", correlation_id)
        with tracer.start_as_current_span("retrieve"):
            chunks = retrieve(question)
            root.set_attribute("chunk_count", len(chunks))
        with tracer.start_as_current_span("llm.complete"):
            answer = call_llm(chunks, question)
        return answer
```

### Span attributes (safe)

| Log | Don't log |
|-----|-----------|
| `correlation_id`, `tenant_id`, `model_deployment`, `latency_ms`, `status` | Full prompt, PII, API keys |

Export via OTLP to **Azure Monitor Application Insights** (workspace-based).

---

## KQL essentials

### Error breakdown

```kusto
traces
| where timestamp > ago(24h)
| where cloud_RoleName == "ai-api"
| where severityLevel >= 3
| summarize count() by message, operation_Name
| order by count_ desc
```

### p95 dependency latency (model calls)

```kusto
dependencies
| where timestamp > ago(1h)
| where name contains "openai" or operation_Name == "llm.complete"
| summarize p95=percentile(duration, 95) by bin(timestamp, 5m)
```

### Join trace to request

```kusto
requests
| where timestamp > ago(1h)
| where success == false
| project timestamp, operation_Id, resultCode, duration
| join kind=inner (
    dependencies
    | project operation_Id, dep_name=name, dep_duration=duration, dep_success=success
) on operation_Id
```

### Service Bus DLQ signal (custom metric/log)

```kusto
traces
| where message contains "deadletter" or message contains "DLQ"
| summarize count() by bin(timestamp, 1h)
```

---

## Troubleshooting workflow

```text
  User report / alert
        │
        ▼
  Find correlation_id in App Insights
        │
        ▼
  requests → dependencies → traces (waterfall)
        │
        ├── slow llm.complete → model 429/5xx, backoff
        ├── retrieve timeout → Cosmos/Postgres/Redis
        ├── auth failure → MI/RBAC/Key Vault
        └── queue backlog → KEDA/worker health
```

---

## Alerting (exam scenarios)

| Alert on | Indicates |
|----------|-----------|
| Error rate > 5% | Deploy/regression |
| p95 latency > SLO | Model or DB degradation |
| DLQ depth > 0 | Poison messages |
| 429 spike on dependency | Throttling / need scale |

---

## ⚠️ Exam traps

1. **Logging prompts** to "debug" in production traces.
2. **Application Insights SDK only** when question asks OpenTelemetry.
3. **KQL on wrong table** — `traces` vs `dependencies` vs `requests`.
4. **No correlation ID** across Function → Service Bus → worker.

---

## Checkpoint questions

**Q1.** Find which step fails in RAG timeout. Tool?  
<details><summary>Answer</summary>Distributed trace (OpenTelemetry) — waterfall retrieve vs llm spans.</details>

**Q2.** p95 model latency doubled after deploy. KQL table?  
<details><summary>Answer</summary>`dependencies` filtered by LLM operation/name.</details>

**Q3.** Official exam monitoring standard emphasized over legacy SDK?  
<details><summary>Answer</summary>OpenTelemetry SDKs + KQL analysis.</details>

---

## Skills checklist (official D2)

- [ ] OpenTelemetry SDK distributed tracing
- [ ] KQL queries on logs and metrics

---

## Next topic

[12 — Responsible AI in production](./12-responsible-ai-production.md)
