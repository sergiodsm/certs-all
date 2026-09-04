# 08 — Copilot features & licensing

**Domain 3.1** · Weight **25–30%** (shared) · Skills measured as of **July 22, 2026**

---

## Official bullets covered

- Compare the built-in capabilities of Copilot and agents
- Compare Copilot monthly license model to pay-as-you-go, including SharePoint
- Identify which Copilot features can be enabled or disabled
- Identify use cases for Researcher
- Identify use cases for Analyst
- Identify use cases for custom agents

---

## Why it matters on the exam

Domain 3 scenarios often start with “which capability / which billing model / which agent?” Getting this map wrong cascades into wrong admin-center answers later. Treat **Copilot (licensed work AI)** and **agents (task/specialized extensions)** as related but not interchangeable. Know when a monthly seat license is required versus when **pay-as-you-go (PAYG)** covers unlicensed usage (especially SharePoint agents).

---

## Core concepts

### Microsoft 365 Copilot (work-grounded AI)

- Combines LLMs with **Microsoft Graph** and the user’s existing M365 content (mail, files, chats, meetings, calendar — subject to permissions).
- Surfaces in **Word, Excel, PowerPoint, Outlook, Teams, OneNote**, and the Microsoft 365 Copilot app / Copilot Chat (work mode).
- Does **not** grant new permissions. Answers reflect what the signed-in user can already access.
- Typically requires a **Microsoft 365 Copilot add-on license** on top of an eligible base plan (e.g. Microsoft 365 E3/E5 or Business Standard/Premium — verify current prerequisites on Learn).

### Agents

- **Agents** extend Copilot with focused instructions, knowledge sources, and skills/actions for a scenario (site Q&A, process helper, department bot, research/analysis workflows).
- Categories exam expects you to distinguish:
  - **Microsoft first-party agents** such as **Researcher** and **Analyst** (core Copilot experiences / Tools — not the same as org-built custom agents).
  - **Custom agents** built by your org (Agent Builder, Copilot Studio, SharePoint agents, etc.).
  - Partner / store / Frontier agents (admin may allow, block, or approve).
- Agents still respect **user permissions** to grounding data.

### Researcher

- Deep, **multi-step research** assistant for complex questions.
- Grounds on work data (Graph / connectors) and, if enabled, web (Bing); produces structured findings with **citations**.
- Best for: competitive/landscape research, synthesizing many sources, long-form investigative answers — **not** spreadsheet modeling.
- Admin note: part of the licensed Copilot experience under Tools; can be blocked by admins but is **not** managed like every custom Agent Store submission. Users typically cannot unpin/disable it themselves.

### Analyst

- Data/analysis-oriented agent — strongest fit for **Excel / tabular / quantitative** work: explore datasets, build analysis steps, explain trends.
- Best for: “analyze this workbook,” “find outliers,” “summarize metrics” — **not** multi-document literature-style research (that’s Researcher).

### Custom agents

- Org-defined agents with instructions + knowledge (SharePoint/OneDrive/sites, connectors, tools) for a **specific business scenario**.
- Created via experiences such as **Copilot Studio**, **Agent Builder**, or **SharePoint agents** on eligible sites.
- Usually enter an **admin approval / publish** path before broad org availability (see topic 10).
- Use when you need a repeatable specialist (HR policy helper, project-site bot, onboarding guide) rather than general Copilot Chat.

---

## How it works

### Copilot vs agents (admin reasoning)

```text
User asks a question
        │
        ├─ General work productivity → Microsoft 365 Copilot (apps + Chat)
        │     Grounding: Graph + user permissions
        │
        └─ Specialized / multi-step / scoped scenario → Agent
              ├─ Researcher  → deep research + citations
              ├─ Analyst     → data / Excel-style analysis
              └─ Custom      → org instructions + knowledge + skills
```

1. Confirm the user has the right **entitlement** (Copilot license and/or PAYG policy covering the scenario).
2. Confirm the feature/agent is **allowed** (tenant feature toggles, agent settings, approval state).
3. Confirm **data access** is correct (site permissions, labels, DLP) — licensing never overrides ACL.

### Monthly license vs pay-as-you-go (including SharePoint)

| Model | What it is | Typical use | Exam cue |
|-------|------------|-------------|----------|
| **Monthly Copilot license** | Per-user seat add-on | Full work Copilot in apps + Graph grounding; first-party agents like Researcher/Analyst for licensed users | “Assign licenses to users/groups”; predictable per-seat cost |
| **Pay-as-you-go (PAYG)** | Metered Azure billing for eligible agent / chat consumption | Unlicensed users using **SharePoint agents** (and related metered agent usage); variable cost | “Azure subscription + billing policy”; spending limits; Cost Management |
| **Neither** | No seat, no PAYG | User **cannot** create/use the covered agents | Both license and PAYG off → no access |

**SharePoint agents (high-yield):**

| Copilot licensed? | PAYG enabled? | Result |
|-------------------|---------------|--------|
| No | No | Cannot create or use SharePoint agents |
| No | Yes | Unlicensed users can **use** agents; billed PAYG |
| Yes | No | Licensed users can **create and use**; unlicensed cannot |
| Yes | Yes | Licensed create/use; unlicensed use via PAYG |

Admin setup for PAYG typically needs: **Azure subscription** (Owner/Contributor), resource linkage, and a **billing policy** configured from the **Microsoft 365 admin center** (Copilot cost / billing experiences). Monitor spend in Azure Cost Management / admin reporting.

