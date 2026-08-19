# Domain 3 — Data Handling & Architecture (10–15%)

## Learning goal

Explain, end-to-end, what happens when Copilot produces a suggestion — and what that implies for **privacy, filtering, and trust**.

---

## 3.1 Suggestion lifecycle (memorize this diagram)

```text
┌──────────────────┐
│ Developer + IDE  │  open files, cursor, comments, intent
└────────┬─────────┘
         │ context gather
         ▼
┌──────────────────┐
│ Prompt building  │  assemble model input from intent + context
└────────┬─────────┘
         │ request
         ▼
┌──────────────────┐
│ GitHub proxy     │  pre-process: policy, toxicity, relevance, routing
│ (Azure path)     │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ LLM inference    │  candidate completions
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ Post-processing  │  safety, quality, security heuristics,
│                  │  public-code matching, truncation/discard
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│ IDE presentation │  developer Accept / Reject / Edit
└──────────────────┘
```

**Exam implications**

- Suggestions are **proposals**, not auto-merges.  
- “Why no suggestion?” can be **post-processing filters**, not only “model failed.”  
- Prompts do **not** go “straight from laptop to random public LLM” without GitHub’s service path/policies.

---

## 3.2 Input processing & prompt building

**Prompt building** = combining:

- User intent (typed code / Chat question / Agent goal)  
- Available editor/repo context (nearby code, comments, selected files, instructions)  
- Product/system framing  

**Common inline context sources**

- Current file near cursor  
- Related open files (when available)  
- Comments and docstrings  
- Language/framework cues  

**Not** typical context: “all of GitHub.com unbounded,” unrelated email, lunch menus (distractors).

---

## 3.3 Proxy filtering & post-processing

| Stage | Role |
|---|---|
| Pre-processing / proxy | Policy checks, toxicity/relevance filtering, routing to model |
| Model | Generate candidates |
| Post-processing | Secondary safety, quality/security checks, **public-code matching**, discard/truncate failing candidates |

**Scenario:** Org sets “Suggestions matching public code: **Blocked**.” User sees fewer completions.

**Best explanation:** Matching/near-matching public-code candidates are filtered in the pipeline — not “all licenses revoked.”

---

## 3.4 Data usage, flow, and sharing (plan-sensitive)

Enterprises care about: **what leaves the workstation**, **retention**, **training use**, **abuse monitoring**.

Study current docs for your plan, but exam-relevant patterns historically include:

| Context | Typical expectation to study |
|---|---|
| Business/Enterprise IDE interactions | Strong privacy posture — prompts/suggestions often **not retained** for model training (verify current docs) |
| Individual plans | Interaction data **may** be usable for model improvement **unless opted out** |
| CLI / Agent Mode workflows | Often **short retention window** (commonly cited: ~28 days) for abuse monitoring / auditing — **not** the same as “train public models on your private code” |
| Product telemetry | Longer retention for product analytics (engagement), distinct from code training |

**Exam-safe answer style:**  
“Verify current Microsoft/GitHub documentation for your plan’s data-handling promises” beats absolute claims that ignore plan differences.

### Professional talking points for stakeholders

1. Distinguish **telemetry** vs **prompt/code retention** vs **model training**.  
2. Distinguish **IDE inline** vs **CLI/Agent** retention behaviors.  
3. Never claim “exclusions encrypt the laptop” or “Copilot stores all private code in public Gists.”

---

## 3.5 LLM / Copilot limitations (architecture view)

| Limitation | Practical effect |
|---|---|
| No guaranteed truth | Confident wrong APIs |
| Context window bounds | Misses files you didn’t attach / excluded |
| Weak undocumented business rules | Needs prompts + instructions + human judgment |
| Non-determinism | Same prompt can vary |
| No automatic compliance | Does not replace legal/security sign-off |

**Correct exam stance:** Copilot lacks full product judgment; engineers supply intent and verify outcomes.

---

## 3.6 Worked example — architecture reasoning

**Scenario:** Security asks why an excluded secrets file still “felt” relevant after Chat analysis elsewhere, and whether the model “stored” it.

**Teachable answer structure:**

1. Explain exclusions apply on **supported surfaces** (Domain 6).  
2. Explain Chat/Agent/CLI may differ.  
3. Explain retention/training depends on **plan + surface**.  
4. Recommend: never paste secrets; keep exclusions; provide non-secret interfaces as context.

---

## Domain 3 quick self-test

1. Draw the lifecycle from memory.  
2. Define prompt building in one sentence.  
3. Name three post-processing jobs.  
4. Why do enterprises care about data flow?  
5. Give two LLM limitations that show up in coding assistants.
