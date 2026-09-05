# Domain 1 practice — Plan and manage an Azure AI solution

**Exam:** AI-103 · Developing AI Apps and Agents on Azure  
**Weight:** 25–30% · Skills measured as of **April 16, 2026**  
**Coverage:** Study guide [`../study-guides/01-plan-manage.md`](../study-guides/01-plan-manage.md)

**How to use:** Cover the **Correct / Why** blocks and answer closed-book first. Unofficial study aids — not Microsoft exam dumps.

**Question types:** single-choice · multi-select

---

### Q1. Model choice for constrained edge tasks
A factory needs on-device text classification with tight latency and cost budgets. Complex multi-step reasoning is not required. Which model category is the best fit?

- A. Large language model with maximum context
- B. Small language model
- C. Multimodal video generation model
- D. Image-inpainting model

**Correct:** B  
**Why correct:** Small language models target lower latency/cost for constrained tasks.  
**Why distractors fail:** A is overkill for simple classification; C/D are generation/vision editing, not on-device text classification.  
**Mapped skill:** 1.1 Choose an appropriate model for each task  

---

### Q2. Grounding vs bigger model
Users say a Foundry chatbot “doesn’t know” internal HR policies stored in SharePoint. Leadership wants to “upgrade to a larger LLM.” What should you recommend first?

- A. Increase temperature so the model invents plausible policy answers
- B. Add grounding with retrieval/indexing over the HR documents
- C. Disable all safety filters to allow longer answers
- D. Switch exclusively to a video-generation model

**Correct:** B  
**Why correct:** Missing private knowledge is a grounding/retrieval problem, not primarily model size.  
**Why distractors fail:** A increases fabrications; C weakens RAI; D is irrelevant to HR text Q&A.  
**Mapped skill:** 1.1 Choose Foundry services for grounding / retrieval  

---

### Q3. Retrieval method (multi-select)
**Select 2.** An enterprise RAG index must handle both conceptual questions and exact invoice ID lookups. Which retrieval approaches should you include?

- A. Vector (semantic similarity) search
- B. Keyword/lexical search or filters for exact IDs
- C. Rely only on a larger context window with no index
- D. Disable indexing and ask the model to memorize all invoices at training time

**Correct:** A, B  
**Why correct:** Hybrid needs — vectors for meaning, keyword/filters for exact identifiers.  
**Why distractors fail:** C/D don’t scale or stay current for enterprise document corpora.  
**Mapped skill:** 1.1 Choose an appropriate method for retrieval and indexing  

---

### Q4. Agent integration services
You are designing an agent that must call internal APIs, remember multi-turn context, and answer from a knowledge base. Which combination best matches Foundry agent design?

- A. Tools + conversation memory + knowledge integration
- B. Image inpainting controls only
- C. Quota increase only, with no tools or memory
- D. Public web browsing with no auth and no knowledge store

**Correct:** A  
**Why correct:** Agents need tool access, memory, and knowledge integration for this scenario.  
**Why distractors fail:** B is vision editing; C doesn’t enable capabilities; D ignores enterprise auth/knowledge requirements.  
**Mapped skill:** 1.1 Memory, tool, and knowledge integration for agents  

---

### Q5. Deployment and CI/CD
A team wants to promote model and agent configurations from dev → test → prod automatically after evaluation gates pass. What is the best approach?

- A. Manually copy API keys into laptops before each release
- B. Integrate Foundry projects with CI/CD pipelines and environment-specific deployments
- C. Train a new foundation model from scratch on every commit
- D. Disable monitoring in production to speed releases

**Correct:** B  
**Why correct:** Foundry project integration with CI/CD and per-environment deployments is the operational pattern.  
**Why distractors fail:** A is insecure; C is unnecessary; D removes required ops controls.  
**Mapped skill:** 1.2 Integrate Foundry projects with CI/CD; configure deployments  

---

### Q6. Rate limits and cost
An app receives intermittent HTTP 429 responses from a model deployment and costs are rising. **Select 2** actions that directly address this class of problem.

- A. Implement backoff/retry, concurrency limits, and review quotas/rate limits
- B. Cache frequent responses and route cheap paths to smaller models
- C. Store model API keys in the git repository for faster retries
- D. Remove all content safety filters permanently

**Correct:** A, B  
**Why correct:** Quotas/rate limits and cost footprints are managed via throttling strategy, caching, and model tiering.  
**Why distractors fail:** C is a security anti-pattern; D is unrelated and harmful.  
**Mapped skill:** 1.3 Manage quotas, scaling, rate limits, and cost  

---

### Q7. Monitoring grounding quality
RAG answers increasingly cite outdated paragraphs after a content migration. Which monitoring focus is most relevant?

- A. GPU temperature of the developer laptop
- B. Data ingestion quality, search index health, and relevance/grounding metrics
- C. Only the marketing website bounce rate
- D. Disabling index refreshes to “stabilize” answers

**Correct:** B  
**Why correct:** Ingestion quality, index health, and grounding/relevance monitoring detect stale or broken retrieval.  
**Why distractors fail:** A/C are unrelated; D worsens staleness.  
**Mapped skill:** 1.3 Monitor ingestion, index health, grounding quality  

---

### Q8. Preferred security pattern
What is the preferred way for a production Azure app to authenticate to Foundry/AI resources without embedding long-lived secrets in code?

- A. Hardcode a shared API key in the source
- B. Managed identity with least-privilege role policies (keyless where possible)
- C. Email the key to the team distribution list
- D. Commit a `.env` file with production keys to the public repo

**Correct:** B  
**Why correct:** Managed identity, keyless credentials, and RBAC are the exam-aligned security baseline.  
**Why distractors fail:** A/C/D expose secrets and violate least privilege.  
**Mapped skill:** 1.3 Configure security: managed identity, keyless credentials, roles  

---

### Q9. Responsible AI controls
A regulated agent can refund orders via an API. Which RAI/governance set is most appropriate?

- A. No filters; full unrestricted tool access; no audit logs
- B. Safety filters/guardrails, tool-access controls, approval workflows, and trace/audit logging
- C. Only increase temperature for friendlier refunds
- D. Only store screenshots of the UI as the audit trail

**Correct:** B  
**Why correct:** High-risk tools need filters, constraints, approvals, and auditable traces/provenance.  
**Why distractors fail:** A is unsafe; C doesn’t govern tools; D is incomplete auditing.  
**Mapped skill:** 1.4 Responsible AI and agent governance  

---

### Q10. Private networking
Security requires that model traffic not traverse the public internet. Which control should you configure?

- A. Public endpoint with anonymous access
- B. Private networking / private endpoints for AI resources
- C. Disable TLS to reduce latency
- D. Share admin credentials across vendors

**Correct:** B  
**Why correct:** Private networking keeps service traffic on the private network path.  
**Why distractors fail:** A/C/D weaken security.  
**Mapped skill:** 1.3 Configure security including private networking  

---

## Answer key

| Q | Answer |
|---|--------|
| 1 | B |
| 2 | B |
| 3 | A, B |
| 4 | A |
| 5 | B |
| 6 | A, B |
| 7 | B |
| 8 | B |
| 9 | B |
| 10 | B |

**Readiness:** Aim ≥8/10 before moving on. Re-read [`../study-guides/01-plan-manage.md`](../study-guides/01-plan-manage.md) for misses.