### Features admins can enable or disable (conceptual map)

Exact UI labels evolve — exam cares about **what class of control** exists:

| Control area | Examples of what admins govern | Where (conceptually) |
|--------------|--------------------------------|----------------------|
| Copilot feature toggles | Web grounding / web search, selected Copilot capabilities | Microsoft 365 admin center (Copilot / org settings) |
| First-party agents | Block/allow **Researcher** / **Analyst** (separate from “disable all agents”) | M365 admin center agent / Copilot Control settings |
| Custom & store agents | Allow install, pin, block, approve requests | Agent Registry / Agents blade |
| Connector / Graph grounding | Which connectors feed Copilot | Admin connector / Graph connector governance |
| Data protection overlays | Labels, DLP, IRM still apply — not “Copilot-only switches” | Purview / Defender |

⚠️ Disabling “agents” broadly does **not** automatically remove Researcher/Analyst from the core Copilot Tools experience; they have **dedicated** block/allow controls.

---

## Compare / choose

### Copilot vs agents

| Dimension | Microsoft 365 Copilot | Agents |
|-----------|----------------------|--------|
| Primary job | Broad productivity AI across apps & Chat | Focused scenarios / skills / workflows |
| Grounding | Graph + user context | Same permission model; plus agent knowledge/tools |
| Admin lifecycle | License + feature policies | Access → create → **approval** → monitor (custom) |
| Example | Draft email, summarize meeting, rewrite doc | Researcher report; Analyst on a table; site FAQ agent |

### Researcher vs Analyst vs custom

| Need | Pick |
|------|------|
| Multi-source investigation with citations | **Researcher** |
| Spreadsheet / quantitative analysis | **Analyst** |
| Department/process bot with org knowledge | **Custom agent** |
| Everyday mail/doc/meeting help | **Copilot** (apps/Chat), not a specialist agent |

### License vs PAYG

| Need | Pick |
|------|------|
| Daily Copilot in Word/Excel/Teams for named users | **Monthly license** |
| Occasional SharePoint agent use by people without Copilot seats | **PAYG** |
| Cap spend for unlicensed agent usage | PAYG **billing policy** + limits/alerts |
| Zero agent access for everyone | No license assignment **and** PAYG not enabled |

---

## ⚠️ Exam traps

1. **Treating Researcher / Analyst / custom as interchangeable** — wrong use case = wrong answer.
2. **Assuming PAYG replaces Copilot seats for full app Copilot** — PAYG is consumption for eligible agent/chat scenarios (esp. SharePoint agents), not a full substitute for every licensed Copilot feature.
3. **Thinking “agents disabled” hides Researcher/Analyst** — they are core Copilot Tools experiences with separate controls.
4. **Believing a license grants content access** — licensing enables the feature; **permissions** still gate data.
5. **Confusing create vs use for SharePoint agents** — creating typically needs Copilot license + ability to add files; use can be license **or** PAYG.
6. **Picking Defender for “enable Copilot feature”** — feature enablement is an **M365 Copilot / admin center** task, not XDR.
7. **Assuming custom agents skip approval** — org-published agents generally need admin review before store-wide availability.

---

## Hands-on checklist

In a lab tenant (if available):

- [ ] Confirm eligible base + Copilot SKU prerequisites on Learn for your tenant type
- [ ] In **Microsoft 365 admin center**, open Copilot / Agents settings; note which features can be toggled
- [ ] Locate controls for **Researcher** / **Analyst** allow/block
- [ ] Review SharePoint agent docs: license-only vs PAYG matrix
- [ ] If permitted: link an Azure subscription and create a **PAYG billing policy**; set a low spending limit
- [ ] Invoke Copilot Chat → Tools: open **Researcher** vs **Analyst**; note different intents
- [ ] Create a simple **SharePoint** or Agent Builder custom agent on a test site (publish later in topic 10)

---

## Checkpoint

1. A user without a Copilot license needs to chat with a SharePoint site agent. What else must be true?
2. Deep multi-document investigation with citations — Researcher, Analyst, or custom?
3. Admin disables agents org-wide. Do Researcher and Analyst automatically disappear?
4. True or false: Assigning a Copilot license lets the user see files they previously could not open.
5. When do you choose PAYG over buying seats for everyone?

### Answers

1. **PAYG billing** must be enabled for SharePoint agents (Azure + billing policy). License **or** PAYG is required for use.
2. **Researcher**.
3. **No** — they are core Copilot Tools experiences; use dedicated block/allow settings.
4. **False** — Copilot respects existing permissions/ACLs.
5. When **unlicensed / occasional** agent usage (e.g. SharePoint agents) should be metered instead of full monthly seats for all users.

---

## Learn links

- [Study guide for Exam AB-900](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ab-900)
- [Microsoft 365 Copilot documentation](https://learn.microsoft.com/en-us/copilot/microsoft-365/)
- [Get started with agents in SharePoint](https://learn.microsoft.com/en-us/sharepoint/get-started-sharepoint-agents)
- [Manage agents in the Microsoft 365 admin center](https://learn.microsoft.com/en-us/microsoft-365/admin/manage/manage-copilot-agents-integrated-apps)
- [Researcher agent FAQ](https://learn.microsoft.com/en-us/microsoft-365/copilot/faq-researcher)
- [Agents admin guide for Microsoft 365](https://learn.microsoft.com/en-us/microsoft-365/copilot/agent-essentials/m365-agents-admin-guide)
- Verify current licensing/PAYG meters on Microsoft Learn before exam day (SKUs and meters change).
