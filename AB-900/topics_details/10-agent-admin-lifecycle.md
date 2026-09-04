# 10 — Agent admin lifecycle

**Domain 3.3** · Weight **25–30%** (shared) · Skills measured as of **July 22, 2026**

---

## Official bullets covered

- Identify how to configure user access to agents
- Create an agent
- Understand the approval process for agents
- Monitor agents, including usage, operational insights, and agent lifecycle, by working with the Microsoft 365 admin center and the Microsoft Power Platform admin center

---

## Why it matters on the exam

Agent questions are a **lifecycle story**: access → create → **approve** → monitor. The classic trap is picking only one admin center. Custom/org agents often involve **both** the **Microsoft 365 admin center** (Agent Registry, requests, allow/block, inventory) and the **Power Platform admin center** (Copilot Studio environments, governance, consumption/operational analytics). Memorize the path, not marketing slogans.

---

## Core concepts

### User access to agents

Access is layered — exam items often test **which layer** is missing:

| Layer | What it controls |
|-------|------------------|
| **License / PAYG** | Entitlement to use or create (see topics 08–09) |
| **Agent allow / block / install policies** | Whether users may install org/Microsoft/partner agents |
| **Approval / publish state** | Whether a custom agent is available in Agent Store for the org |
| **Sharing / audience** | Which users/groups the agent is scoped to after publish |
| **Data permissions** | What the agent can ground on for each user (Graph/SharePoint ACLs) |
| **Power Platform environment / DLP / auth policies** | Maker restrictions, connector/auth rules for studio agents |

First-party **Researcher / Analyst** access is primarily **Copilot license + dedicated allow/block**, not the same “submit → approve → Agent Store” path as custom agents.

### Create an agent

Common creation surfaces (fundamentals level):

| Surface | Typical agent | Notes |
|---------|---------------|-------|
| **SharePoint** | Site/library-scoped agent | Create often needs Copilot license + permission to add files; use needs license or PAYG |
| **Agent Builder / Copilot experiences** | Lightweight declarative agents | Instructions + knowledge |
| **Copilot Studio** (Power Platform) | Richer custom / custom-engine agents | Environments, connectors, channels (Teams/Copilot) |

Creation ≠ organization-wide availability. Makers build and **submit**; admins **approve**.

### Approval process

High-level path for org-published agents to Microsoft Copilot / Agent Store:

```text
Maker creates agent (Studio / Builder / etc.)
        │
        ▼
Publish channel includes Microsoft Copilot / Teams as required
        │
        ▼
Submit for admin review
        │
        ▼
Microsoft 365 admin center → Agents → Requests (Agent Registry)
        │
        ├─ Publish / Approve → available in org Agent Store (scoped audience)
        └─ Reject → not available org-wide
```

Admins review capabilities, data access, and maker info before publishing. Users only get agents the org has **allowed**. Shared-by-creator agents may appear in inventory for lifecycle/block actions even when not store-published the same way — know that **admins retain block/remove** controls.

### Monitor agents (two admin centers)

| Concern | Prefer |
|---------|--------|
| Inventory, requests, publish/block, pin, availability, org agent lifecycle | **Microsoft 365 admin center** (Agents / Agent Registry / Copilot Control) |
| Copilot Studio environments, maker governance, auth policies, message/capacity consumption, studio analytics | **Power Platform admin center** |
| Adoption / top agents / credits (org insights) | **Copilot Analytics** / Agent Dashboard (overlaps topic 09) |
| Site-level SharePoint agent usage | SharePoint admin tools / audit / Cost Management (as documented) |

**Usage** — who uses which agents, volume, trends  
**Operational insights** — health, performance, satisfaction/session metrics (often Studio/Power Platform analytics)  
**Lifecycle** — draft → submitted → approved/published → updated → blocked/retired

---

## How it works

### Configure access (decision tree)

```text
Need users to use an agent?
  ├─ Licensed Copilot user? → check agent not blocked + approved/available + ACL OK
  ├─ Unlicensed? → PAYG policy covering scenario (e.g. SharePoint agents)
  └─ Still failing? → install policy, audience scope, environment DLP/auth, or pending approval
```

Admin actions mapped to outcomes:

- **Allow / deploy / pin** → increases discoverability for permitted users  
- **Block / remove** → stops use even if users previously installed  
- **Reject request** → never reaches store  
- **Scope to group** → least-privilege rollout

### Create (what exam expects you to know)

1. Choose the right builder for the scenario (SharePoint vs Studio vs lightweight builder).
2. Define **instructions**, **knowledge** sources, and any **actions/tools**.
3. Test as a user who has realistic permissions (not only Global Admin).
4. Prepare store metadata / channel settings if publishing to Copilot.
5. Submit for **admin approval** when org-wide Copilot availability is required.

### Approval (admin checklist)

In **Microsoft 365 admin center → Agents → Requests**:

- [ ] Open pending agent request  
- [ ] Review maker, description, capabilities, data access  
- [ ] **Publish/Approve** or **Reject**  
- [ ] After publish, manage availability (users/groups) and monitor  

