# 04 — Purview protection & lifecycle

**Exam:** AB-900 · Domain 2 (35–40%) · Skill **2.1 Understand Microsoft Purview**  
**Skills measured as of:** July 22, 2026  
**Admin home:** [Microsoft Purview portal](https://purview.microsoft.com)

---

## 1. Official bullets covered

- Understand features and capabilities of Microsoft Purview **Information Protection**, **Data Loss Prevention (DLP)**, **Insider Risk Management**, **Communication Compliance**, **Data Security Posture Management (DSPM) for AI**, and **Data Lifecycle Management**
- Identify the use cases for **sensitivity labels** in Microsoft Purview
- Understand **data classification** in Microsoft Purview
- Understand **retention**

---

## 2. Why it matters on the exam

Domain 2 is the heaviest scoring block. Skill 2.1 is mostly “name the right Purview capability for the scenario.” Candidates lose points by swapping **labels vs DLP vs retention vs DSPM for AI**. Know one-sentence purpose for each product, then the Copilot-specific wrinkles (label inheritance, DLP location for Copilot, retention of Copilot interactions).

---

## 3. Core concepts

### Microsoft Purview (family, not one product)

Purview is the suite for **data security, governance, and compliance** across Microsoft 365 (and beyond). AB-900 names a specific subset — learn those names exactly as written in the study guide.

| Capability | One-line purpose |
|------------|------------------|
| **Information Protection** | Classify and protect content with **sensitivity labels** (markings, encryption, access rights) that travel with the item |
| **Data Loss Prevention (DLP)** | Detect sensitive content and **enforce policies** to prevent inappropriate sharing/use (including Copilot processing) |
| **Insider Risk Management (IRM)** | Detect and investigate **internal risk** patterns (exfiltration, IP theft, risky AI usage) using ML signals |
| **Communication Compliance** | Detect **conduct / regulatory** issues in communications (including AI prompts/responses) |
| **DSPM for AI** | Discover, assess, and govern **AI activity** and sensitive data exposed through AI apps |
| **Data Lifecycle Management** | **Retain or delete** content (including Copilot prompts/responses) for business/legal needs |

### Sensitivity labels (Information Protection)

- Persistent classification + optional protection (encryption, headers/footers/watermarks, access control)
- Apply manually, via policy prompts, or automatically (auto-labeling — deeper automation often needs higher license tiers)
- Follow the file/email across apps and locations once applied
- **Use cases to memorize:**
  - Mark Confidential / Highly Confidential content
  - Encrypt so only authorized users can open or extract content
  - Scope SharePoint/Teams site privacy and external sharing when labels are applied to containers
  - Constrain what Copilot can ground on (especially when encryption/usage rights or DLP-for-Copilot policies apply)
  - Inherit into new content Copilot drafts from a labelled source

### Data classification

- Discovers and tags sensitive data using:
  - **Sensitive information types (SITs)** — patterns (credit cards, national IDs, etc.)
  - **Trainable classifiers** — ML models for categories hard to regex (contracts, resumes, etc.)
- Feeds reporting in explorers, auto-labeling, DLP, and AI posture views
- Classification answers “**what sensitive data do we have and where?**” — not “block the send” (that’s DLP)

### Retention (Data Lifecycle Management)

- **Retention policies** and **retention labels** keep or delete content for a period
- Copilot **prompts and responses** are organizational records — they can be retained/deleted via dedicated Copilot retention locations
- Retention ≠ encryption ≠ DLP. Retention answers “**how long do we keep it?**”

### DLP (Data Loss Prevention)

- Policies match conditions (SITs, labels, keywords, etc.) and take actions (audit, warn, block, restrict Copilot processing)
- Includes a **Microsoft 365 Copilot / Copilot Chat** policy location so you can stop Copilot from using content with specific labels or sensitive types
- Generates **alerts** for investigation (covered more in topic 06)

### Insider Risk Management vs Communication Compliance

| | **Insider Risk Management** | **Communication Compliance** |
|--|----------------------------|------------------------------|
| Focus | User **risk patterns** over time (exfil, IP theft, risky AI) | **Message/content** policy violations (harassment, regulatory language) |
| Output | Risk alerts / cases for investigation | Policy violation reviews for investigators |
| Copilot angle | Risky AI usage templates / Adaptive Protection scenarios | Unethical or policy-breaking AI prompts/responses |

### DSPM for AI

- Front door for **AI data security posture**: which AI apps are in use, sensitive data in interactions, oversharing risk assessments, recommendations/one-click policies
- Exam wording: **“DSPM for AI”** (study guide). Product UI may also show broader **DSPM** — answer with the outline term
- Complements (does not replace) labels, DLP, IRM, and Communication Compliance

---

## 4. How it works (admin reasoning)

### Protection stack for Copilot-ready tenants

1. **Classify** — SITs / trainable classifiers find sensitive content  
2. **Label** — sensitivity labels mark and optionally encrypt  
3. **Prevent leakage / misuse** — DLP policies (including Copilot location)  
4. **Detect people risk** — IRM for risky behavior; Communication Compliance for conduct  
5. **Govern AI posture** — DSPM for AI assessments and recommendations  
6. **Lifecycle** — retention for records including Copilot interactions  

### Sensitivity labels + Copilot (high-yield)

- Copilot respects **existing permissions** first; labels add a second gate when encryption/usage rights apply  
- For encrypted labelled content, AI apps typically need **VIEW + EXTRACT** usage rights to return/summarize content — VIEW alone may open the file for a user but block Copilot summarization  
- Enable sensitivity labels for **SharePoint and OneDrive** so encrypted files are properly processed beyond “data in use” on Windows Office apps  
- When Copilot drafts new content from a labelled source in Word/PowerPoint/Outlook, the **source label (and protection) can be inherited**; if multiple sources, **highest-priority label** wins  
- Copilot Chat can **display sensitivity labels** for cited items  

### Retention of Copilot content

- Treat prompts/responses like other M365 records  
- Use Data Lifecycle Management retention policies scoped to Copilot experiences when the scenario is “keep AI chats for N days / delete after investigation window”

---

## 5. Compare / choose

### Labels vs DLP vs retention vs DSPM for AI

| Need | Choose | Why |
|------|--------|-----|
| Persistently classify & protect a document (markings/encryption) | **Sensitivity labels** (Information Protection) | Protection travels with the item |
| Stop a user from emailing/sharing (or stop Copilot processing) sensitive content | **DLP** | Policy enforcement + alerts |
| Keep or delete Copilot chats / files for N years | **Data Lifecycle Management / retention** | Time-based keep/delete |
| See AI usage posture, sensitive data in AI, get AI risk recommendations | **DSPM for AI** | Discovery + posture for AI apps |
| Investigate employee exfiltration / risky AI patterns | **Insider Risk Management** | People-risk cases |
| Flag harassing or policy-breaking messages/prompts | **Communication Compliance** | Conduct / regulatory review |
| Find where PCI/PII lives before rollout | **Data classification** (+ explorers in topic 06) | Discovery, not enforcement |

### Sensitivity label vs container settings alone

| Approach | Strength | Limit |
|----------|----------|-------|
| File/email sensitivity label | Follows the item; encryption/rights | Must publish labels; users or auto-label must apply |
| SharePoint/Teams sharing & site privacy | Controls who can reach the site | Doesn’t encrypt a file that left the site |
| Both | Best practice | Labels + least-privilege sharing |

### When exam says “protect” vs “prevent sharing” vs “keep”

- **Protect / classify / encrypt** → sensitivity labels  
- **Prevent sharing / block Copilot use of labelled content** → DLP  
- **Keep for compliance period** → retention  
- **AI risk posture / discover AI activity** → DSPM for AI  

---

## 6. ⚠️ Exam traps

- **Labels ≠ DLP.** Labels classify/protect; DLP enforces spill/use policies.  
- **Retention ≠ backup.** Retention manages keep/delete for compliance, not restore-from-disaster.  
- **DSPM for AI ≠ generic DLP.** DSPM discovers/governs AI posture; DLP still does the block.  
- **IRM ≠ Communication Compliance.** People-risk cases vs message-policy violations.  
- **Copilot does not replace Purview.** Copilot consumes content that labels/DLP/permissions already govern.  
- **VIEW ≠ EXTRACT.** Encrypted labelled files may open for a user but still be unavailable to Copilot without EXTRACT.  
- Answer **“DSPM for AI”** when the outline/scenario is about AI activity posture — even if your tenant UI says “DSPM.”  
- Do not invent Preview-only portals; prefer **purview.microsoft.com** (not retired compliance.microsoft.com).

---

## 7. Hands-on checklist

In a lab tenant (roles permitting):

- [ ] Open **Microsoft Purview** portal → locate Information Protection, DLP, Data Lifecycle Management, DSPM for AI, Insider Risk Management, Communication Compliance  
- [ ] Review existing **sensitivity labels** and a label policy (published to users/groups)  
- [ ] Confirm whether **sensitivity labels for SharePoint and OneDrive** are enabled  
- [ ] Create or inspect a **DLP policy** and note locations (Exchange, SharePoint, Teams, **Copilot**)  
- [ ] Open **Data Lifecycle Management** → retention policies; note any Copilot-related location  
- [ ] Open **DSPM for AI** (or DSPM) → view recommendations / AI activity overview  
- [ ] Skim one **Insider Risk** policy template and one **Communication Compliance** policy  
- [ ] Apply a sensitivity label to a test file → open in Word → use Copilot draft and observe **label inheritance** (if licensed)

---

## 8. Checkpoint

1. Which Purview capability applies persistent classification and optional encryption that travels with a file?  
2. An admin must stop Microsoft 365 Copilot from summarizing items labelled Highly Confidential. Which capability is the primary enforcement tool?  
3. Legal asks how long Copilot prompts/responses are kept. Which Purview area do you configure?  
4. True or false: DSPM for AI replaces the need for sensitivity labels.  
5. A user can open an encrypted labelled Word doc but Copilot won’t summarize it. Which usage-right concept explains this?

### Answers

1. **Microsoft Purview Information Protection / sensitivity labels**  
2. **DLP** (policy location for Microsoft 365 Copilot / Copilot Chat; often driven by sensitivity label conditions)  
3. **Data Lifecycle Management / retention**  
4. **False** — DSPM for AI discovers and recommends; labels (and DLP/IRM/etc.) still protect  
5. Copilot/AI needs **EXTRACT** (with VIEW) on encrypted content; VIEW alone is not enough for summarization

---

## 9. Learn links

- [Study guide for Exam AB-900](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ab-900)  
- [Use Microsoft Purview for Microsoft 365 Copilot & Copilot Chat](https://learn.microsoft.com/en-us/purview/ai-m365-copilot)  
- [Learn about sensitivity labels](https://learn.microsoft.com/en-us/purview/sensitivity-labels)  
- [Learn about data loss prevention](https://learn.microsoft.com/en-us/purview/dlp-learn-about-dlp)  
- [DSPM for AI (classic)](https://learn.microsoft.com/en-us/purview/dspm-for-ai)  
- [Microsoft Purview documentation](https://learn.microsoft.com/en-us/purview/)  
- [Configure a secure & governed foundation for Copilot](https://learn.microsoft.com/en-us/microsoft-365/copilot/configure-secure-governed-data-foundation-microsoft-365-copilot)

**Related topics:** [05 Copilot data security & Graph](./05-copilot-data-security-graph.md) · [06 Governance risks & alerts](./06-governance-risks-alerts.md) · [07 SharePoint oversharing](./07-sharepoint-oversharing.md)
