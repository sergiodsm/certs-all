# Domain 2 practice — Data protection and governance for Microsoft 365 and Copilot

**Exam:** AB-900 · Microsoft 365 Copilot and Agent Administration Fundamentals  
**Weight:** 35–40% (highest) · Skills measured as of **July 22, 2026**  
**Coverage:** Topics 04–07 (Purview, Copilot data security/Graph, governance risks/alerts, SharePoint oversharing)

**How to use:** Domain 2 carries the most points — drill this bank until ≥80%. Cover answer blocks while practicing. **Unofficial study aids** — not exam dumps. Match the **tool to the symptom**; do not invent non-GA product capabilities.

**Question types:** single-choice · multi-select · which Purview / SharePoint tool

---

### Q1. Sensitivity label vs DLP
An admin needs documents containing social security numbers to be automatically classified and encrypted when users save them. Which Purview capability is the **best primary fit**?

- A. Communication Compliance
- B. Sensitivity labels (Information Protection)
- C. Content search only
- D. Copilot Analytics

**Correct:** B  
**Why correct:** Sensitivity labels classify and can protect (including encryption/usage rights) as part of Microsoft Purview Information Protection.  
**Why distractors fail:** A reviews communications for policy/conduct; C finds existing items; D measures Copilot adoption — none primarily classify/encrypt on save.  
**Mapped skill:** 2.1 Describe Microsoft Purview Information Protection and sensitivity labels  
⚠️ Trap: Labels ≠ DLP — DLP detects/constrains risky sharing; labels classify/protect.

---

### Q2. DLP policy scenario
Users report they can still email spreadsheets with credit card numbers to external recipients. Leadership wants automatic detection and blocking of that sharing. What should the admin configure?

- A. A Data Loss Prevention (DLP) policy
- B. Privileged Identity Management
- C. Teams meeting recording policies only
- D. Identity Secure Score

**Correct:** A  
**Why correct:** DLP policies detect sensitive information types and can block or warn on risky sharing/exfiltration paths.  
**Why distractors fail:** B is privileged role JIT; C is Teams workload policy; D is identity posture scoring.  
**Mapped skill:** 2.1 Describe Microsoft Purview Data Loss Prevention  

---

### Q3. Retention vs sensitivity
Legal requires email and files in a project site to be kept for seven years, then disposed. Which Purview area addresses this requirement?

- A. Insider Risk Management only
- B. Data Lifecycle Management / retention
- C. Microsoft Defender XDR incidents
- D. Enterprise applications SSO

**Correct:** B  
**Why correct:** Retention and disposal timelines are Data Lifecycle Management (retention) concerns — not sensitivity classification.  
**Why distractors fail:** A is people-risk behaviors; C is threat incidents; D is Entra app SSO.  
**Mapped skill:** 2.1 Describe classification, retention, and Data Lifecycle Management  
⚠️ Trap: Retention ≠ sensitivity label.

---

### Q4. Purview product matching (multi-select)
**Select 3.** Match the need to the correct Purview capability family. Which pairings are correct?

- A. Detect potential data theft by departing employees → Insider Risk Management
- B. Review potentially harassing Teams chats against corporate policy → Communication Compliance
- C. Discover and manage AI application data risks/posture → DSPM for AI
- D. Assign Microsoft 365 Copilot seats to a group → DSPM for AI
- E. Create a user mailbox → Communication Compliance

**Correct:** A, B, C  
**Why correct:** IRM = people-risk; Comm Compliance = communication conduct/policy; DSPM for AI = AI data security posture/activity.  
**Why distractors fail:** D is M365 license assignment; E is Exchange.  
**Mapped skill:** 2.1 Describe Purview IP, DLP, IRM, Communication Compliance, DSPM for AI, and DLM  

---

### Q5. Copilot and existing permissions
A user asks Copilot to summarize a confidential budget workbook stored in SharePoint. The user is not a member of that site. What should happen?

- A. Copilot returns the full workbook because it has tenant-wide Graph admin rights
- B. Copilot grounds only on content the signed-in user can already access; the workbook should not be returned as authorized work data
- C. Copilot always decrypts sensitivity-labeled files regardless of permissions
- D. Assigning a Copilot license automatically grants SharePoint Visitor to all sites

**Correct:** B  
**Why correct:** Copilot uses Microsoft Graph and the user’s existing permissions — it does not become a super-user or bypass ACLs.  
**Why distractors fail:** A/C/D invent privilege escalation via Copilot or licensing.  
**Mapped skill:** 2.2 Understand how Copilot accesses data and how Microsoft Graph influences responses  
⚠️ Trap: License ≠ content access; Copilot does not bypass ACL.

---

### Q6. Graph influence
Which statement best describes Microsoft Graph’s role with Microsoft 365 Copilot?

- A. Graph stores all LLM model weights for Copilot
- B. Graph is the API layer used to retrieve organizational content the user is permitted to access, shaping grounded responses
- C. Graph replaces Conditional Access for Copilot sessions
- D. Graph grants Global Admin whenever Copilot is licensed