⚠️ Approving an agent does **not** bypass Purview DLP, sensitivity labels, or SharePoint permissions for end users.

### Monitor across centers

**Microsoft 365 admin center**

- Agent inventory / registry status  
- Pending requests and publication state  
- Block unsafe or noncompliant agents  
- Org-level enablement settings  

**Power Platform admin center**

- Environment strategy for Copilot Studio  
- Capacity / PAYG message consumption for studio agents  
- Operational analytics (sessions, topics, performance)  
- Governance: connector policies, authentication requirements for agents  

Use **both** when the stem mentions lifecycle **and** studio consumption/operations.

---

## Compare / choose

### Which admin center?

| Task | Center |
|------|--------|
| Approve agent request for Agent Store | **Microsoft 365 admin center** |
| Block a published/shared agent for the tenant | **Microsoft 365 admin center** |
| Copilot Studio environment permissions / DLP for makers | **Power Platform admin center** |
| Agent message pack / PAYG consumption metrics (studio) | **Power Platform admin center** |
| Assign Copilot user licenses | **Microsoft 365 admin center** (topic 09) |
| Deep adoption dashboard | **Copilot Analytics** |

### Access vs approval vs monitoring

| Verb in stem | Likely answer theme |
|--------------|---------------------|
| “Users can’t see the agent” | Access policy, block, audience, pending approval, license/PAYG |
| “Maker finished building” | Submit for **approval** |
| “Is the agent healthy / how many sessions?” | **Monitor** (PPAC and/or Analytics) |
| “Retire / stop unsafe agent” | Block/remove lifecycle in **M365 admin center** |

### First-party vs custom lifecycle

| | Researcher / Analyst | Custom org agent |
|--|----------------------|------------------|
| Build | Microsoft | Your makers |
| Store approval | Not the same custom request path | Yes for org publish |
| Admin control | Allow/block + Copilot license | Approve, scope, block, monitor |
| Customize logic | No | Yes |

---

## ⚠️ Exam traps

1. **Approval only in Power Platform** — org Copilot Agent Store approval is **Microsoft 365 admin center** Requests.
2. **Ignoring Power Platform entirely** — studio governance and consumption live there.
3. **Assuming create = available to everyone** — missing approval/publish/audience steps.
4. **Equating Researcher with custom agents** — different control and customization model.
5. **Fixing “agent can’t read file” with approval** — that’s **permissions/ACL**, not publish state.
6. **Using Defender XDR to approve agents** — wrong center.
7. **Thinking PAYG approval replaces agent approval** — billing entitlement ≠ content/security review of an agent package.
8. **Single-center monitoring answer when stem cites both usage and studio ops** — expect **M365 + Power Platform**.

---

## Hands-on checklist

- [ ] M365 admin center: open **Agents** inventory; note statuses (available, blocked, requested)
- [ ] Submit a test custom agent for Copilot channel; process **Approve** and **Reject** once each in a lab
- [ ] Scope an approved agent to a security group; verify a non-member cannot use it
- [ ] Block an agent; confirm it disappears/stops for users
- [ ] Power Platform admin center: locate Copilot Studio environments and capacity/analytics
- [ ] Compare SharePoint agent create vs use requirements (license vs PAYG)
- [ ] Open Copilot Analytics / Agent Dashboard (if eligible) for top agents / credits
- [ ] Trace one agent from create → request → publish → usage metric end-to-end

---

## Checkpoint

1. Where does an admin approve a custom agent for the org Agent Store?
2. Name one monitoring concern that typically belongs in Power Platform admin center.
3. A maker created an agent but users don’t see it in Copilot. What step is likely missing?
4. Does approving an agent grant users access to SharePoint files they couldn’t open before?
5. Which two admin centers does the official skill bullet name for monitoring agents?

### Answers

1. **Microsoft 365 admin center** → Agents → **Requests** (publish/approve or reject).
2. Examples: **Copilot Studio capacity/consumption**, environment governance, studio **operational analytics**, agent auth policies.
3. **Admin approval / publish** (or audience/install policy still blocking).
4. **No** — permissions still apply per user.
5. **Microsoft 365 admin center** and **Microsoft Power Platform admin center**.

---

## Learn links

- [Manage agents in the Microsoft 365 admin center](https://learn.microsoft.com/en-us/microsoft-365/admin/manage/manage-copilot-agents-integrated-apps)
- [Agents admin guide for Microsoft 365](https://learn.microsoft.com/en-us/microsoft-365/copilot/agent-essentials/m365-agents-admin-guide)
- [Agent Store in Microsoft Copilot](https://learn.microsoft.com/en-us/microsoft-365/copilot/copilot-agent-store)
- [Get started with agents in SharePoint](https://learn.microsoft.com/en-us/sharepoint/get-started-sharepoint-agents)
- [Microsoft Copilot reports for IT admins](https://learn.microsoft.com/en-us/microsoft-365/copilot/microsoft-365-copilot-reports-for-admins)
- Power Platform admin / Copilot Studio governance — verify current docs on Microsoft Learn
- [AB-900 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ab-900)
