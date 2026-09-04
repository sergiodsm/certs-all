# 07 — SharePoint oversharing

**Exam:** AB-900 · Domain 2 (35–40%) · Skill **2.4 Identify and monitor oversharing in SharePoint**  
**Skills measured as of:** July 22, 2026  
**Admin home:** [SharePoint admin center](https://admin.microsoft.com/sharepoint)

---

## 1. Official bullets covered

- Identify the **tools to troubleshoot oversharing** in an organization  
- Run a **data access governance report** in SharePoint  
- Understand features and capabilities of **SharePoint Advanced Management**, including **restricted access control**

---

## 2. Why it matters on the exam

Oversharing is why Copilot security feels “broken” when permissions were already wrong. Generative AI **amplifies** discoverability of broadly shared content. AB-900 expects you to name **SharePoint** governance tools — especially **data access governance (DAG) reports** and **SharePoint Advanced Management (SAM)** with **restricted access control (RAC)** — not Defender malware workflows.

⚠️ **Oversharing ≠ malware.**

---

## 3. Core concepts

### What “oversharing” means

Content is accessible to a **wider audience than intended**, for example:

- Shared with **Everyone except external users (EEEU)** or organization-wide groups  
- **Anyone** (anonymous) links  
- Broken permission inheritance / sprawling unique permissions  
- Ownerless or inactive sites with stale broad access  
- Large membership on sites that hold sensitive files  

Before Copilot, obscurity hid much of this. Copilot surfaces it via natural language for anyone who already has access.

### SharePoint Advanced Management (SAM)

Governance controls for SharePoint and OneDrive that help admins:

- **Identify** oversharing and access risk (reports + insights)  
- **Restrict** access and discovery for high-risk sites  
- **Remediate** via site access reviews, ownership/inactive site policies, and related controls  

SAM is commonly available with **Microsoft 365 Copilot** licensing (verify current packaging on Learn). Exam focus: capabilities, not SKU pricing.

### Data access governance (DAG) reports

Reports in the SharePoint admin center that help you find sites/content with oversharing or sensitive exposure risk. Typical DAG report types include:

| Report / insight | What it helps you find |
|------------------|------------------------|
| **Permission state** reports (sites / OneDrive / files) | Snapshot of how broadly data is exposed |
| **Site permissions for a given user** | All sites a user can access and how |
| **Sensitivity label snapshot** | Label distribution across sites |
| **Sharing links activity** | Sites with many new sharing links (recent window) |
| **EEEU insights** | Top items/groups shared with Everyone except external users |

Admins can generate insights and initiate **site access reviews** from DAG findings so site owners remediate.

### Restricted access control (RAC)

- Limits access to a SharePoint or OneDrive site to members of specified **Microsoft 365 groups / Entra security groups**  
- Users outside the control groups are blocked from the site even if they somehow had direct file permissions in some scenarios — RAC is honored in **site access, organization-wide search, and Copilot**  
- Exam bullet name: **restricted access control** (not “restricted site access”)

### Related SAM capability: Restricted Content Discovery (RCD)

Not always spelled out as its own skills bullet, but strongly associated with Copilot readiness docs:

- **RCD** prevents high-risk site content from surfacing in **Microsoft 365 Copilot / agentic experiences** (and related discovery) while you fix permissions  
- **RAC** = who can access the site  
- **RCD** = whether content is discoverable to Copilot/search experiences (interim control)

Know the distinction if a scenario offers both.

### Other troubleshooting tools (identify)

When the exam asks for tools to troubleshoot oversharing, think the SAM toolkit:

- DAG reports (+ AI insights on reports where available)  
- Site access reviews  
- Restricted access control  
- Restricted content discovery  
- Inactive site / site ownership policies  
- Tenant sharing settings (Anyone links, external sharing) in SharePoint admin center  
- Purview DSPM data risk assessments (complements SAM; often paired in Copilot foundation guidance)

---

## 4. How it works (admin reasoning)

### Investigate oversharing

1. Open **SharePoint admin center**  
2. Run **Data access governance** reports (permission state, sharing links, EEEU, etc.)  
3. Prioritize sites with **sensitive content + broad access**  
4. Optionally use **AI insights** on reports for patterns/next steps  
5. Kick off **site access reviews** for owners  
6. Apply interim controls (**RCD**) and/or **RAC** for business-critical sites  
7. Fix root cause: remove EEEU/Anyone, repair inheritance, assign owners, apply site sensitivity labels  

### Foundational remediation order (from Copilot secure-foundation guidance)

1. **Remediate** oversharing (identify → interim protect → fix access)  
2. **Guardrails** (secure defaults at provisioning, RAC defaults, disable risky link types, auto-label/DLP)  
3. **Meet regulations** (Compliance Manager, retention, eDiscovery hygiene)

Exam takeaway: don’t “just pilot Copilot” past known oversharing — **remediate first**.

### RAC and Copilot

- RAC policies are honored in Copilot and org-wide search  
- Index/propagation delay can occur; larger sites may take longer to reflect  
- Purview audit can log RAC apply/remove/change events  

---

## 5. Compare / choose

### Oversharing vs threat

| Symptom | Category | Typical tool |
|---------|----------|--------------|
| Salary spreadsheet open to whole company | **Oversharing / governance** | DAG reports, RAC, RCD, sharing settings |
| Encrypted ransomware payload in email | **Malware / threat** | Microsoft Defender |
| Copilot cites an old project site the user “shouldn’t” see | Usually **ACL oversharing** | SharePoint permissions + SAM |
| User prompts Copilot with harassment | **Conduct** | Communication Compliance (topic 06) |

### RAC vs RCD vs DLP vs labels

| Control | Primary effect |
|---------|----------------|
| **Restricted access control (RAC)** | Only specified groups can access the site (and thus Copilot/search for that site) |
| **Restricted Content Discovery (RCD)** | Hide site content from Copilot/discovery while access may remain |
| **Sensitivity labels** | Classify/protect items or configure container privacy/sharing |
| **DLP for Copilot** | Block Copilot processing of matching labelled/sensitive content |
| **DAG reports** | **Find** the problem — not the permanent fix by themselves |

### Where to click

| Task | Admin center |
|------|----------------|
| Run DAG reports / configure RAC | **SharePoint admin center** |
| DLP / DSPM / labels | **Microsoft Purview** |
| Malware incidents | **Microsoft Defender** portal |

---

## 6. ⚠️ Exam traps

- **Oversharing ≠ malware.** Don’t pick Defender XDR as the primary oversharing answer.  
- Say **restricted access control**, not informal “lock the site” alone.  
- **DAG reports identify** risk; they don’t automatically revoke all bad permissions.  
- Copilot did not “hack” the tenant — the user already had access.  
- RAC ≠ RCD (access vs discovery).  
- Fixing one file’s link doesn’t fix tenant-wide EEEU culture — use reports + policies.  
- July 2026 change log: oversharing skill area marked **Minor** (wording) — substance still SAM + DAG + RAC.

---

## 7. Hands-on checklist

- [ ] SharePoint admin center → **Data access governance** → run a **permission state** or **sharing links** report  
- [ ] Identify a lab site shared too broadly; note EEEU / Anyone link usage  
- [ ] Review **Restricted access control** settings for a site (apply a test group in lab)  
- [ ] Review **Restricted Content Discovery** docs/UI for Copilot exclusion scenarios  
- [ ] Initiate or review a **site access review** from a DAG report (if available)  
- [ ] Check organization-level **sharing** settings (Anyone links, external sharing)  
- [ ] Cross-check a high-risk site in Purview **DSPM** data risk assessment recommendations  

---

## 8. Checkpoint

1. Which SharePoint report family helps identify overshared sites and broad permissions?  
2. Which SAM feature restricts site access to specific Microsoft 365 / Entra groups and is honored by Copilot?  
3. True or false: Microsoft Defender is the primary tool to remediate “Everyone except external users” on an HR site.  
4. Does Copilot create new SharePoint permissions when it cites a file?  
5. RAC vs RCD — which one primarily hides content from Copilot discovery as an interim control?

### Answers

1. **Data access governance (DAG) reports**  
2. **Restricted access control (RAC)**  
3. **False** — that is SharePoint oversharing / SAM governance, not malware remediation  
4. **No** — it uses existing access; oversharing means the user already could open the content  
5. **Restricted Content Discovery (RCD)**

---

## 9. Learn links

- [Study guide for Exam AB-900](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ab-900)  
- [SharePoint Advanced Management overview](https://learn.microsoft.com/en-us/sharepoint/advanced-management)  
- [Get ready for Copilot with SharePoint Advanced Management](https://learn.microsoft.com/en-us/sharepoint/get-ready-copilot-sharepoint-advanced-management)  
- [Data access governance reports](https://learn.microsoft.com/en-us/sharepoint/data-access-governance-reports)  
- [Restricted access control for SharePoint sites](https://learn.microsoft.com/en-us/sharepoint/restricted-access-control)  
- [Restricted content discovery](https://learn.microsoft.com/en-us/sharepoint/restricted-content-discovery) (verify current Learn title)  
- [Configure a secure & governed foundation for Copilot](https://learn.microsoft.com/en-us/microsoft-365/copilot/configure-secure-governed-data-foundation-microsoft-365-copilot)

**Related topics:** [04 Purview protection & lifecycle](./04-purview-protection-lifecycle.md) · [05 Copilot data security & Graph](./05-copilot-data-security-graph.md) · [06 Governance risks & alerts](./06-governance-risks-alerts.md)