**Correct:** B  
**Why correct:** Graph provides the permitted org context (mail, files, chats, etc.); the model generates language over that grounded content.  
**Why distractors fail:** A/C/D are inaccurate product claims.  
**Mapped skill:** 2.2 Microsoft Graph influences Copilot responses  

---

### Q7. Three control planes (multi-select)
**Select 2.** An admin is hardening Copilot risk. Which statements correctly map control planes?

- A. Microsoft 365 site/library permissions remain the primary gate for what Copilot can ground on
- B. Purview labels, DLP, and related controls add protection beyond raw ACLs
- C. Microsoft Defender alone remediates SharePoint “Everyone” oversharing links
- D. Turning on Copilot disables all Purview policies automatically

**Correct:** A, B  
**Why correct:** ACL + Purview (+ Defender for threats) work together; Copilot respects permissions and protection controls.  
**Why distractors fail:** C — oversharing is SharePoint governance, not primarily Defender malware; D invents a dangerous default.  
**Mapped skill:** 2.2 Permissions and controls in Microsoft 365, Purview, and Defender  

---

### Q8. Responsible AI
During Copilot enablement, executives ask what “responsible AI” means for administrators. Which admin-aligned statement is best?

- A. Disable all citations and hide that AI is involved
- B. Apply least privilege, enforce Purview/governance, monitor AI usage, and keep humans accountable for outcomes
- C. Grant everyone Owner on all sites so Copilot answers are always complete
- D. Replace legal review with unsupervised Copilot decisions for contracts

**Correct:** B  
**Why correct:** Fundamentals map responsible AI themes (privacy/security, transparency, accountability, etc.) to admin actions: least privilege, controls, monitoring, human governance.  
**Why distractors fail:** A hurts transparency; C worsens oversharing; D removes accountability.  
**Mapped skill:** 2.2 Understand responsible AI principles  

---

### Q9. Compliance Manager vs eDiscovery
Auditors want a prioritized improvement score and recommended actions to strengthen compliance posture. Separately, legal needs to find specific emails about a vendor dispute. Which pairing is correct?

- A. Compliance Manager for posture recommendations; Content search (eDiscovery) for finding specific items
- B. Content search for Secure Score; Compliance Manager for mailbox creation
- C. Both tasks are done only in the Teams admin center
- D. Both tasks are done only with Copilot Analytics

**Correct:** A  
**Why correct:** Compliance Manager = compliance posture/recommendations; Content search = locate specific content for investigations/eDiscovery scenarios.  
**Mapped skill:** 2.3 Describe Compliance Manager and Content search  
⚠️ Trap: Compliance Manager ≠ eDiscovery.

---

### Q10. DLP alerts and activity explorer
Security needs to review recent DLP policy matches and explore where sensitive information types are being used or shared. Which Purview experiences fit?

- A. DLP alerts and activity explorer
- B. PIM activation history and Exchange DKIM only
- C. Teams dial pad settings
- D. Azure Cost Management alone

**Correct:** A  
**Why correct:** DLP alerts surface policy matches; activity explorer helps investigate sensitive data activities/labeling signals.  
**Why distractors fail:** B/C/D do not address DLP investigation for this stem.  
**Mapped skill:** 2.3 Describe DLP alerts and activity explorer  

---

### Q11. DSPM for AI
Leadership wants visibility into AI application usage and related data security posture across the organization — not only one classic DLP alert. Which capability is the best exam-aligned fit?

- A. DSPM for AI
- B. Exchange transport rules only
- C. SharePoint site theme gallery
- D. Entra Access reviews only

**Correct:** A  
**Why correct:** DSPM for AI focuses on discovering/managing AI-related data risks and posture/activity — distinct from “create one DLP policy” as the entire answer.  
**Why distractors fail:** B/C/D are wrong tool classes for org-wide AI data posture.  
**Mapped skill:** 2.3 Describe DSPM for AI  
⚠️ Trap: DSPM for AI ≠ “generic DLP only.”

---

### Q12. Insider Risk vs Comm Compliance
HR reports unusual downloads of confidential files by an employee who submitted resignation, and separately wants review of potentially inappropriate language in Teams. Which tools map correctly?

- A. File theft risk → Insider Risk Management; inappropriate communications → Communication Compliance
- B. Both scenarios → SharePoint theme settings
- C. Both scenarios → Defender antivirus definitions only
- D. Both scenarios → assign more Copilot licenses

**Correct:** A  
**Why correct:** IRM targets risky user behaviors (e.g., potential data theft); Communication Compliance reviews communications against conduct/policy.  
**Why distractors fail:** B/C/D miss the governance product match.  
**Mapped skill:** 2.3 Describe Insider Risk Management and Communication Compliance  

---

### Q13. Data Explorer
An admin needs to explore where sensitive content resides and understand classification volume to plan labeling. Which Purview tool is designed for exploring that landscape?

- A. Data Explorer
- B. Teams Live events only
- C. App registrations
- D. Power Platform maker portal billing address

