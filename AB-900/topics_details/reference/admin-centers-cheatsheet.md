# AB-900 Admin centers cheatsheet

Which object or task lives where. Fundamentals map for **Exam AB-900** (skills as of **July 22, 2026**). UI names shift; reason by **workload ownership**.

---

## Quick matrix

| Need to… | Admin center |
|----------|----------------|
| Domains, org settings, billing, **assign Copilot licenses**, Copilot feature/agent inventory & **approvals**, basic Copilot usage reports, PAYG billing policy entry | **Microsoft 365 admin center** |
| Mailboxes, distribution groups, mail flow (as in-scope) | **Exchange admin center** |
| Sites, libraries, folders, sharing/oversharing tools, DAG reports, Advanced Management / RAC | **SharePoint admin center** |
| Teams, channels, Teams policies | **Teams admin center** |
| Users, groups, Conditional Access, SSO apps, MFA registration, risky sign-ins, Identity Secure Score, audit/sign-in logs, **PIM**, App registrations, Enterprise apps | **Microsoft Entra admin center** |
| Information Protection, DLP, IRM, Communication Compliance, DSPM for AI, DLM/retention, sensitivity labels, classification, Compliance Manager, Data Explorer, activity explorer, Content search | **Microsoft Purview** portal |
| Threat protection / XDR incidents, hunting across security workloads | **Microsoft Defender** portal |
| Copilot Studio environments, maker governance, agent auth/DLP for studio, capacity / message consumption, studio operational analytics | **Power Platform admin center** |
| Deep Copilot adoption / impact / Agent Dashboard insights | **Copilot Analytics** (Viva Insights Copilot Dashboard) — often linked from M365/AI admin experiences |
| Azure subscription spend for PAYG meters | **Azure** Cost Management (+ policy created from M365) |

---

## Microsoft 365 admin center

| Objects / tasks |
|-----------------|
| Domain names, org profile/settings |
| User list shortcuts, roles (high-level) |
| **License assignment** (including Microsoft 365 Copilot) |
| Copilot setup guidance |
| **Agents** / Agent Registry: inventory, **requests/approval**, allow/block, pin |
| Copilot feature settings (enable/disable capabilities as exposed) |
| PAYG / Copilot **billing policies** (link Azure) |
| Basic Copilot **usage/adoption** reports |
| Integrated apps / org-level app settings (as applicable) |

---

## Exchange admin center

| Objects / tasks |
|-----------------|
| Mailboxes |
| Distribution groups / mail-enabled groups (as scoped on exam) |
| Mailbox permissions / recipient management fundamentals |

*Not* the home for SharePoint libraries, Teams policies, or Purview DLP authoring.

---

## SharePoint admin center

| Objects / tasks |
|-----------------|
| Site collections / sites |
| Libraries & folder governance (admin view) |
| Site roles & permission models (Owner/Member/Visitor patterns) |
| Sharing settings / oversharing troubleshooting entry points |
| **Data access governance (DAG) reports** |
| **SharePoint Advanced Management**, including **restricted access control (RAC)** |
| SharePoint agent admin considerations (usage monitoring hooks per docs) |

---

## Teams admin center

| Objects / tasks |
|-----------------|
| Teams & team settings |
| Channels |
| Teams **policies** (messaging, meeting, app, etc.) |

Copilot *in* Teams still depends on **licenses + Graph permissions**; policy work for the Teams workload lives here.

---

## Microsoft Entra admin center

| Objects / tasks |
|-----------------|
| Users & groups (security objects) |
| **Conditional Access** |
| Authentication methods / MFA |
| **SSO** enterprise configuration |
| Risky sign-ins / Identity Protection signals (as available) |
| **Identity Secure Score** |
| Sign-in & audit logs for identity |
| **Privileged Identity Management (PIM)** |
| **App registrations** |
| **Enterprise applications** |

---

## Microsoft Purview

| Objects / tasks |
|-----------------|
| **Information Protection** / sensitivity labels |
| Data classification |
| **DLP** policies & alerts |
| **Insider Risk Management** |
| **Communication Compliance** |
| **DSPM for AI** |
| **Data Lifecycle Management** / retention |
| **Compliance Manager** |
| **Data Explorer** |
| **Activity explorer** |
| **Content search** (eDiscovery) |

---

## Microsoft Defender (XDR)

| Objects / tasks |
|-----------------|
| Threat protection & intelligence views |
| Incidents/alerts across Defender workloads |
| Correlation of identity/email/endpoint/cloud signals |

Use for **threat** scenarios — not SharePoint oversharing governance and not agent store approval.

---

## Power Platform admin center

| Objects / tasks |
|-----------------|
| Environments for **Copilot Studio** |
| Maker / environment security |
| Agent **authentication** / connector governance policies |
| Capacity, **PAYG/message pack consumption** for studio agents |
| Operational insights / analytics for custom engine agents |

Pair with **M365 admin center** for full agent lifecycle (approval + ops).

---

## Scenario → center drill

| Scenario | Go to |
|----------|-------|
| User needs Copilot license | M365 admin center |
| Cap unlicensed SharePoint agent spend | M365 billing policy + Azure Cost Management |
| Approve custom agent for Agent Store | M365 admin center → Agents → Requests |
| Studio agent burning message capacity | Power Platform admin center |
| DLP alert on sensitive sharing | Purview |
| AI usage posture across org | Purview **DSPM for AI** |
| EveryoneExceptExternal link sprawl | SharePoint (DAG / Advanced Management / RAC) |
| Require MFA for all users from untrusted locations | Entra Conditional Access |
| JIT Global Admin activation | Entra PIM |
| Mailbox for new hire | Exchange |
| New team + channel policy | Teams |
| Suspected malware campaign | Defender XDR |
| Leader wants Copilot adoption impact | Copilot Analytics |
| Search mail/files for legal hold prep | Purview Content search |

---

## Related reference

- [glossary.md](./glossary.md)
- [exam-traps.md](./exam-traps.md)
- [checklist.md](./checklist.md)
