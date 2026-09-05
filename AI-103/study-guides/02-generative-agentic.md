# Section 2 — Implement generative AI and agentic solutions (30–35%)

> **Exam:** AI-103 · Developing AI Apps and Agents on Azure  
> **Mapped skills:** 2.1–2.3 · [Official study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-103)  
> **Mock test:** [`../practice/domain-2-questions.md`](../practice/domain-2-questions.md)

## In one sentence

You build Foundry apps and agents that call models, retrieve grounded knowledge, use tools, then evaluate, observe, and optimize those systems in production.

## Why it matters on the exam

Heaviest domain (~30–35%). Expect scenarios on **RAG**, **function calling**, **multi-agent orchestration**, prompt/parameter tuning, and what to measure when quality or safety fails.

## Mental model

```text
  App / Agent
      │
      ├── Models (LLM, SLM, code, multimodal)
      ├── Retrieval (RAG / knowledge)
      ├── Tools (APIs, search, functions)
      ├── Memory (conversation state)
      └── Orchestration (flows, multi-agent)
              │
              ▼
      Evaluate + observe + tune
```

## Topics checklist

### 2.1 Build generative applications

- [ ] Deploy/consume LLMs, small models, code models, multimodal models
- [ ] Implement **RAG** end to end
- [ ] Design workflows, tool-augmented flows, multistep reasoning
- [ ] Evaluate fabrications, relevance, quality, safety
- [ ] Integrate via Foundry **SDKs** and connectors
- [ ] Connect an application to a Foundry **project**

### 2.2 Build agents

- [ ] Define roles, goals, conversation tracking, **tool schemas**
- [ ] Combine retrieval + function calling + conversation memory
- [ ] Integrate tools: APIs, knowledge stores, search, content understanding, custom functions
- [ ] Orchestrate **multi-agent** solutions
- [ ] Autonomous / semiautonomous flows with safeguards and approvals
- [ ] Monitor agents, evaluate behavior, error analysis

### 2.3 Optimize and operationalize

- [ ] Prompt engineering and model parameter tuning
- [ ] Reflection, chain-of-thought evaluations, self-critique loops
- [ ] Observability: tracing, token analytics, safety signals, latency breakdowns
- [ ] Orchestrate multiple models, flows, or hybrid LLM + rules engines

---

## Key concepts

### Generative app vs agent

| Pattern | Behavior |
|---------|----------|
| Generative app | Prompt in → completion out (optionally with RAG) |
| Tool-augmented flow | Model decides when to call functions / APIs |
| Agent | Persistent goals, memory, tools, multi-step planning |
| Multi-agent | Specialized agents coordinated by an orchestrator |

### RAG essentials

```text
  Query → retrieve (vector/hybrid) → ground prompt with chunks → generate → cite/evaluate
```

- Chunking, embeddings, index freshness, and citation quality matter as much as the LLM.
- Evaluate **groundedness** (supported by retrieved evidence) separately from fluency.
- Fabrications / hallucinations rise when retrieval fails or the prompt allows unconstrained invention.

### Agents: roles, tools, memory

- **Role + goal** = system instructions and success criteria.
- **Tool schema** = name, description, parameters (JSON schema) so the model can call correctly.
- **Conversation memory** = short-term turn history; long-term may use knowledge/store summaries.
- **Function calling** bridges natural language to deterministic APIs.

⚠️ **Exam trap:** Building a free-form agent for a task that only needs a single RAG completion or a rules engine.

### Multi-agent and autonomy

- Use specialized agents (research, writer, critic, executor) with a clear handoff protocol.
- **Semiautonomous** = agent proposes; human or policy approves high-risk tools.
- Safeguards: allowlists of tools, spend/rate caps, approval workflows, kill switches.

### Evaluation dimensions

| Signal | Question it answers |
|--------|---------------------|
| Relevance | Does the answer address the user ask? |
| Groundedness / fabrications | Is it supported by sources? |
| Quality | Coherence, completeness, format |
| Safety | Harm, jailbreaks, policy violations |
| Agent success | Did tools run correctly? Goal met? |

### Optimization knobs

| Control | Effect |
|---------|--------|
| System / few-shot prompts | Style, constraints, task framing |
| Temperature / top_p | Creativity vs determinism |
| Max tokens | Length / cost / truncation |
| Reflection / self-critique | Second pass to catch errors |
| Hybrid LLM + rules | Hard constraints for compliance |

### Observability

- **Tracing** spans: retrieve → prompt build → model → tool calls → response.
- **Token analytics** for cost and prompt bloat.
- **Latency breakdown** isolates slow retrieval vs model vs tools.
- **Safety signals** count filter hits and policy violations.

## Common mistakes

- Skipping evaluation and only checking “looks good” demos.
- No tool schema / vague tool descriptions → bad function calls.
- Multi-agent complexity without an orchestrator or shared memory contract.
- Tuning temperature when the real issue is bad retrieval.

## Study focus order

1. RAG + evaluation (2.1)  
2. Agents, tools, memory (2.2)  
3. Observability + prompt/parameter tuning (2.3)  
4. Multi-agent and approval patterns (2.2)

## Check your understanding

Design an agent that books meetings via an API: list role, tools, memory approach, approval rules, and three metrics you would monitor.
