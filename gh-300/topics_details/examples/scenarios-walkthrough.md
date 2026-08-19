# Scenario Walkthroughs — How to Reason on GH-300

Work these out loud. Then compare with the answer keys. These are **unofficial** study scenarios.

---

## Scenario A — Regulated fintech wants Copilot

**Facts:** Company needs org policies, content exclusions for `/pci/**`, IP indemnity posture, and auditability of admin changes. Developers already use Pro individually.

**Question:** Which plan direction, and which first three settings?

**Reasoning**

1. Individual Pro cannot provide org exclusions/indemnity/admin audit.  
2. Move to **Business** at minimum; consider **Enterprise** if advanced knowledge/custom models/PR features required.  
3. Settings: public-code **Blocked**; content exclusions for `/pci/**`; enable audit log review process.  
4. Train humans: never paste PAN/secrets into Chat; Agent Mode tightly governed.

**Answer shape:** Business/Enterprise + Block + exclusions + audit + training.

---

## Scenario B — Agent keeps reading secrets

**Facts:** Exclusions configured for `**/secrets/**`. Inline suggestions stopped in those files. Agent Mode still proposes reading them.

**Question:** Are exclusions misconfigured?

**Reasoning**

1. Inline behavior suggests exclusions **work** on supported surfaces.  
2. Agent Mode is a documented **non-full-application** surface for exclusions.  
3. Misconfiguration is less likely than expecting the wrong control.

**Answer:** Exclusions behaving as designed for inline; use different Agent controls.

---

## Scenario C — Fewer suggestions after hardening

**Facts:** Yesterday admin set public-code matching to Blocked. Users complain Copilot “broke.”

**Reasoning:** Filter removes near-matching public snippets → fewer completions. Expected. Not mass seat revocation.

---

## Scenario D — Choose the mode

**Facts:** Need to rename a type across 8 files; want to accept hunks selectively; no terminal autonomy required.

**Answer:** Edit Mode / Copilot Edits — not full Agent.

---

## Scenario E — Hallucinated package

**Facts:** Chat invents `ultra-hash-pro` on npm. Suggestion looks clean.

**Answer:** Hallucination → validate against registry/docs/tests before trust. Responsible AI validation, not “disable Copilot forever.”

---

## Scenario F — Weak hashing compiles

**Facts:** Copilot suggests MD5 for passwords; unit tests pass with fixtures.

**Answer:** Insecure generative suggestion risk. Reject; use approved KDF; improve tests; security review.

---

## Scenario G — SDK “forgotten”

**Facts:** After security sprint, completions in `app.ts` no longer reflect helpers in `internal/sdk/*`.

**Answer:** Check whether SDK paths were content-excluded. If intentional, expose non-secret contracts on allowed paths.

---

## Scenario H — Prompt quality

**Facts:** Developer prompts “make payment better.” Output is vague and wrong framework.

**Answer:** Missing specificity/context. Rewrite with stack, signature, constraints, success criteria; attach payment module; consider few-shot for response shape.

---

## Scenario I — MCP for CI failures

**Facts:** Team wants Agent to read failing CI logs from an internal system.

**Answer:** Use MCP server integrating that system with least privilege; keep write actions gated; don’t confuse MCP with free Enterprise seats.

---

## Scenario J — Ownership debate

**Facts:** Legal asks who owns Copilot suggestions the team accepted into the product.

**Answer:** GitHub does not claim ownership of suggestions; the company/developers remain responsible for what they accept and distribute — still need license/security review.

---

## Scenario K — Sub-Agent usage

**Facts:** Parent Agent implements export feature; context window fills with CSV fixture brainstorming.

**Answer:** Delegate fixture generation to a Sub-Agent for isolated context; parent integrates after review.

---

## Scenario L — Section timing

**Facts:** Candidate is unsure about 6 items in Section 1 but advances to see Section 2 topics.

**Answer:** Operational mistake — cannot return. Flag and review Section 1 before advancing.

---

## How to practice

For each scenario, force this template:

```text
1) What is being asked (plan, mode, control, principle)?
2) Which domain(s)?
3) What is the tempting distractor?
4) What documented rule decides it?
5) One-sentence answer
```

Then reinforce with the 60 practice questions in `../../gh-300-topics.md`.
