# AB-900 Exam traps

Cross-topic gotchas for **Exam AB-900** (skills as of **July 22, 2026**). Unofficial study aid — not brain dumps.

Read the night before; pair with [checklist.md](./checklist.md) and [admin-centers-cheatsheet.md](./admin-centers-cheatsheet.md).

---

## Copilot data access & Graph

1. **Permissions follow the user.** Copilot answers using the signed-in user’s access via **Microsoft Graph**. It does **not** become a super-user.
2. **Copilot does not bypass ACL.** If the user cannot open the file in SharePoint/OneDrive/mail, Copilot should not surface that content as authorized work data.
3. **License ≠ access to content.** Assigning Microsoft 365 Copilot enables the AI feature; site/library permissions still gate grounding.
4. **Graph grounding ≠ web search.** Work grounding uses Graph/connectors; web is a separate admin-controllable capability.

---

## Purview & governance

5. **Oversharing ≠ malware.** Broad “Everyone” links and loose SharePoint permissions are a **governance** problem (DAG reports, Advanced Management / RAC) — not primarily Defender XDR malware detection.
6. **Labels vs DLP.** Sensitivity labels classify/protect; DLP policies detect and constrain risky sharing/exfil. Scenarios often include both, but the **first tool** in the stem matters.
7. **Retention ≠ sensitivity label.** Retention/DLM answers “how long to keep/delete”; labels answer “how sensitive / how protected.”
8. **DSPM for AI ≠ generic DLP only.** DSPM for AI discovers/manages **AI activity and posture**. Do not pick “create a DLP policy” as the only DSPM answer unless the stem is clearly about DLP alerts.
9. **IRM vs Communication Compliance vs DLP.** People-risk behaviors (IRM), communication conduct/policy violations (Comm Compliance), sensitive data movement (DLP) — match the symptom.
10. **Compliance Manager ≠ eDiscovery.** Compliance Manager = posture/recommendations; Content search / eDiscovery = find specific files/emails.

---

## Identity & security

11. **PIM ≠ MFA for all users.** PIM = just-in-time **privileged** roles. Day-to-day MFA for the workforce is usually **Conditional Access** + authentication methods.
12. **Authentication vs authorization.** MFA proves identity; roles/CA/grants decide access.
13. **SSO is not Conditional Access.** SSO reduces sign-in friction across apps; CA enforces conditions/controls.
14. **App registrations ≠ Enterprise apps (interchangeable).** Related but different Entra objects — registration defines the app; enterprise app is the tenant’s instance/assignments.
15. **Identity Secure Score ≠ Defender Secure Score only.** Identity Secure Score lives in **Entra** improvement actions for identity posture.
16. **Zero Trust ≠ “buy one product.”** Principles: verify explicitly, least privilege, assume breach — implemented with many controls.

---

## Admin center selection

17. **Pick the correct admin center.** Mailboxes/DGs → Exchange; sites/libraries → SharePoint; teams/channels/policies → Teams; users/CA/PIM/apps → Entra; labels/DLP/IRM/DSPM/search → Purview; threats → Defender; Copilot licenses/agent approval → M365 admin; Studio capacity/maker governance → **Power Platform**.
18. **Agent approval path.** Custom agents submitted to Copilot typically need **M365 admin center → Agents → Requests** approve/publish — not Defender, not “Exchange policy.”
19. **Monitoring agents can need two centers.** Inventory/approval/lifecycle → **M365**; studio consumption/ops → **Power Platform**. Stem saying both is a hint.
20. **Copilot Analytics ≠ license assignment.** Analytics measures adoption/impact; licenses are assigned in **M365 admin center**.

---

## Copilot features, licensing, agents

21. **Researcher / Analyst / custom are not interchangeable.** Researcher = deep research + citations; Analyst = data/Excel-style analysis; custom = org-specific instructions/knowledge.
22. **Disabling “agents” does not automatically remove Researcher/Analyst** from core Copilot Tools — they have dedicated controls.
23. **Monthly license vs PAYG.** Seats for Copilot productivity features; PAYG meters eligible agent usage (esp. SharePoint agents for unlicensed users). PAYG is not a full silent replacement for every licensed Copilot capability.
24. **Create vs use (SharePoint agents).** Creating usually needs a Copilot license; using can be license **or** PAYG.
25. **Create ≠ approved for org.** Maker build still needs **approval/publish/audience** for store-wide Copilot availability.
26. **Approving an agent does not widen file ACLs.** Users still only ground on what they can access.

---

## Prompt & adoption traps

27. **Deleting prompts does not revoke Copilot.** Use license removal, feature policy, or agent block.
28. **Audit log is not an adoption dashboard.** Use M365 reports / Copilot Analytics for adoption; Purview audit for investigations.
29. **High PAYG spend** → billing policy limits/scope (or seats for heavy users) — not “turn off Conditional Access.”

---

## If you remember only ten

1. Copilot **respects existing permissions** (Graph).  
2. Oversharing → **SharePoint governance** (DAG / Advanced Management / RAC).  
3. Labels ≠ DLP ≠ retention ≠ DSPM for AI.  
4. **PIM** = privileged JIT; **CA/MFA** = workforce access controls.  
5. Right **admin center** wins many items.  
6. Agents: access → create → **approve** → monitor (**M365 + Power Platform**).  
7. Researcher ≠ Analyst ≠ custom.  
8. License ≠ content ACL; PAYG ≠ full seat substitute.  
9. DSPM for AI is about **AI posture/activity**, not “DLP only.”  
10. Responsible AI / human accountability still applies — Copilot assists; org controls and humans own outcomes.
