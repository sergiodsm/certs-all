# AB-900 Complementary Study Guide

**Exam:** AB-900 — Microsoft 365 Copilot and Agent Administration Fundamentals  
**Credential:** Microsoft 365 Certified: Copilot and Agent Administration Fundamentals  
**Companion to:** [`../AB-900-topics.md`](../AB-900-topics.md) · Instructor prompt: [`../AB-900-PROMPT.md`](../AB-900-PROMPT.md)

This folder holds **admin-instructor study notes**: official bullet mapping, compare/choose tables, exam traps, hands-on checklists, and checkpoints. Use with the topics map and practice banks.

| Resource | Role |
|----------|------|
| [`../AB-900-topics.md`](../AB-900-topics.md) | Official skill map, weights, hardest→easiest order |
| `./` (this folder) | Deep dives per topic |
| [`../practice/`](../practice/) | Unofficial practice questions (not exam dumps) |
| [`../AB-900-PROMPT.md`](../AB-900-PROMPT.md) | Prompt for AI-guided tutoring / content generation |

> Skills measured as of **July 22, 2026**. Re-check: [AB-900 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ab-900) · [aka.ms/ab900-StudyGuide](https://aka.ms/ab900-StudyGuide)

---

## How to use this guide

1. Start with [00-exam-roadmap.md](./00-exam-roadmap.md) and pick a study path.  
2. Follow the Pass 1 / Pass 2 order in the roadmap (Domain 2 depth first).  
3. For each topic: Core concepts → Compare tables → Hands-on → Checkpoint (closed-book).  
4. Drill matching questions in [`../practice/`](../practice/).  
5. Before exam day: mixed mock + traps + admin-center chooser from Topic 01.

---

## Topic files

### Strategy

| # | File | Focus |
|---|------|--------|
| 0 | [00-exam-roadmap.md](./00-exam-roadmap.md) | Study paths, how the exam thinks, exam-day ops, pass mindset, practice loop |

### Domain 1 — Core features and objects (30–35%)

| # | File | Official skill block |
|---|------|----------------------|
| 1 | [01-m365-objects-admin-centers.md](./01-m365-objects-admin-centers.md) | 1.1 Licenses, M365/Exchange/SharePoint/Teams objects |
| 2 | [02-security-principles-zero-trust.md](./02-security-principles-zero-trust.md) | 1.2 Zero Trust, AuthN/AuthZ, threat protection, Defender XDR |
| 3 | [03-entra-identity-access.md](./03-entra-identity-access.md) | 1.3 Entra ID, CA, SSO, MFA/risk, Secure Score, audit, PIM, apps |

### Domain 2 — Data protection and governance (35–40%)

| # | File | Official skill block |
|---|------|----------------------|
| 4 | [04-purview-protection-lifecycle.md](./04-purview-protection-lifecycle.md) | 2.1 Purview IP, DLP, IRM, Comm Compliance, DSPM for AI, lifecycle |
| 5 | [05-copilot-data-security-graph.md](./05-copilot-data-security-graph.md) | 2.2 Copilot data access, Graph, permissions, responsible AI |
| 6 | [06-governance-risks-alerts.md](./06-governance-risks-alerts.md) | 2.3 Compliance Manager, explorers, alerts, eDiscovery Content search |
| 7 | [07-sharepoint-oversharing.md](./07-sharepoint-oversharing.md) | 2.4 Oversharing tools, DAG reports, Advanced Management / RAC |

### Domain 3 — Copilot and agent administration (25–30%)

| # | File | Official skill block |
|---|------|----------------------|
| 8 | [08-copilot-features-licensing.md](./08-copilot-features-licensing.md) | 3.1 Copilot vs agents, monthly vs PAYG, Researcher/Analyst |
| 9 | [09-copilot-admin-tasks.md](./09-copilot-admin-tasks.md) | 3.2 Licenses, PAYG billing, usage/Analytics, prompts |
| 10 | [10-agent-admin-lifecycle.md](./10-agent-admin-lifecycle.md) | 3.3 Access, create, approval, monitor (M365 + Power Platform) |

### Reference (planned)

| File | Purpose |
|------|---------|
| `reference/glossary.md` | Short definitions |
| `reference/exam-traps.md` | Cross-topic gotchas |
| `reference/admin-centers-cheatsheet.md` | Object → admin center map |
| `reference/checklist.md` | Pre-exam skills checklist |

---

## Exam snapshot

| Item | Detail |
|------|--------|
| Duration | ~45 minutes |
| Passing score | **700 / 1000** |
| Typical items | ~40–60 (scenario MCQ / multi-select; confirm on schedule page) |
| Largest domain | Data protection & governance (**35–40%**) |
| Practice | [`../practice/`](../practice/) + Microsoft Learn practice assessment if available + [exam sandbox](https://aka.ms/examdemo) |

---

## Mental model (read once)

AB-900 tests whether you can reason as a **Microsoft 365 / Copilot administrator**:

- Which **admin center** owns the object?  
- Is the gap a **license**, a **permission**, or a **policy**?  
- Does Copilot respect **Graph + existing ACLs**?  
- Is the problem **threat** (Defender) or **governance** (Purview / oversharing)?  
- For agents: access → create → **approval** → monitor  

If you can answer those under time pressure, you are close to ready.

---

## Official links

- [AB-900 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ab-900)  
- [Exam sandbox](https://aka.ms/examdemo)  
- [Exam scoring](https://learn.microsoft.com/en-us/credentials/certifications/exam-scoring-reports)  
- [Microsoft 365 documentation](https://learn.microsoft.com/en-us/microsoft-365/)  
- [Microsoft 365 Copilot documentation](https://learn.microsoft.com/en-us/copilot/microsoft-365/)  
- [Microsoft Purview documentation](https://learn.microsoft.com/en-us/purview/)  
- [Microsoft 365 admin center help](https://learn.microsoft.com/en-us/microsoft-365/admin/)  