**Correct:** A  
**Why correct:** Data Explorer helps explore sensitive content/classification landscape in Purview governance scenarios.  
**Why distractors fail:** B/C/D are unrelated admin surfaces.  
**Mapped skill:** 2.3 Describe Data Explorer  

---

### Q14. Oversharing amplification
After Copilot rollout, users suddenly “discover” many confidential files via natural language prompts. Investigation shows the files were already shared with broad Everyone-style links. What is the best framing?

- A. Copilot created new SharePoint permissions for those users
- B. Copilot amplified existing oversharing; remediate SharePoint permissions and governance, not “uninstall Graph”
- C. Only Defender XDR can remove SharePoint links
- D. Deleting saved prompts revokes all file ACLs

**Correct:** B  
**Why correct:** Copilot surfaces content users already could access — oversharing becomes more visible. Fix permissions/governance.  
**Why distractors fail:** A/C/D are false mechanisms.  
**Mapped skill:** 2.2 / 2.4 Copilot data access and SharePoint oversharing  
⚠️ Trap: Oversharing ≠ malware.

---

### Q15. DAG reports
A SharePoint admin needs reports on sites with “Everyone except external users” sharing and other oversharing patterns. Which capability should they start with?

- A. Data access governance (DAG) reports in SharePoint
- B. Exchange message trace for calendar invites
- C. Entra Identity Secure Score only
- D. Copilot prompt gallery deletion

**Correct:** A  
**Why correct:** DAG reports are the SharePoint governance reporting entry for oversharing patterns.  
**Why distractors fail:** B/C/D do not provide SharePoint oversharing governance reports.  
**Mapped skill:** 2.4 Troubleshoot oversharing with Data access governance reports  

---

### Q16. Advanced Management / RAC
Leadership wants stronger controls to restrict access to SharePoint content for specific groups and reduce oversharing risk beyond basic sharing settings. Which SharePoint capability family is the exam-aligned answer?

- A. SharePoint Advanced Management, including restricted access control (RAC)
- B. Teams dial plans
- C. Outlook offline mode
- D. Azure Disk Encryption for VMs only

**Correct:** A  
**Why correct:** SharePoint Advanced Management / RAC addresses advanced access restriction and oversharing governance scenarios.  
**Why distractors fail:** B/C/D are wrong products for SharePoint access governance.  
**Mapped skill:** 2.4 Describe SharePoint Advanced Management / restricted access control  

---

### Q17. Which tool? — governance chooser
An investigator must find all emails and files mentioning a project code for an upcoming legal matter. Where do they go?

- A. Microsoft Purview Content search (eDiscovery)
- B. Microsoft 365 admin center → Domains
- C. Teams admin center → Holidays
- D. Power Platform → Connection references only

**Correct:** A  
**Why correct:** Content search locates specific mail/files across Microsoft 365 for investigation/eDiscovery scenarios.  
**Why distractors fail:** B/C/D do not perform content discovery for legal matters.  
**Mapped skill:** 2.3 Describe Content search  

---

### Q18. Labels, DLP, and Copilot together (multi-select)
**Select 2.** Which statements are accurate about protecting content that Copilot might ground on?

- A. Fixing over-permissioned SharePoint libraries reduces what Copilot can surface to those users
- B. Sensitivity labels and DLP can add constraints beyond ACLs for risky AI/data scenarios
- C. Approving a custom agent automatically grants EXTRACT rights on all labeled files
- D. Identity Secure Score encrypts all SharePoint libraries by default

**Correct:** A, B  
**Why correct:** Permissions are the primary gate; Purview labels/DLP add protective controls. Agent approval does not widen ACLs; Secure Score does not auto-encrypt libraries.  
**Why distractors fail:** C/D invent capabilities.  
**Mapped skill:** 2.2 Permissions/controls with Purview and Copilot  
⚠️ Trap: Approving an agent does not widen file ACLs.

---

### Domain 2 answer key

| Q# | Answer | Focus |
|----|--------|--------|
| 1 | B | Sensitivity labels |
| 2 | A | DLP |
| 3 | B | Retention / DLM |
| 4 | A, B, C | Purview product map |
| 5 | B | Copilot + ACL |
| 6 | B | Microsoft Graph |
| 7 | A, B | Control planes |
| 8 | B | Responsible AI |
| 9 | A | Compliance Manager vs search |
| 10 | A | DLP alerts / activity explorer |
| 11 | A | DSPM for AI |
| 12 | A | IRM vs Comm Compliance |
| 13 | A | Data Explorer |
| 14 | B | Oversharing amplification |
| 15 | A | DAG reports |
| 16 | A | Advanced Management / RAC |
| 17 | A | Content search |
| 18 | A, B | Labels/DLP + permissions |

**Suggested pass bar:** ≥15/18 (≥80%). Revisit topics [`04`](../topics_details/04-purview-protection-lifecycle.md)–[`07`](../topics_details/07-sharepoint-oversharing.md) and [`exam-traps.md`](../topics_details/reference/exam-traps.md).
