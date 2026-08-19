# GH-300 Complementary Study Guide

**Exam:** GH-300 — GitHub Copilot  
**Level:** Intermediate  
**Companion to:** [`../gh-300-topics.md`](../gh-300-topics.md) (official topics + practice Q&A)

This folder is a **professor-style complementary guide**: explanations, professional setup labs, worked examples, and exam traps that the topic outline alone does not teach. Use both files together.

| Resource | Role |
|---|---|
| `../gh-300-topics.md` | Official skill map + 60 practice questions with keys |
| `./gh-300/` (this guide) | How to configure, how to reason, how to pass |

> Skills measured as of **August 7, 2026**. Always re-check: [GH-300 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/gh-300).

---

## How to use this guide

1. Read [00-exam-roadmap.md](./00-exam-roadmap.md) and pick a study timeline.
2. Study Domains 1→6 in order (or start with Domain 2 + 6 if you already use Copilot daily).
3. Complete every lab in [`labs/`](./labs/) — scenario questions reward hands-on muscle memory.
4. Drill [`reference/plan-tiers-cheatsheet.md`](./reference/plan-tiers-cheatsheet.md) until you can recite Business vs Enterprise differences.
5. Walk [`examples/scenarios-walkthrough.md`](./examples/scenarios-walkthrough.md), then take the official Microsoft free practice assessment.
6. Before exam day: [`reference/exam-traps.md`](./reference/exam-traps.md) + checklist.

---

## Guide map

### Core domains

| # | File | Weight | Focus |
|---|---|---|---|
| 0 | [00-exam-roadmap.md](./00-exam-roadmap.md) | — | Strategy, timeline, exam-day ops |
| 1 | [01-responsible-ai.md](./01-responsible-ai.md) | 15–20% | Ethics, harms, validation, oversight |
| 2 | [02-features.md](./02-features.md) | 25–30% | IDE, CLI, Agent, MCP, Spaces, org policy |
| 3 | [03-data-architecture.md](./03-data-architecture.md) | 10–15% | Pipeline, retention, LLM limits |
| 4 | [04-prompt-engineering.md](./04-prompt-engineering.md) | 10–15% | Context, zero/few-shot, prompt files |
| 5 | [05-productivity.md](./05-productivity.md) | 10–15% | Tests, refactor, docs, security, SDLC |
| 6 | [06-privacy-safeguards.md](./06-privacy-safeguards.md) | 10–15% | Exclusions, public-code filter, ownership |

### Professional setup labs

| Lab | What you configure |
|---|---|
| [labs/01-ide-setup.md](./labs/01-ide-setup.md) | VS Code, Visual Studio, JetBrains — install, auth, settings |
| [labs/02-cli-setup.md](./labs/02-cli-setup.md) | GitHub Copilot CLI — install, interactive, sessions, scripts |
| [labs/03-agent-mcp-setup.md](./labs/03-agent-mcp-setup.md) | Agent Mode, Edit/Plan, MCP, Sub-Agents |
| [labs/04-org-policies.md](./labs/04-org-policies.md) | Org/Enterprise policies, Code Review, audit logs, REST API |
| [labs/05-content-exclusions.md](./labs/05-content-exclusions.md) | Repo/org/enterprise exclusions end-to-end |
| [labs/06-instructions-prompts.md](./labs/06-instructions-prompts.md) | Instructions files, prompt files, customization |

### Reference & examples

| File | Purpose |
|---|---|
| [reference/plan-tiers-cheatsheet.md](./reference/plan-tiers-cheatsheet.md) | Free / Pro / Pro+ / Business / Enterprise matrix |
| [reference/exam-traps.md](./reference/exam-traps.md) | High-frequency wrong answers |
| [reference/glossary.md](./reference/glossary.md) | Exam vocabulary |
| [reference/checklist.md](./reference/checklist.md) | Pre-exam mastery checklist |
| [examples/prompts-catalog.md](./examples/prompts-catalog.md) | Ready-to-use prompt patterns |
| [examples/scenarios-walkthrough.md](./examples/scenarios-walkthrough.md) | End-to-end scenario reasoning |

---

## Exam snapshot

| Item | Detail |
|---|---|
| Duration | 100 minutes |
| Passing score | 700 / 1000 |
| Format | Scenario MCQ / multi-response; proctored (Pearson VUE) |
| Validity | 2 years (renew via free Microsoft Learn assessment) |
| Related file | Practice Q&A in `gh-300-topics.md` |

---

## Mental model (read this once)

GH-300 does **not** primarily test “can you accept ghost text?”  
It tests whether you can reason as a **developer + Copilot administrator**:

- Which **plan** unlocks which control?
- What context leaves the workstation, and for how long?
- What do **content exclusions** cover — and what do they **not** cover?
- When is **Agent Mode** appropriate vs **Edit Mode** vs inline?
- How do you keep **humans accountable** for AI output?

If you can answer those under time pressure, you pass.

---

## Official links

- [GH-300 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/gh-300)
- [GitHub Copilot certification](https://learn.microsoft.com/en-us/credentials/certifications/github-copilot/)
- [GitHub Copilot docs](https://docs.github.com/en/copilot)
- [Content exclusion](https://docs.github.com/en/copilot/concepts/context/content-exclusion)
- [Customization cheat sheet](https://docs.github.com/en/copilot/reference/customization-cheat-sheet)
