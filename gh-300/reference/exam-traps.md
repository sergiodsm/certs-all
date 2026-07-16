# Exam Traps — High-Frequency Wrong Answers

Read this the night before. Each trap pairs a **tempting answer** with the **correct reasoning**.

---

## Trap 1 — Content exclusions stop Agent Mode

| Tempting | Correct |
|---|---|
| “Add content exclusions to stop Agent reading `/secrets`” | Exclusions do **not** fully apply to Agent Mode / CLI / coding agent. Use other controls. |

---

## Trap 2 — Tests passed ⇒ ship AI code

| Tempting | Correct |
|---|---|
| Skip review because generated tests are green | Tests may be shallow; humans still validate assertions & security. |

---

## Trap 3 — GitHub owns suggestions

| Tempting | Correct |
|---|---|
| GitHub owns all Copilot output | GitHub **does not claim ownership**; **you** are responsible for accepted code. |

---

## Trap 4 — Wrong mode for the job

| Need | Wrong pick | Right pick |
|---|---|---|
| Selective multi-file accept | Agent Mode | Edit Mode |
| Autonomous run/fix loop | Edit Mode only | Agent Mode |
| Plan without edits | Agent unrestricted | Plan Mode / negative constraints |

---

## Trap 5 — Plan tier off-by-one

| Need | Wrong | Right |
|---|---|---|
| Content exclusions | Pro | Business/Enterprise |
| Org audit of Copilot admin actions | Individual settings | Org/Enterprise audit logs |
| Enterprise knowledge features | Business | Often Enterprise |

---

## Trap 6 — Public-code indemnity setting name

| Tempting | Correct |
|---|---|
| “Enable license checking” / “block MIT” | Set **Suggestions matching public code → Blocked** |

---

## Trap 7 — Exclusions mean absolute secret safety

| Tempting | Correct |
|---|---|
| Exclusions guarantee secrets never enter prompts | Path controls on supported surfaces; humans can still paste secrets; IDE may expose limited semantics |

---

## Trap 8 — MCP misunderstood

| Tempting | Correct |
|---|---|
| MCP deletes audit logs / grants free Enterprise | MCP connects agents to **external tools/context** via a standard protocol |

---

## Trap 9 — Data retention absolutism

| Tempting | Correct |
|---|---|
| “All plans train on your private code” or “nothing is ever retained anywhere” | Retention/training depends on **plan + surface**; verify current docs; CLI/Agent often differ from IDE Business posture |

---

## Trap 10 — Two-section exam mechanic

| Tempting | Correct |
|---|---|
| “I’ll fix Section 1 answers later” | You **cannot return** after advancing. Review Section 1 fully first. |

---

## Trap 11 — Responsible AI as isolated trivia

Responsible AI themes appear **inside** feature/governance scenarios. Always ask: where is human oversight?

---

## Trap 12 — Feedback publishes private code

| Tempting | Correct |
|---|---|
| Sending Chat feedback publishes the private repo | Feedback is governed by product/org settings; it does not auto-publish private repositories |

---

## Trap 13 — Propagation impatience

| Tempting | Correct |
|---|---|
| Exclusions broken because IDE didn’t update instantly | Allow up to ~**30 minutes** + reload |

---

## Trap 14 — Sub-Agents exist to remove auth

| Tempting | Correct |
|---|---|
| Sub-Agents remove authentication needs | They **delegate specialized work** and optimize context usage |

---

## 60-second pre-submit checklist

1. Did I pick the right **surface** (inline/chat/edit/agent/cli)?  
2. Did I pick the right **plan tier**?  
3. Did I respect the **exclusion gotcha**?  
4. Did I keep a **human** in the accountability loop?  
5. Is the option **document-precise** rather than vaguely plausible?
