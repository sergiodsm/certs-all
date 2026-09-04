# 00 — Exam Roadmap & Strategy

**Exam:** AB-900 — Microsoft 365 Copilot and Agent Administration Fundamentals  
**Credential:** Microsoft 365 Certified: Copilot and Agent Administration Fundamentals  
**Skills measured as of:** July 22, 2026  

Official study guide: [Microsoft Learn — AB-900](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ab-900) · Short link: [aka.ms/ab900-StudyGuide](https://aka.ms/ab900-StudyGuide)

Companion map: [`../AB-900-topics.md`](../AB-900-topics.md)  
Practice banks: [`../practice/`](../practice/)  
Instructor prompt: [`../AB-900-PROMPT.md`](../AB-900-PROMPT.md)

---

## Exam snapshot

| Item | Detail |
|------|--------|
| Level | Fundamentals |
| Duration | ~45 minutes (confirm on scheduling page) |
| Question count | Typically ~40–60 (pool varies) |
| Passing score | **700 / 1000** (scaled) |
| Delivery | Proctored (Pearson VUE / Microsoft testing) |
| Focus | M365 objects, Entra security, Purview/governance, Copilot & agent admin |
| Practice assessment | Use Microsoft Learn practice assessment if available + [exam sandbox](https://aka.ms/examdemo) |

This is **not** an Azure AI / Azure OpenAI developer exam. Think **admin centers**, permissions, Purview, and Copilot/agent lifecycle — not writing prompts as a developer skill.

---

## Skills at a glance (where points live)

| Weight | Official domain | Local topics |
|--------|-----------------|--------------|
| **30–35%** | Identify the core features and objects of Microsoft 365 services | [01](./01-m365-objects-admin-centers.md) · [02](./02-security-principles-zero-trust.md) · [03](./03-entra-identity-access.md) |
| **35–40%** | Understand data protection and governance tasks for Microsoft 365 and Copilot | 04–07 (Purview, Copilot data security, governance risks, SharePoint oversharing) |
| **25–30%** | Perform basic administrative tasks for Copilot and agents | 08–10 (features/licensing, Copilot admin, agent lifecycle) |

**Study takeaway:** Domain 2 is the largest scoring block. Prioritize Purview + Copilot data security + SharePoint oversharing, then Entra identity (Domain 1.3), then Copilot/agent admin procedures.

Related topics may appear even if not listed as bullets. Prefer **GA** features; Preview only if commonly used and clearly labeled.

---

## Recommended study paths

### Path A — Working M365 admin (already live in admin centers): 1–2 weeks

| Day block | Focus | Outcome |
|-----------|-------|---------|
| 1–2 | Domain 2 depth (04–07) | Labels vs DLP vs retention; Graph + permissions; oversharing tools |
| 3 | Domain 1.3 Entra ([03](./03-entra-identity-access.md)) | CA, MFA, PIM, app regs vs enterprise apps |
| 4 | Domain 3 (08–10) | License vs PAYG; Researcher/Analyst; agent approval path |
| 5 | Domain 1.1–1.2 skim ([01](./01-m365-objects-admin-centers.md), [02](./02-security-principles-zero-trust.md)) | Admin-center chooser + Zero Trust / Defender XDR vocabulary |
| 6–7 | Mixed practice + traps | ≥80% on Domain 2 set; timed mixed mock |

### Path B — MS-900 / light M365 experience: 3–4 weeks

| Week | Focus |
|------|-------|
| 1 | [01](./01-m365-objects-admin-centers.md) + [02](./02-security-principles-zero-trust.md) + [03](./03-entra-identity-access.md) — build the object map and identity mental model |
| 2 | Topics 04–06 — Purview products, Copilot data path, governance tool chooser |
| 3 | Topics 07–10 — Oversharing + Copilot/agent admin |
| 4 | Practice loop: Domain banks → mixed mock → weak-area re-read |

### Path C — New to Microsoft 365 admin: 5–6 weeks

1. Get a **Microsoft 365 developer / trial tenant** if possible — reading alone is weaker for this exam.  
2. Week 1–2: Users, licenses, M365 / Exchange / SharePoint / Teams admin centers ([01](./01-m365-objects-admin-centers.md)).  
3. Week 3: Zero Trust + Entra ([02](./02-security-principles-zero-trust.md), [03](./03-entra-identity-access.md)).  
4. Week 4–5: Purview + Copilot data security + oversharing (04–07).  
5. Week 6: Copilot/agent admin (08–10) + timed mocks.

---

## Hardest → easiest (study order)

Difficulty = how easy it is to confuse on exam day (not only weight). Full rationale: [`../AB-900-topics.md`](../AB-900-topics.md).

```text
Pass 1 (depth):  04 → 05 → 06 → 03 → 10
Pass 2 (faster): 07 → 08 → 01 → 09 → 02
Pass 3:          Mixed mock + exam-traps + checklist
```

Do **not** skip Domain 1 objects — “which admin center?” items are easy points if you memorize the map.

---

## How the exam thinks

Most items are **admin scenarios**. Pattern:

1. Stakeholder need (license a user, stop oversharing, investigate sign-in, govern an agent…).  
2. Two answers that “kinda work.”  
3. Correct answer = the one that names the **right admin center / Purview tool / control**, and respects **existing permissions**.

**Tie-breaker rules:**

| Situation | Prefer |
|-----------|--------|
| Copilot “sees” data | Microsoft Graph + **user’s existing permissions** — Copilot does not grant new ACL |
| Data protection | Match tool to job: label vs DLP vs retention vs DSPM for AI |
| Oversharing | SharePoint governance (DAG reports, Advanced Management / RAC) — not Defender malware |
| Privileged access | **PIM** = just-in-time elevation, not day-to-day MFA for everyone |
| Agents | Access → create → **approval** → monitor (M365 + Power Platform admin centers) |
| Identity vs app | **App registration** = app identity definition; **Enterprise app** = tenant instance / SSO assignment |

---

## Exam-day operations

| Rule | Why it matters |
|------|----------------|
| ~45 minutes, ~40–60 questions | Roughly **45–70 seconds** per item — flag and move after ~90 seconds |
| Read the **last sentence** of the stem | Often names the exact goal (which center, which control) |
| Multi-select: select **exactly N** | Partial sets usually score zero — eliminate systematically |
| Case / multi-part | Keep object ownership straight (Exchange mailbox ≠ SharePoint site ≠ Teams policy) |
| Use [exam sandbox](https://aka.ms/examdemo) before test day | Reduces UI surprise under proctoring |
| Quiet room, clear desk, ID ready | Online Pearson VUE requirements |

Retakes: confirm current Microsoft policy (first retake wait, annual attempt caps) on Learn before you schedule a retry.

---

## Pass mindset (700/1000)

- 700 is a **scaled** pass — do not aim to “barely scrape” on practice.  
- Target **≥80–85%** on Domain 2 practice and **≥80%** on a timed mixed mock before booking.  
- Official practice assessments (when available) are often slightly easier than the live exam — treat 75% as “not ready yet.”  
- Wrong answers are usually **wrong tool / wrong center / wrong control**, not obscure trivia.

---

## Weekly practice loop

While studying:

```text
1. Pick one topic file (prefer Pass 1 order)
2. Read Core concepts + Compare/choose tables
3. Complete the Hands-on checklist in a lab tenant (or simulate UI paths from docs)
4. Answer the Checkpoint questions closed-book
5. Drill 8–12 questions from ../practice/ for that domain
6. Log 3 near-miss distractors — and why they fail
```

Before exam week:

```text
1. Full mixed mock under ~45 minutes
2. Re-read exam traps across Domains 1–3
3. Re-check official study guide for July 22, 2026 (or newer) skill changes
4. Skim admin-centers cheatsheet + Purview tool chooser
```

---

## Source-of-truth hierarchy

When docs conflict with blogs or third-party dumps:

1. [Official AB-900 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ab-900)  
2. Microsoft Learn documentation (M365, Entra, Purview, Copilot)  
3. This repo’s [`AB-900-topics.md`](../AB-900-topics.md) + `topics_details/`  
4. Community write-ups  

Practice questions in [`../practice/`](../practice/) are **unofficial study aids** — not Microsoft exam dumps. Do not use brain dumps.

---

## Readiness bar (book the exam when…)

- [ ] You can name which admin center owns mailboxes, sites, teams/policies, identity, Purview, and Power Platform agents  
- [ ] You can explain Zero Trust in one sentence and AuthN vs AuthZ without hesitation  
- [ ] You can walk a failed sign-in: MFA vs Conditional Access vs risky sign-in  
- [ ] You know PIM, Identity Secure Score, audit logs, app registration vs enterprise app at fundamentals level  
- [ ] You can match Purview tools to scenarios (labels, DLP, retention, IRM, Comm Compliance, DSPM for AI, Compliance Manager, eDiscovery Content search)  
- [ ] You can state: Copilot respects Graph + existing permissions; oversharing ≠ malware  
- [ ] You can compare monthly Copilot license vs pay-as-you-go and sketch agent approval/lifecycle  
- [ ] Timed mixed practice ≥80% with Domain 2 not dragging the score  

---

## Learn links

| Resource | URL |
|----------|-----|
| AB-900 study guide | https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ab-900 |
| Exam sandbox | https://aka.ms/examdemo |
| Exam scoring | https://learn.microsoft.com/en-us/credentials/certifications/exam-scoring-reports |
| Microsoft 365 docs | https://learn.microsoft.com/en-us/microsoft-365/ |
| Copilot docs | https://learn.microsoft.com/en-us/copilot/microsoft-365/ |
| Purview docs | https://learn.microsoft.com/en-us/purview/ |
| M365 admin center help | https://learn.microsoft.com/en-us/microsoft-365/admin/ |
