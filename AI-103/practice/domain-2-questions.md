# Domain 2 practice — Implement generative AI and agentic solutions

**Exam:** AI-103 · Developing AI Apps and Agents on Azure  
**Weight:** 30–35% · Skills measured as of **April 16, 2026**  
**Coverage:** Study guide [`../study-guides/02-generative-agentic.md`](../study-guides/02-generative-agentic.md)

**How to use:** Cover the **Correct / Why** blocks and answer closed-book first. Unofficial study aids — not Microsoft exam dumps.

**Priority drill:** Heaviest exam domain — retake until ≥80%.

---

### Q1. RAG purpose
What is the primary reason to implement retrieval-augmented generation in a Foundry application?

- A. To permanently retrain the base model weights on every user query
- B. To ground responses in retrieved enterprise content at query time
- C. To replace all safety evaluations with random sampling
- D. To disable conversation memory for all users

**Correct:** B  
**Why correct:** RAG retrieves relevant content and conditions generation on it.  
**Why distractors fail:** A confuses RAG with training; C/D are unrelated/harmful.  
**Mapped skill:** 2.1 Implement RAG in an application  

---

### Q2. Connecting an app to Foundry
A Python backend must call deployed models in a Foundry project. What should you configure?

- A. Application connection to the Foundry project (endpoint/project config + auth) via SDKs/connectors
- B. Only a local CSV file with no project reference
- C. FTP upload of prompts to a public share
- D. Manual copy-paste of completions from the portal for each request

**Correct:** A  
**Why correct:** Apps integrate through Foundry SDKs/connectors and project configuration.  
**Why distractors fail:** B/C/D are not production integration patterns.  
**Mapped skill:** 2.1 Integrate via SDKs; connect to a Foundry project  

---

### Q3. Evaluation signals (multi-select)
**Select 2.** After shipping a support copilot, which evaluation dimensions catch “fluent but wrong” answers?

- A. Fabrication/groundedness detection
- B. Relevance to the user question
- C. Font size of the chat widget
- D. Number of emoji in the system prompt

**Correct:** A, B  
**Why correct:** Fabrications and relevance address accuracy beyond surface fluency.  
**Why distractors fail:** C/D are not model evaluation dimensions.  
**Mapped skill:** 2.1 Evaluate models/apps (fabrications, relevance, quality, safety)  

---

### Q4. Agent definition
You create a Foundry agent that books travel. Which elements belong in the agent design?

- A. Role/goals, conversation-tracking approach, and tool schemas
- B. Only a static HTML page with no tools
- C. Only increasing max tokens with no goals
- D. Only disabling tracing for privacy of tool errors

**Correct:** A  
**Why correct:** Agents need roles/goals, conversation tracking, and tool schemas.  
**Why distractors fail:** B/C omit agent capabilities; D removes needed observability.  
**Mapped skill:** 2.2 Define agent roles, goals, conversation tracking, tool schemas  

---

### Q5. Function calling
An agent must check order status in a CRM API. What is the correct integration pattern?

- A. Paste CRM passwords into the system prompt
- B. Define a tool/function schema and let the agent call the CRM API via function calling
- C. Ask the model to hallucinate order status codes
- D. Train a new vision model on screenshots of the CRM

**Correct:** B  
**Why correct:** Function calling with a tool schema connects NL intent to deterministic APIs.  
**Why distractors fail:** A is insecure; C invents data; D is the wrong modality.  
**Mapped skill:** 2.2 Agents with retrieval, function-calling, and tools  

---

### Q6. Multi-agent orchestration
A research agent gathers sources and a writer agent drafts a report. What do you need?

- A. Orchestrated multi-agent solution with clear handoffs
- B. A single temperature setting and no roles
- C. Deleting conversation memory every token
- D. Removing all evaluation after the first demo

**Correct:** A  
**Why correct:** Specialized agents require orchestration and coordination.  
**Why distractors fail:** B/C/D don’t implement multi-agent design.  
**Mapped skill:** 2.2 Implement orchestrated multi-agent solutions  

---

### Q7. Autonomous safeguards
An agent can delete production database rows. Which control is most appropriate?

- A. Fully autonomous deletes with no approval
- B. Semiautonomous workflow with safeguards and human/policy approval for destructive tools
- C. Hide the tool from logs but keep it callable
- D. Increase temperature so deletes are “creative”

**Correct:** B  
**Why correct:** Destructive actions need safeguards and approval flow controls.  
**Why distractors fail:** A/C/D increase risk without governance.  
**Mapped skill:** 2.2 Autonomous/semiautonomous workflows with safeguards  

---

### Q8. Prompt vs retrieval issue
Answers are off-topic even though retrieval returns the correct chunks. Temperature is already low. What should you tune first?

- A. Prompt engineering / instructions that force use of provided context and citations
- B. Buy a new GPU for the browser
- C. Disable the index entirely
- D. Convert all documents to audio only

**Correct:** A  
**Why correct:** When retrieval is good, generation behavior (prompts/parameters) is the next lever.  
**Why distractors fail:** B/C/D don’t address grounding instructions.  
**Mapped skill:** 2.3 Tune generation behavior (prompt engineering, parameters)  

---

### Q9. Observability (multi-select)
**Select 2.** Which signals help diagnose slow, expensive agent runs?

- A. Tracing across retrieve → model → tool spans
- B. Token analytics and latency breakdowns
- C. Only the color theme of the portal
- D. Disabling safety signals permanently

**Correct:** A, B  
**Why correct:** Tracing, tokens, and latency breakdowns are core observability for generative systems.  
**Why distractors fail:** C irrelevant; D removes safety telemetry.  
**Mapped skill:** 2.3 Observability: tracing, token analytics, safety, latency  

---

### Q10. Hybrid orchestration
A claims workflow needs strict business rules for payout limits and LLM help for narrative summaries. Best pattern?

- A. Hybrid LLM + rules engine orchestration
- B. Rules only with no language capability
- C. LLM only with no payout caps
- D. Multi-agent video generation for every claim

**Correct:** A  
**Why correct:** Hybrid orchestration keeps hard constraints in rules while using LLMs for language tasks.  
**Why distractors fail:** B lacks summarization flexibility; C risks compliance; D is unrelated.  
**Mapped skill:** 2.3 Orchestrate multiple models/flows or hybrid LLM and rules  

---

## Answer key

| Q | Answer |
|---|--------|
| 1 | B |
| 2 | A |
| 3 | A, B |
| 4 | A |
| 5 | B |
| 6 | A |
| 7 | B |
| 8 | A |
| 9 | A, B |
| 10 | A |

**Readiness:** Aim ≥8/10. This is the highest-weight domain — drill misses in [`../study-guides/02-generative-agentic.md`](../study-guides/02-generative-agentic.md).
