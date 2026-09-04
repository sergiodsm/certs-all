# 05 — Copilot data security & Microsoft Graph

**Exam:** AB-900 · Domain 2 (35–40%) · Skill **2.2 Understand data security implications of Copilot**  
**Skills measured as of:** July 22, 2026  

---

## 1. Official bullets covered

- Understand **how Copilot accesses data**
- Understand how **Microsoft Graph** influences Copilot responses
- Understand how Copilot uses **permissions and other controls** in Microsoft 365, Microsoft Purview, and Microsoft Defender to protect against risks
- Understand **responsible AI** principles

---

## 2. Why it matters on the exam

This is the conceptual heart of Domain 2. Most wrong answers assume Copilot is a “superuser” that can read the whole tenant. **It is not.** Copilot grounds answers in content the **signed-in user** can already access via Microsoft Graph and existing ACLs. Bad permissions → bad Copilot answers. Purview and Defender add extra gates; they don’t invent a parallel permission model.

---

## 3. Core concepts

### How Copilot accesses data

1. User signs in with their Microsoft 365 identity.  
2. User prompts Copilot.  
3. Copilot’s grounding layer retrieves **organizational content the user is already allowed to open** (mail, files, chats, meetings, etc.).  
4. That permitted content is passed as context to the model.  
5. Response cites / summarizes only what the user could have found manually (faster).

**Hard rule for the exam:**  
> Copilot does **not** bypass ACLs. If the user cannot open it in SharePoint/Outlook/Teams, Copilot must not return it to that user.

Microsoft’s Purview guidance: AI apps Purview supports use existing controls so tenant data is **never returned to the user or used by the LLM** if the user lacks access.

### Microsoft Graph influence

- **Microsoft Graph** is the API layer over Microsoft 365 data (users, files, mail, calendar, Teams, etc.).  
- Copilot uses Graph (and related grounding services) to **find and retrieve permitted content** that shapes the answer.  
- Graph does not grant new rights — it **honors the same permissions** the user has in the workload.  
- Quality of Graph-accessible data (well governed, correctly shared, labelled) → quality and safety of Copilot answers.

Think: **Graph = permitted org context; LLM = language; permissions = boundary.**

### Permissions & controls (three planes)

| Plane | What it does for Copilot risk |
|-------|-------------------------------|
| **Microsoft 365** | Site/library/folder permissions, sharing links, Teams membership, mailbox ACL — **primary gate** |
| **Microsoft Purview** | Sensitivity labels (encryption/usage rights), DLP (incl. Copilot location), IRM, Communication Compliance, DSPM for AI, retention, audit |
| **Microsoft Defender** | Threat protection (malware, phishing, XDR signals) — protects against **malicious** content/activity, not “oversharing governance” by itself |

### Extra gates beyond ACLs

- **Sensitivity label encryption:** needs appropriate usage rights (typically **VIEW + EXTRACT** for AI to return content).  
- **DLP for Copilot:** can block processing of items with specific labels / sensitive info.  
- **S/MIME protected email:** not returned by Copilot; Copilot unavailable in Outlook when an S/MIME message is open.  
- **Password-protected documents:** generally not accessible to AI apps unless already opened by the user in the same app (data in use).  
- **Labels for SharePoint/OneDrive** should be enabled so encrypted files are handled correctly beyond local Office “in use” scenarios.

### Responsible AI principles (admin view)

Microsoft’s responsible AI themes you’ll see in fundamentals material include:

- **Fairness** — avoid unfair outcomes  
- **Reliability & safety** — systems behave as expected; fail safely  
- **Privacy & security** — protect data; honor access controls  
- **Inclusiveness** — accessible to diverse users  
- **Transparency** — users understand AI is involved; citations help  
- **Accountability** — humans govern deployment, monitoring, and remediation  

For AB-900, map responsible AI to **admin actions**: least privilege, Purview controls, oversharing remediation, monitoring with DSPM/audit, human review of risky AI usage — not “turn off all security to make Copilot smarter.”

---

## 4. How it works (admin reasoning)

### Grounding flow (exam mental model)

```text
User prompt
    → Identity (Entra)
    → Graph retrieves only ACL-permitted content (+ label/DLP filters)
    → Model generates grounded response + citations
    → Audit / Purview can record interaction (when configured)
```

### Why oversharing becomes an AI problem

- Before Copilot: over-permissioned files were often **hard to discover**.  
- With Copilot: natural language **surfaces** those files instantly for anyone who already had access.  
- Copilot **amplifies** oversharing; it does not create new permissions.  
→ Fix SharePoint/OneDrive permissions and Purview controls (topics 04, 06, 07) — don’t blame Defender malware detection.

### Controls checklist when “Copilot showed a secret file”

1. Did the user already have permission? (M365 ACL / sharing link / group)  
2. Was the file labelled/encrypted? Did they have EXTRACT?  
3. Is there a DLP-for-Copilot policy that should have blocked it?  
4. Is the site a candidate for DAG report / Restricted Access Control / Restricted Content Discovery? (topic 07)  
5. Is this a threat (malware) or a **governance** issue? Usually governance.

