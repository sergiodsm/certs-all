# 09 — Copilot admin tasks

**Domain 3.2** · Weight **25–30%** (shared) · Skills measured as of **July 22, 2026**

---

## Official bullets covered

- Assign Copilot licenses
- Monitor and manage Copilot pay-as-you-go billing policies
- Monitor Copilot usage and adoption, including Copilot Analytics and the Microsoft 365 admin center
- Manage prompts, including saving, sharing, scheduling, and deleting

---

## Why it matters on the exam

This skill area is **procedural**: which portal, which object, which action. Expect scenarios like “assign Copilot to a group,” “cap PAYG spend,” “show adoption,” or “share a saved prompt.” Success = naming the right **admin center / analytics surface** and the right lifecycle action for licenses, billing, usage, and prompts.

---

## Core concepts

### Assign Copilot licenses

- Copilot is an **add-on license** assigned to **users** (and commonly via **groups**) in the **Microsoft 365 admin center**.
- Assignment alone is not a full rollout: users still need eligible base licenses, client readiness, and correct data permissions.
- Typical admin path: **Billing → Licenses** (or Users → Licenses) / Copilot setup guidance → assign to users or security/Microsoft 365 groups.
- Group-based licensing (Entra) is a valid enterprise pattern when available — exam cares that **licenses gate feature access**, not that you memorize every SKU ID.

### PAYG billing policies

- **Pay-as-you-go** meters eligible agent/chat consumption (notably **SharePoint agents** for unlicensed users) against an **Azure subscription**.
- Admins create and manage **billing policies**: which Azure subscription/resource, which users/groups are covered, spending limits / budgets / alerts.
- Without a valid policy + Azure linkage, unlicensed PAYG usage does not work.
- Monitor cost in **Microsoft 365 admin center** Copilot cost experiences and **Azure Cost Management**.

### Usage and adoption monitoring

Two complementary surfaces (do not collapse them into one):

| Surface | Focus | Typical audience |
|---------|--------|------------------|
| **Microsoft 365 admin center** reports | License readiness, basic Copilot usage/adoption metrics, admin operational view | IT admins |
| **Copilot Analytics** (Viva Insights Copilot Dashboard / related insights) | Deeper adoption, impact, agent/credit insights, org/team views | AI admins, leaders, delegated analysts |

Also related (not substitutes for “adoption dashboard”):

- **Purview audit logs** — activity for compliance/security investigation
- **Power Platform admin center** — agent consumption / studio analytics (more topic 10)

### Prompt management

Users (and org galleries) work with prompts in Copilot **Prompt Gallery** / prompt experiences:

| Action | Meaning |
|--------|---------|
| **Save** | Persist a useful prompt for reuse (user / library collection) |
| **Share** | Make a prompt available to a team or colleagues |
| **Schedule** | Run / trigger a prompt on a schedule (automation-style reuse — verify UI name in tenant; exam lists scheduling as in-scope) |
| **Delete** | Remove a saved/shared prompt you own or administer per policy |

Admins may track engagement with saved/liked/shared prompts via available analytics; day-to-day save/share/delete is primarily a **user productivity** skill that admins must **understand and support**.

---

## How it works

### Assign licenses (admin flow)

```text
1. Confirm eligible base Microsoft 365 license on the user
2. Purchase / provision Microsoft 365 Copilot seats
3. Microsoft 365 admin center → assign license to user or group
4. Allow replication; user signs in to Copilot-enabled apps
5. Validate: app shows Copilot; Graph grounding respects permissions
```

Troubleshooting cues:

- License assigned but feature missing → client channel, app version, feature policy, or replication delay
- Feature present but “no useful work data” → permissions / oversharing / empty Graph context — **not** a license bug

### Manage PAYG billing policies

```text
1. Azure subscription with Owner/Contributor for setup admin
2. M365 admin center → Copilot cost / billing → create billing policy
3. Bind subscription / resource; scope users or groups
4. Set monthly spend limit / alerts
5. Monitor consumption; adjust scope or disable policy if needed
```

Policy management actions exam may imply: **create, scope, monitor, limit, revise, disable**.

### Monitor usage & adoption

**Microsoft 365 admin center**

- Copilot usage / adoption reports (active users, app usage patterns as available)
- License assignment vs utilization (seats purchased vs used)

**Copilot Analytics**

- Copilot Dashboard: readiness recommendations, adoption trends, impact-oriented insights
- Agent-related views / credit usage where licensed thresholds apply
- Delegation: leaders/analysts can receive dashboard access without Global Admin

Pick the surface from the stem:

