# Exam AB-900: Microsoft 365 Copilot and Agent Administration Fundamentals — Topics Overview

Official certification topics from Microsoft Learn.  
Source of truth: [Study guide for Exam AB-900](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ab-900)  
Short link: [aka.ms/ab900-StudyGuide](https://aka.ms/ab900-StudyGuide)

**Skills measured as of:** July 22, 2026  
Re-check the study guide before exam day — Microsoft updates skill outlines.

**Deep dives:** [`topics_details/`](./topics_details/)  
**Practice banks:** [`practice/`](./practice/)  
**Instructor prompt:** [`AB-900-PROMPT.md`](./AB-900-PROMPT.md)

Practice questions are **unofficial study aids**. They are not Microsoft exam dumps.

---

## Exam snapshot

| Item | Detail |
|------|--------|
| Exam code | **AB-900** |
| Name | Microsoft 365 Copilot and Agent Administration Fundamentals |
| Level | Fundamentals |
| Duration | ~45 minutes (confirm on scheduling page) |
| Question count | Typically ~40–60 (pool varies) |
| Passing score | **700 / 1000** |
| Delivery | Proctored |
| Focus | Admin fundamentals for M365 objects, Purview/governance, Copilot & agents |

---

## Audience profile

Candidates should be familiar with Microsoft 365 core services, security, identity, data protection/governance, Copilot and agents, and admin centers (Exchange, SharePoint, Teams, Entra, Purview). Experience with AI productivity tools and modern IT management is expected.

---

## Skills at a glance

| # | Skill area | Weight | Local topics |
|---|------------|--------|--------------|
| 1 | Identify the core features and objects of Microsoft 365 services | **30–35%** | 01–03 |
| 2 | Understand data protection and governance tasks for Microsoft 365 and Copilot | **35–40%** | 04–07 |
| 3 | Perform basic administrative tasks for Copilot and agents | **25–30%** | 08–10 |

**Study takeaway:** Domain 2 is the largest scoring block. Prioritize Purview + Copilot data security + SharePoint oversharing.

---

## Study order: hardest → easiest

Difficulty = how hard the topic is to keep straight on exam day (not only weight).

| Rank | Difficulty | Topic | Weight | Why |
|------|------------|-------|--------|-----|
| 1 | Hardest | [04 — Purview protection & lifecycle](./topics_details/04-purview-protection-lifecycle.md) | 35–40% (shared) | Many similarly named tools; labels vs DLP vs retention vs DSPM |
| 2 | Very hard | [05 — Copilot data security & Graph](./topics_details/05-copilot-data-security-graph.md) | 35–40% (shared) | Graph + permissions model; easy to think Copilot “opens everything” |
| 3 | Hard | [06 — Governance risks & alerts](./topics_details/06-governance-risks-alerts.md) | 35–40% (shared) | Tool-to-scenario matching across Compliance Manager, IRM, DLP, eDiscovery |
| 4 | Hard | [03 — Entra identity & access](./topics_details/03-entra-identity-access.md) | 30–35% (shared) | CA, MFA, PIM, Secure Score, app regs — dense identity surface |
| 5 | Hard | [10 — Agent admin lifecycle](./topics_details/10-agent-admin-lifecycle.md) | 25–30% (shared) | Access → create → approval → monitor across two admin centers |
| 6 | Moderate | [07 — SharePoint oversharing](./topics_details/07-sharepoint-oversharing.md) | 35–40% (shared) | Smaller surface; DAG reports + Advanced Management / RAC |
| 7 | Moderate | [08 — Copilot features & licensing](./topics_details/08-copilot-features-licensing.md) | 25–30% (shared) | License vs PAYG; Researcher vs Analyst vs custom agents |
| 8 | Moderate | [01 — M365 objects & admin centers](./topics_details/01-m365-objects-admin-centers.md) | 30–35% (shared) | Which object lives where — memorize the map |
| 9 | Easier | [09 — Copilot admin tasks](./topics_details/09-copilot-admin-tasks.md) | 25–30% (shared) | Assign licenses, usage, prompts — procedural |
| 10 | Easiest | [02 — Security principles / Zero Trust](./topics_details/02-security-principles-zero-trust.md) | 30–35% (shared) | Short concept set; overlaps Domain 1.3 |

### Suggested pass order

```text
Pass 1 (depth):  04 → 05 → 06 → 03 → 10
Pass 2 (faster): 07 → 08 → 01 → 09 → 02
Pass 3:          Mixed mock + exam-traps + checklist
```

---

## Domain 1 — Core features and objects of Microsoft 365 (30–35%)

### 1.1 Core objects — [01](./topics_details/01-m365-objects-admin-centers.md)

- License types (users/groups) and feature access
- Microsoft 365 admin center: domains, org settings
- Exchange admin center: mailboxes, distribution groups
- SharePoint admin center: sites, libraries, folders; site roles/permissions
- Teams admin center: teams, channels, policies

### 1.2 Security principles — [02](./topics_details/02-security-principles-zero-trust.md)

- Zero Trust principles
- Authorization vs authentication methods
- Threat protection and intelligence
- Microsoft Defender XDR capabilities

### 1.3 Core security features — [03](./topics_details/03-entra-identity-access.md)

- Microsoft Entra ID
- Conditional Access, SSO
- Users/groups as security objects
- Troubleshoot sign-in (MFA, CA, risky sign-ins)
- Identity Secure Score, audit logs, PIM
- App registrations and Enterprise apps

---

## Domain 2 — Data protection and governance (35–40%)

### 2.1 Microsoft Purview — [04](./topics_details/04-purview-protection-lifecycle.md)

- Information Protection, DLP, Insider Risk Management, Communication Compliance, DSPM for AI, Data Lifecycle Management
- Sensitivity labels, classification, retention

### 2.2 Copilot data security — [05](./topics_details/05-copilot-data-security-graph.md)

- How Copilot accesses data; Microsoft Graph influence
- Permissions/controls in M365, Purview, Defender
- Responsible AI principles

### 2.3 Governance risks — [06](./topics_details/06-governance-risks-alerts.md)

- Compliance Manager, Data Explorer, IRM, DLP alerts
- Communication Compliance, activity explorer, DSPM for AI
- Content search (eDiscovery)

### 2.4 SharePoint oversharing — [07](./topics_details/07-sharepoint-oversharing.md)

- Troubleshoot oversharing tools
- Data access governance reports
- SharePoint Advanced Management / restricted access control

---

## Domain 3 — Copilot and agent administration (25–30%)

### 3.1 Features & capabilities — [08](./topics_details/08-copilot-features-licensing.md)

- Copilot vs agents
- Monthly license vs pay-as-you-go (incl. SharePoint)
- Enable/disable features
- Researcher, Analyst, custom agents use cases

### 3.2 Copilot admin tasks — [09](./topics_details/09-copilot-admin-tasks.md)

- Assign licenses; PAYG billing policies
- Usage/adoption (Copilot Analytics, M365 admin center)
- Manage prompts (save, share, schedule, delete)

### 3.3 Agent admin tasks — [10](./topics_details/10-agent-admin-lifecycle.md)

- User access to agents; create agents; approval process
- Monitor usage, insights, lifecycle (M365 + Power Platform admin centers)

---

## Official study resources

| Resource | Link |
|----------|------|
| Study guide | https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ab-900 |
| Exam sandbox | https://aka.ms/examdemo |
| Scoring | https://learn.microsoft.com/en-us/credentials/certifications/exam-scoring-reports |
| M365 docs | https://learn.microsoft.com/en-us/microsoft-365/ |
| Copilot docs | https://learn.microsoft.com/en-us/copilot/microsoft-365/ |
| Purview docs | https://learn.microsoft.com/en-us/purview/ |

---

## Topic checklist

- [ ] 01 M365 objects & admin centers
- [ ] 02 Zero Trust & security principles
- [ ] 03 Entra identity & access
- [ ] 04 Purview protection & lifecycle
- [ ] 05 Copilot data security & Graph
- [ ] 06 Governance risks & alerts
- [ ] 07 SharePoint oversharing
- [ ] 08 Copilot features & licensing
- [ ] 09 Copilot admin tasks
- [ ] 10 Agent admin lifecycle
- [ ] Reference: glossary, exam-traps, admin-centers, checklist
- [ ] Practice: Domain 1, 2, 3 + mixed mock ≥80%