### Responsible AI in operations

- Deploy with **least privilege** and sensitivity labels before broad Copilot rollout  
- Monitor AI activity (DSPM for AI, audit)  
- Use Communication Compliance / IRM for misuse  
- Keep humans accountable for agent approval and data governance (Domain 3)

---

## 5. Compare / choose

### What limits Copilot vs what finds threats

| Scenario | Primary control plane |
|----------|----------------------|
| User sees a salary file they shouldn’t | **M365 permissions / oversharing** (SharePoint) |
| User has access but must not summarize Highly Confidential | **Purview DLP / labels** |
| Encrypted file opens in Word but Copilot won’t summarize | **Label usage rights (EXTRACT)** |
| Phishing attachment / malware | **Microsoft Defender** |
| Need to prove which files grounded an answer | **Purview audit / eDiscovery** (topic 06) |
| Discover risky AI usage patterns org-wide | **DSPM for AI / IRM** |

### Graph vs search vs Copilot

| Capability | Role |
|------------|------|
| Microsoft Graph | Programmatic access to M365 objects the caller can access |
| Microsoft Search | Discover content within permissions |
| Microsoft 365 Copilot | LLM + grounding over permitted Graph/search-accessible work data |

Same boundary: **user’s permissions.**

### “Enable Copilot” vs “secure Copilot”

| Action | Outcome |
|--------|---------|
| Assign Copilot license only | Users get the feature; oversharing risks amplify |
| Remediate permissions + labels + DLP + DSPM | Feature + safer grounding |
| Disable Defender | Does **not** fix oversharing |

---

## 6. ⚠️ Exam traps

- **Copilot is not Global Admin.** It does not bypass site ACLs or mailbox permissions.  
- **Graph does not override ACLs** — it enforces them.  
- **Defender ≠ oversharing tool.** Malware detection won’t fix “Everyone except external users” on HR sites.  
- **Purview does not replace permissions** — it adds classification, DLP, retention, AI posture.  
- **Responsible AI ≠ “block all AI.”** It means privacy, security, transparency, accountability while using AI.  
- Users with **direct file permission** but blocked by **Restricted Access Control** won’t see that content in Copilot/search (topic 07) — permissions planes can stack.  
- S/MIME and password-protected docs are common “why didn’t Copilot read this?” distractors.

---

## 7. Hands-on checklist

- [ ] Pick a test user with **limited** SharePoint access; prompt Copilot about a file only **another** user can open — confirm it is **not** returned  
- [ ] As that other user, confirm Copilot **can** cite the same file  
- [ ] Apply a sensitivity label with encryption; test summarization with/without EXTRACT rights (if lab licenses allow)  
- [ ] In Purview, locate DLP policies with **Copilot** location  
- [ ] In SharePoint admin center, note sharing defaults that create oversharing (Anyone links, EEEU)  
- [ ] Review Microsoft Learn page on Purview + Copilot data security (link below)  
- [ ] List the six responsible AI principles and one admin control that supports each (privacy → ACL/labels; accountability → audit/IRM)

---

## 8. Checkpoint

1. Does Microsoft 365 Copilot bypass SharePoint ACLs to improve answer quality?  
2. What Microsoft platform primarily supplies the organizational content that grounds Copilot responses?  
3. Name the three control planes called out in the skills outline for protecting against Copilot-related risks.  
4. A phishing doc is delivered by email. Which plane is the first line for malware/threat detection?  
5. Why can Copilot “suddenly” expose old HR files that were always shared too broadly?

### Answers

1. **No** — Copilot only uses content the user is already permitted to access  
2. **Microsoft Graph** (grounding over permitted Microsoft 365 data)  
3. **Microsoft 365**, **Microsoft Purview**, and **Microsoft Defender**  
4. **Microsoft Defender** (threat protection)  
5. Copilot **surfaces** over-permissioned content that was previously hard to discover — it amplifies oversharing, it doesn’t create new access

---

## 9. Learn links

- [Study guide for Exam AB-900](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ab-900)  
- [Use Microsoft Purview for Microsoft 365 Copilot & Copilot Chat](https://learn.microsoft.com/en-us/purview/ai-m365-copilot)  
- [Configure a secure & governed foundation for Copilot](https://learn.microsoft.com/en-us/microsoft-365/copilot/configure-secure-governed-data-foundation-microsoft-365-copilot)  
- [Microsoft 365 Copilot documentation](https://learn.microsoft.com/en-us/copilot/microsoft-365/)  
- [Microsoft Graph overview](https://learn.microsoft.com/en-us/graph/overview)  
- [Microsoft responsible AI](https://www.microsoft.com/ai/responsible-ai) (verify current principles on Microsoft Learn / corporate Responsible AI pages)

**Related topics:** [04 Purview protection & lifecycle](./04-purview-protection-lifecycle.md) · [06 Governance risks & alerts](./06-governance-risks-alerts.md) · [07 SharePoint oversharing](./07-sharepoint-oversharing.md)