- “Are licenses being used?” → **M365 admin center** reports
- “Business impact / adoption deep dive / dashboard for leaders” → **Copilot Analytics**
- “Who prompted what for investigation?” → **Purview audit** (governance domain overlap)

### Manage prompts

```text
User crafts effective prompt
  → Save to personal / gallery collection
  → Share with team (consistency)
  → Schedule recurring use when supported
  → Delete obsolete prompts to reduce clutter / risk of outdated instructions
```

Admin coaching angle: shared prompts improve adoption quality; stale shared prompts are a **governance hygiene** issue (wrong process guidance), not malware.

---

## Compare / choose

| Task | Primary place |
|------|----------------|
| Assign / remove Copilot license | **Microsoft 365 admin center** |
| PAYG billing policy & spend controls | **M365 admin center** (+ Azure subscription / Cost Management) |
| Basic usage & license adoption | **M365 admin center** reports |
| Rich Copilot Analytics / impact dashboard | **Copilot Analytics** (Viva Insights Copilot Dashboard) |
| Save / share / schedule / delete prompts | Copilot **Prompt Gallery** / prompt UX (user); analytics may report engagement |
| Agent message packs / studio consumption | **Power Platform admin center** (see topic 10) |

| Signal | Interpret as |
|--------|----------------|
| High license count, low active use | Adoption problem → Analytics + enablement, not “buy more seats” |
| Spiking PAYG cost | Billing policy limits / restrict unlicensed agent use / consider seats for heavy users |
| Great adoption, DLP alerts rising | Governance/oversharing — not a licensing failure |

---

## ⚠️ Exam traps

1. **Sending license assignment to Entra “Enterprise apps”** — licenses are M365 admin / billing assignments (Enterprise apps = app identity objects).
2. **Using Copilot Analytics to assign seats** — Analytics measures; **admin center** assigns.
3. **Ignoring Azure for PAYG** — PAYG needs an Azure subscription behind the billing policy.
4. **Equating audit logs with adoption dashboards** — audit = investigation; Analytics/admin reports = adoption.
5. **Thinking admins author every prompt** — users save/share; admins enable measurement and governance culture.
6. **Deleting a prompt to “revoke Copilot”** — wrong control; use **license / feature / agent policy**.
7. **PAYG policy = sensitivity label** — unrelated; billing ≠ data classification.

---

## Hands-on checklist

- [ ] Assign Copilot to a test user; confirm appearance in Word/Teams/Copilot app
- [ ] Assign via a **group**; add/remove member and observe license effect
- [ ] Open M365 admin center Copilot **usage/adoption** reports
- [ ] Open **Copilot Dashboard** / Copilot Analytics (if tenant eligible); note readiness tips
- [ ] Create or review a **PAYG billing policy**; set a low cap; generate a test SharePoint agent interaction if allowed
- [ ] In Copilot: **save** a prompt, **share** to a team, **schedule** if available, then **delete**
- [ ] Find where prompt engagement or Copilot activity appears in admin/analytics docs for your tenant

---

## Checkpoint

1. Where do you assign Microsoft 365 Copilot licenses?
2. What cloud resource is required before PAYG SharePoint agent billing works?
3. Leader wants impact/adoption insights beyond basic admin charts — which surface?
4. List the four prompt management actions named in the skills outline.
5. Seats are assigned but PAYG spend is climbing for unlicensed SharePoint agent users. What do you adjust first?

### Answers

1. **Microsoft 365 admin center** (user/group license assignment).
2. An **Azure subscription** (linked via a billing policy).
3. **Copilot Analytics** (Copilot Dashboard / Viva Insights analytics).
4. **Save, share, schedule, delete**.
5. The **PAYG billing policy** (limits, scope, alerts) — and/or reduce unlicensed agent use; heavy users may need seats.

---

## Learn links

- [Assign licenses in the Microsoft 365 admin center](https://learn.microsoft.com/en-us/microsoft-365/admin/manage/assign-licenses-to-users) — verify on Learn
- [Microsoft Copilot reports for IT admins](https://learn.microsoft.com/en-us/microsoft-365/copilot/microsoft-365-copilot-reports-for-admins)
- [Microsoft Copilot Dashboard](https://learn.microsoft.com/en-us/viva/insights/org-team-insights/copilot-dashboard)
- [Prompt Gallery in Copilot](https://learn.microsoft.com/en-us/microsoft-365/copilot/copilot-prompt-gallery)
- [Get started with agents in SharePoint (PAYG)](https://learn.microsoft.com/en-us/sharepoint/get-started-sharepoint-agents)
- [AB-900 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ab-900)
