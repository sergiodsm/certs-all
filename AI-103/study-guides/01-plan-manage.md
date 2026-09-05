# Section 1 — Plan and manage an Azure AI solution (25–30%)

> **Exam:** AI-103 · Developing AI Apps and Agents on Azure  
> **Mapped skills:** 1.1–1.4 · [Official study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-103)  
> **Mock test:** [`../practice/domain-1-questions.md`](../practice/domain-1-questions.md)

## In one sentence

You select the right **Microsoft Foundry** models and services, design deployable infrastructure, then operate those systems with cost, security, monitoring, and responsible AI controls.

## Why it matters on the exam

This is ~¼–⅓ of the exam. Scenario questions often ask *which service/model/control* fits a requirement — not how to write every API call. Wrong answers usually mix up grounding vs generation, keys vs managed identity, or filters vs full RAI governance.

## Mental model

```text
  Business task
       │
       ▼
  Choose model + Foundry service
  (LLM / SLM / multimodal / Tools)
       │
       ▼
  Design infra + deployment + CI/CD
       │
       ▼
  Operate: quotas · cost · monitoring · security
       │
       ▼
  Govern: safety filters · evaluators · audit · agent constraints
```

## Topics checklist

### 1.1 Choose the appropriate Foundry services

- [ ] Match **LLMs** (complex reasoning, long context) vs **small language models** (latency/cost/edge) vs **multimodal** (image/audio/video + text) vs **Foundry Tools** (vision, speech, search, content understanding)
- [ ] Map needs to services: generation, **grounding**, **vector search**, agent workflows, multimodal processing
- [ ] Choose retrieval/indexing method: keyword, semantic, vector, hybrid
- [ ] Choose agent **memory**, **tools**, and **knowledge** integration patterns

### 1.2 Set up AI solutions in Foundry

- [ ] Design Azure infra for apps and agents (projects, networking, identity, storage, search)
- [ ] Choose deployment options (managed endpoints, capacity, regional considerations)
- [ ] Configure model and agent deployments (names, versions, parameters, endpoints)
- [ ] Wire Foundry projects into **CI/CD** (infra as code, promotion across envs)

### 1.3 Manage, monitor, and secure AI systems

- [ ] Manage **quotas**, scaling, **rate limits**, and cost footprints
- [ ] Monitor model performance, **drift**, safety events, **grounding quality**
- [ ] Monitor ingestion quality, **search index health**, relevance
- [ ] Secure with **managed identity**, private networking, **keyless** credentials, RBAC

### 1.4 Implement responsible AI

- [ ] Configure safety filters, guardrails, risk detection, content moderation
- [ ] Use evaluators, safety evaluations, explanation tooling
- [ ] Audit via trace logging, provenance metadata, approval workflows
- [ ] Govern agents: oversight modes, constraints, tool-access controls

---

## Key concepts

### Model and service selection

| Need | Prefer |
|------|--------|
| Open-ended reasoning, coding, long documents | Large language model |
| High throughput, low cost, constrained tasks | Small language model |
| Image/video/audio + text in one flow | Multimodal model |
| OCR, speech, translation, search, content understanding | Foundry Tools / Azure AI services |
| Answers from private data | Grounding + retrieval (RAG), not a bigger model alone |
| Agent that calls APIs and remembers turns | Agent + tools + memory + knowledge store |

⚠️ **Exam trap:** Picking a larger LLM when the real gap is **grounding** (missing or stale private knowledge).

### Retrieval and indexing methods

| Method | When to use |
|--------|-------------|
| Keyword / lexical | Exact terms, IDs, codes, rare proper nouns |
| Vector / semantic | Conceptual similarity, paraphrases |
| Hybrid | Best default for enterprise RAG (precision + recall) |
| Semantic ranking | Reorder candidates for relevance after retrieval |

### Deployment and CI/CD

- Treat **project → model deployment → agent deployment → app config** as separate promotion stages.
- Use environment-specific endpoints and deployment names; avoid hardcoding production keys.
- CI/CD should validate config, run safety/eval checks, then deploy infrastructure and app code.

### Ops: quotas, cost, monitoring

- **429 / rate limits** → backoff, concurrency caps, caching, quota increases, smaller models for cheap paths.
- Track **tokens**, latency, tool-call failures, grounding hit rate, and safety filter triggers.
- **Drift** = quality or behavior changes over time (data, prompts, model versions) — monitor evals continuously.
- Search health: index freshness, failed enrichments, zero-result rate, relevance metrics.

### Security baseline

| Control | Purpose |
|---------|---------|
| Managed identity + RBAC | No long-lived keys in code |
| Private networking / private endpoints | Keep traffic off public internet |
| Keyless credentials | Prefer token-based auth over API keys |
| Least-privilege roles | Separate deploy, invoke, admin duties |

⚠️ **Exam trap:** “Store the API key in app settings” as the *preferred* answer when managed identity is available.

### Responsible AI stack

```text
  Input → safety filters / moderation
            │
            ▼
  Model / agent (constraints, allowed tools)
            │
            ▼
  Output filters + evaluators (groundedness, safety, quality)
            │
            ▼
  Audit trail (traces, provenance) + human approval for high-risk actions
```

- **Oversight / approval flows** for autonomous agents that can change data or call sensitive tools.
- **Tool-access controls** limit which APIs an agent may invoke.
- Instrumentation is not optional on the exam: evaluators + traces show *why* an answer or action happened.

## Common mistakes

- Choosing multimodal when only text translation or entity extraction is needed (Foundry Tools may be enough).
- Confusing **content moderation** with full **agent governance** (tool constraints + approvals).
- Ignoring search index health when diagnosing bad RAG answers.
- Treating Preview features as the only correct answer when GA alternatives exist.

## Study focus order

1. Service/model chooser tables (1.1)  
2. Security + RAI controls (1.3–1.4)  
3. Monitoring signals for models, agents, and search (1.3)  
4. Deployment + CI/CD promotion patterns (1.2)

## Check your understanding

Before the mock test: for a chatbot that must answer from SharePoint PDFs, list model type, retrieval method, security controls, and which RAI features you would enable.
