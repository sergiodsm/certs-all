# Azure AI Cloud Developer Associate: Evaluation, Responsible AI, & Deployment

## Topics checklist
### Evaluation & monitoring (AI quality)
- [ ] Creating evaluation datasets/test sets (representative queries and expected outcomes)
- [ ] Offline evaluation vs online monitoring concepts
- [ ] Metrics you should be able to reason about (relevance, grounding/faithfulness, safety)
- [ ] Regression testing strategy (prompt changes, retrieval changes, model upgrades)
- [ ] Interpreting evaluation results and improving the system iteratively

### Responsible AI (safety & governance)
- [ ] Content filtering and why it’s needed (blocking vs allowing with warnings)
- [ ] Threat thinking: common failure modes (prompt injection, data leakage, toxic outputs)
- [ ] Applying safety controls in an app pipeline (input validation, retrieval filtering, output constraints, and safe fallbacks)
- [ ] Mitigation patterns (input filtering, retrieval filtering, output constraints)
- [ ] PII handling concepts (identify, avoid storing unnecessary sensitive data)
- [ ] Data governance basics (retention, logging, and auditability considerations)
- [ ] Human-in-the-loop / escalation concepts for high-risk outputs

### Deployment patterns
- [ ] Deploying an AI solution endpoint (high-level flow)
- [ ] Versioning prompts/indexes/models (how changes affect behavior)
- [ ] Scaling considerations (throughput, batching, caching where appropriate)
- [ ] Observability basics (logs, traces, metrics relevant to AI apps)
- [ ] Cost management strategies (reduce tokens/calls; optimize retrieval)

## Exam-style practice (with answers)
### Question 1
Before you change prompts or retrieval logic in production, why do you run regression evaluation?

**Answer (model):**
To catch **behavior drift** and quality regressions caused by changes. Regression testing helps ensure improvements don’t break other scenarios and provides confidence that the updated system still meets the expected metrics.

### Question 2
Your RAG system treats retrieved text as “context.” A malicious document tries to instruct the model to ignore rules. What’s the best mitigation approach?

**Answer (model):**
Treat retrieved content as **data, not instructions**: isolate system/developer instructions from retrieved passages, apply **prompt/instruction separation**, and add **input/output safety controls** (including content filtering and retrieval filtering for malicious or irrelevant content).

### Question 3
You changed the prompt and want to know which version produced an incorrect answer. What should you log/version?

**Answer (model):**
Log and version at least: the **prompt version**, the **retrieval/index version** (or index update timestamp), and the **model/deployment version**. Then correlate those version IDs with request/response traces so you can reproduce and debug the failure.

