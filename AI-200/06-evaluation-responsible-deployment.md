# Azure AI Cloud Developer Associate: Monitoring, Troubleshooting, Security & Responsible AI

The exam explicitly calls out that you must **secure, monitor, and troubleshoot Azure solutions**. For AI-enabled backends, that means more than uptime: you need telemetry for AI calls, safe handling of sensitive data, and quality/safety regression checks when you change prompts, retrieval, or models.

## What you should understand
- Operational excellence: logs/metrics/traces, alerts, and fast root-cause analysis.
- Security: least privilege, safe secret handling, and protecting data flows.
- Responsible AI patterns: reduce harmful outputs, mitigate prompt injection, and avoid sensitive data leakage.

## Topics checklist
- [ ] Instrument your AI backend (structured logs, request IDs, model call durations)
- [ ] Monitoring signals: errors/timeouts, latency percentiles, rate limiting events
- [ ] Alerting strategy (what to alert on to detect failures early)
- [ ] Troubleshooting workflow (trace from failing request to downstream dependency)
- [ ] Offline evaluation vs online monitoring (quality vs production telemetry)
- [ ] Regression testing for changes (prompts, retrieval/indexing, model upgrades)
- [ ] Prompt injection mitigation concepts (treat retrieved text as data)
- [ ] Content safety controls (input/output constraints, safe fallbacks)
- [ ] PII handling and auditability (minimize logging; retention choices)
- [ ] Security fundamentals (RBAC, managed identity, avoid over-privileged access)

## Exam-style practice (10 questions + answers)
### Question 1
What telemetry fields are most helpful for debugging an AI request in production?

**Answer (model):**
Include a correlation/request ID, timestamps, which steps were executed, downstream dependency status (AI endpoint, retrieval/vector search), error codes, and timing (latency) per step.

### Question 2
Why is offline evaluation important even if you monitor production?

**Answer (model):**
Because production metrics can be biased by traffic and don’t always provide ground truth. Offline evaluation lets you test known scenarios and catch regressions before impact.

### Question 3
How do you reduce the risk that your RAG system follows malicious instructions from retrieved content?

**Answer (model):**
Use instruction separation and treat retrieved passages as **data**. Add retrieval filtering and safety constraints so the model doesn’t treat untrusted content as authoritative instructions.

### Question 4
Your logs show prompt text and user queries containing sensitive data. What should you change?

**Answer (model):**
Stop logging sensitive raw content. Implement redaction/minimization and log only what’s necessary for troubleshooting, with strict access controls and clear retention policies.

### Question 5
What’s the safest production behavior when monitoring detects a spike in model failures?

**Answer (model):**
Degrade gracefully: reduce concurrency, use backoff, fall back to safer responses, and alert. Avoid cascading failures by limiting calls to downstream AI services.

### Question 6
You shipped a new prompt and some answers became worse. What should you have logged/versioned to investigate?

**Answer (model):**
Log/version the prompt (or prompt template) version, retrieval/index versions, and the model/deployment version. Then correlate those versions to affected requests via traces.

### Question 7
What does “least privilege” practically mean for an AI backend?

**Answer (model):**
Give the backend identity only the minimum permissions it needs (to call required services and access required data), and avoid using broad admin permissions.

### Question 8
How can you measure and reduce quality regressions after changing retrieval?

**Answer (model):**
Run retrieval regression tests and quality evaluation on a representative dataset, compare metrics (relevance/grounding/safety), and ship changes behind a controlled rollout if possible.

### Question 9
When should you trigger human review/escalation in an AI system?

**Answer (model):**
When outputs are high-risk, policy-sensitive, or confidence/quality is below thresholds—especially when the cost of being wrong is high.

### Question 10
What’s a good troubleshooting flow when a containerized AI backend times out?

**Answer (model):**
Start with the correlation ID/trace: confirm request arrival, check container health, then drill into downstream AI endpoint latency/timeouts and network/dependency errors to find the exact failing step.

