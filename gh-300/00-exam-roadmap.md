# 00 — Exam Roadmap & Strategy

## Learning outcomes

By the end of this guide you will be able to:

1. Map every GH-300 skill area to a concrete configuration or workflow.
2. Distinguish Individual vs Business vs Enterprise behaviors under exam scenarios.
3. Configure Copilot professionally (IDE, CLI, org policy, exclusions, customizations).
4. Avoid the documented traps that fail otherwise strong candidates.

---

## Recommended study paths

### Path A — Daily Copilot user (Business/Enterprise): 4–8 hours

| Block | Hours | Material |
|---|---|---|
| 1 | 1.0 | Domains 1 + 3 (responsible AI + architecture) |
| 2 | 2.0 | Domain 2 depth + [plan-tiers-cheatsheet](./reference/plan-tiers-cheatsheet.md) |
| 3 | 1.5 | Domain 6 + Lab 05 (exclusions) + Lab 04 (org policy) |
| 4 | 1.5 | Agent/MCP Lab 03 + Domains 4–5 skim |
| 5 | 1.0 | Practice assessment + [exam-traps](./reference/exam-traps.md) |

### Path B — Daily Copilot user (Free/Pro only): 10–20 hours

Add hands-on admin simulation even if you lack org access:

- Read Labs 04–05 carefully and memorize the UI paths and precedence rules.
- Build the plan-tier matrix from memory twice.
- Practice Agent Mode / Edit Mode / CLI yourself (Free/Pro still teach features).

### Path C — New to Copilot: 3–6 weeks

Week 1: Labs 01–02 + Domain 2 basics  
Week 2: Domains 4–5 + examples catalog (daily prompting practice)  
Week 3: Domains 1 + 3 + Lab 03  
Week 4: Domain 6 + Labs 04–06 + practice assessment loop  
Week 5–6: Weak-domain drill + full mock under timed conditions

---

## How the exam thinks

Most items are **scenarios**. Pattern:

1. Stakeholder need (privacy, productivity, indemnity, agent autonomy…).
2. Two answers that “kinda work.”
3. Correct answer = the one that matches **documented GitHub/Microsoft governance**.

**Tie-breaker rule:** pick the option that is *most precise* about plan tier, surface (IDE vs Agent vs CLI), and human accountability.

---

## Exam-day operations

| Rule | Why it matters |
|---|---|
| Two sections — **no return** after advancing | Review Section 1 completely before submit |
| ~65 questions / 100 minutes | ~90 seconds each; flag and move after 2 min |
| Multi-response questions | Eliminate; do not guess partial sets |
| Register with a **personal Microsoft account** | Protects cert portability if you change jobs |
| Quiet room, one monitor, clear desk | Online Pearson VUE requirements |

Retakes: 24h after first fail; longer waits later; max 5 attempts/year (confirm current policy on Microsoft Learn).

---

## Passing score mindset

700/1000 is a **scaled** pass. Aim for **≥85%** on practice assessments before scheduling. Official practice is slightly easier than the real exam — treat 80% as “not ready yet.”

---

## Weekly practice loop (while studying)

```text
1. Pick one domain
2. Read the complementary chapter
3. Complete the matching lab (or re-run it)
4. Answer 10 questions from ../gh-300-topics.md
5. Write 3 wrong answers you almost chose — and why they fail
```

---

## Source-of-truth hierarchy

When docs conflict with blogs:

1. [Microsoft GH-300 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/gh-300)
2. [docs.github.com/en/copilot](https://docs.github.com/en/copilot)
3. This complementary guide
4. Community write-ups

Re-check plan names, retention numbers, and Agent/exclusion caveats in the week before your exam — product UI labels evolve.
