# Domain 1 — Use GitHub Copilot Responsibly (15–20%)

## Professor framing

Responsible AI on GH-300 is not philosophy trivia. Every scenario asks: **who is accountable, what can go wrong, and what mitigation is proportionate?**

Core sentence to memorize:

> **Copilot suggests. Humans decide, verify, and own the merged code.**

---

## 1.1 Risks and limitations of generative AI

| Risk | Exam-visible symptom | Mitigation |
|---|---|---|
| Hallucination | Invented APIs, fake packages, wrong flags | Validate against docs, types, builds, tests |
| Insecure patterns | Weak crypto, SQL concat, hardcoded secrets | Security review + SAST + secret scanning |
| Outdated advice | Deprecated APIs, old framework idioms | Pin versions in prompt; check current docs |
| Incomplete edge cases | Happy-path only | Explicitly request boundaries & failure modes |
| License / public-code risk | Near-verbatim public snippets | Public-code filter (Block) + legal review |
| Privacy leakage | Secrets pasted into Chat | Never paste secrets; use exclusions + discipline |
| Over-reliance | Shipping without review | Mandatory human review for production paths |
| Bias / unfairness | Stereotyping in comments, hiring helpers, policies | Human review against inclusive standards |

### Worked example — weak but compiling code

**Scenario:** Copilot suggests MD5 for password hashing. Code compiles and tests “pass” with a toy suite.

**Responsible reading:** This is a **security limitation of generative AI**, not a licensing issue and not “training data leakage.”

**Correct action:** Reject/replace with a modern KDF (e.g., Argon2/bcrypt/scrypt per org standard), add real tests, run security review.

---

## 1.2 Ethical and responsible usage principles

Map scenarios to principles (Microsoft Responsible AI language appears in exam framing):

| Principle | Coding-assistant meaning |
|---|---|
| Fairness | Avoid biased outputs; review AI-written policies/comments |
| Reliability & safety | Validate correctness and security before ship |
| Privacy & security | Minimize sensitive context in prompts |
| Inclusiveness | Accessible language/UX; don’t encode stereotypes |
| Transparency | Know filters/policies exist; don’t pretend AI is infallible |
| Accountability | Named humans own accepted code and decisions |

**Exam tip:** Fairness ≠ Inclusiveness. Fairness is about equitable outcomes/bias; inclusiveness is about designing so people can participate. Both can appear as distractors in the same item.

---

## 1.3 Potential harms and mitigations (professional checklist)

Use this as an org onboarding checklist:

1. **Code quality harm** → PR review + CI gates  
2. **Security harm** → threat prompts, dependency scanning, secret scanning  
3. **IP/license harm** → public-code Block + counsel for high-risk reuse  
4. **Privacy harm** → content exclusions, Chat hygiene, no prod data in prompts  
5. **Operational harm** → never let Agent Mode alone declare incident root cause  
6. **Compliance harm** → audit logs, org policies, documented acceptance criteria  

---

## 1.4 Validate AI output (mandatory skill)

Validation ladder (apply bottom-up):

```text
1. Read the suggestion (does it match intent?)
2. Typecheck / compile
3. Unit tests (including edges you asked for)
4. Security & license glance
5. Peer / PR review for production paths
```

### Bad practice (exam distractor)

- “Tests passed, so skip review.”  
  Passing tests can be **shallow**. Review assertions for real requirements.

### Good practice (exam answer shape)

- Treat Copilot as a junior pair: useful drafts, never final authority.

---

## 1.5 Operating Copilot responsibly day to day

| Do | Don’t |
|---|---|
| Keep developers accountable for merges | Blind-accept all ghost text |
| Put constraints in prompts and instructions files | Paste production secrets for “better context” |
| Use Agent Mode with boundaries + review | Let Agent Mode decide production incidents alone |
| Prefer small incremental refactors | Unreviewed whole-module rewrites |
| Document when AI assisted high-risk changes (team policy) | Claim AI output is legally guaranteed |

### Scenario drill

**Prompt:** “Teammate wants Copilot Chat to decide production incident root cause without engineer review. Highest risk?”

**Answer:** Over-reliance / insufficient human oversight.

---

## Mini lab — Responsible AI review of a suggestion

1. Ask Copilot Chat to generate an auth middleware.  
2. Intentionally review for: injection, authz gaps, logging of tokens, weak crypto.  
3. Write a 5-bullet rejection note as if mentoring a junior.  
4. Re-prompt with security constraints and compare.

Template rejection note:

```text
Rejecting suggestion because:
- Uses string concat for SQL (injection)
- Logs Authorization header
- No rate limiting on login
- Hardcodes JWT secret fallback
- Missing authz check on admin route
Next prompt: regenerate with parameterized queries, no secret logging, …
```

---

## Domain 1 quick self-test

1. Name five generative AI risks relevant to coding assistants.  
2. Distinguish fairness vs inclusiveness in one sentence each.  
3. Why can green unit tests still be irresponsible to ship?  
4. What is the accountability model for accepted Copilot code?

When stuck, re-read the Domain 1 Q&A in `../gh-300-topics.md`.
