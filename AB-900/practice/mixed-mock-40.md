# Mixed mock — 40 questions (AB-900)

**Exam:** AB-900 · Microsoft 365 Copilot and Agent Administration Fundamentals  
**Skills measured as of:** July 22, 2026  
**Weighting in this mock:** ~12 Domain 1 · ~16 Domain 2 · ~12 Domain 3 (mirrors exam emphasis; Domain 2 heaviest)

**How to use**

1. **Cover the answers** under each question (or use a sheet over **Correct / Why**).  
2. Time yourself ~**45 minutes** if simulating exam pace.  
3. Score with the key at the end. Target **≥80%** (32/40) before booking — especially do not let Domain 2 drag the score.  
4. These are **unofficial study aids** — **not** Microsoft exam dumps.

**Legend:** `[D1]` `[D2]` `[D3]` · SC = single choice · MS = multi-select

---

### Q1. [D1][SC] Distribution group home
An admin needs to create a distribution group for company announcements. Which admin center should they use?

- A. SharePoint admin center
- B. Exchange admin center
- C. Power Platform admin center
- D. Microsoft Purview portal

**Correct:** B  
**Why correct:** Distribution groups / mail recipients are Exchange Online objects.  
**Why distractors fail:** A sites; C Power Platform; D compliance — none own DGs.  
**Mapped skill:** 1.1 Exchange admin center objects  

---

### Q2. [D1][SC] SharePoint site roles
Users can view a SharePoint site but cannot edit documents in a library. Where should the admin primarily adjust site/library permissions?

- A. Teams admin center → Holidays
- B. SharePoint admin center / site permissions model
- C. Defender portal → Device inventory only
- D. Entra → App registrations secrets only

**Correct:** B  
**Why correct:** Site roles and library permissions are SharePoint-owned.  
**Why distractors fail:** A/C/D wrong ownership.  
**Mapped skill:** 1.1 SharePoint admin center objects  

---

### Q3. [D1][SC] Teams policies
An admin must apply a meeting policy to a pilot team. Which center?

- A. Teams admin center
- B. Exchange admin center
- C. Purview Data Explorer only
- D. Azure Disk Encryption

**Correct:** A  
**Why correct:** Teams policies live in the Teams admin center.  
**Why distractors fail:** B/C/D wrong centers.  
**Mapped skill:** 1.1 Teams admin center objects  

---

### Q4. [D1][MS] M365 admin center tasks
**Select 2.** Which tasks belong primarily in the Microsoft 365 admin center?

- A. Assign Microsoft 365 Copilot licenses
- B. Manage tenant domain names
- C. Author Insider Risk Management policies
- D. Create Conditional Access MFA policies
- E. Hunt XDR malware incidents

**Correct:** A, B  
**Why correct:** Licenses and domains/org settings are M365 admin center fundamentals.  
**Why distractors fail:** C Purview; D Entra; E Defender.  
**Mapped skill:** 1.1 Microsoft 365 admin center objects  

---

### Q5. [D1][SC] Zero Trust
Which statement best summarizes Zero Trust for an M365 admin?

- A. Trust internal IPs permanently after first login
- B. Verify explicitly, least privilege, assume breach
- C. Replace MFA with shared service accounts
- D. Purchase one SKU and disable all other controls

**Correct:** B  
**Why correct:** Core Zero Trust principles.  
**Why distractors fail:** A/C/D contradict Zero Trust.  
**Mapped skill:** 1.2 Zero Trust principles  
⚠️ Trap: Zero Trust ≠ one product.

---

### Q6. [D1][SC] AuthN vs AuthZ
A user passes MFA but cannot open a Teams team. What is the best explanation?

- A. Authentication failed
- B. Authentication succeeded; authorization/membership is likely insufficient
- C. SSO automatically grants Owner on all teams after MFA
- D. MFA deletes Teams policies

**Correct:** B  
**Why correct:** MFA proves identity; team membership/roles authorize access.  
**Why distractors fail:** A contradicts stem; C/D false.  
**Mapped skill:** 1.2 Authentication vs authorization  

---

### Q7. [D1][SC] Defender XDR
Security needs correlated incident investigation across identity, email, and endpoints for a suspected phishing campaign. Best portal?

- A. Microsoft Defender (XDR)
- B. SharePoint DAG reports
- C. Copilot prompt gallery
- D. Teams dial plans

**Correct:** A  
**Why correct:** Defender XDR is the threat protection/intelligence correlation surface.  
**Why distractors fail:** B governance; C/D unrelated.  
**Mapped skill:** 1.2 Microsoft Defender XDR capabilities  

---

### Q8. [D1][SC] Conditional Access
Admins must require MFA for Microsoft 365 access from unfamiliar locations. Which Entra feature enforces this?

- A. Conditional Access
- B. PIM only
- C. SharePoint RAC only
- D. Communication Compliance

**Correct:** A  
**Why correct:** CA evaluates conditions and requires controls like MFA.  
**Why distractors fail:** B privileged JIT; C SharePoint access restriction; D Purview comms.  
**Mapped skill:** 1.3 Conditional Access and SSO  
⚠️ Trap: SSO ≠ Conditional Access.

---

### Q9. [D1][SC] Risky sign-ins
Help desk escalates blocked sign-ins marked risky. Which admin center to investigate?

- A. Microsoft Entra admin center
- B. Exchange admin center
- C. SharePoint admin center
- D. Teams admin center

**Correct:** A  
**Why correct:** Risky sign-ins and identity troubleshooting are Entra surfaces.  
**Why distractors fail:** B/C/D wrong workloads.  
**Mapped skill:** 1.3 Troubleshoot MFA, CA, risky sign-ins  

---

### Q10. [D1][MS] PIM truths
**Select 2.** Which statements about PIM are true?

- A. PIM supports just-in-time privileged role activation
- B. PIM replaces MFA for all standard users
- C. Standing permanent Global Admin for every help desk agent is the PIM goal
- D. Eligible admins activate roles when needed
- E. PIM is configured in the Teams admin center

**Correct:** A, D  
**Why correct:** PIM = privileged JIT elevation.  
**Why distractors fail:** B/C misuse PIM; E wrong center.  
**Mapped skill:** 1.3 Privileged Identity Management  
⚠️ Trap: PIM ≠ workforce MFA.

---

### Q11. [D1][SC] Identity Secure Score
Leadership wants prioritized identity posture improvements. Where?

- A. Identity Secure Score in Entra
- B. SharePoint site designs
- C. Exchange litigation hold UI only
- D. Power Platform currency settings

**Correct:** A  
**Why correct:** Identity Secure Score provides identity improvement actions.  
**Why distractors fail:** B/C/D wrong tools.  
**Mapped skill:** 1.3 Identity Secure Score and audit logs  

---

### Q12. [D1][SC] App registration vs enterprise app
Which statement is correct?

- A. App registration defines the app identity; Enterprise application is the tenant instance for assignment/SSO
- B. They are always the same object name in every blade
- C. Enterprise apps are created in Purview only
- D. App registrations replace DLP

**Correct:** A  
**Why correct:** Fundamentals distinction between registration and enterprise app instance.  
**Why distractors fail:** B/C/D incorrect.  
**Mapped skill:** 1.3 App registrations and enterprise applications  
⚠️ Trap: Not interchangeable labels for the same job.

---

### Q13. [D2][SC] Sensitivity labels
Finance needs automatic classification and protection on files containing personal data. Best primary Purview fit?

- A. Sensitivity labels (Information Protection)
- B. Copilot Analytics
- C. Teams holiday calendar
- D. Azure Cost Management alone

**Correct:** A  
**Why correct:** Labels classify/protect content.  
**Why distractors fail:** B/C/D wrong jobs.  
**Mapped skill:** 2.1 Information Protection / sensitivity labels  

---

### Q14. [D2][SC] DLP
The org must block external sharing of files containing credit card numbers. Configure:

- A. Data Loss Prevention (DLP) policies
- B. PIM eligible roles
- C. Identity Secure Score only
- D. Outlook dark mode

**Correct:** A  
**Why correct:** DLP detects sensitive info and constrains risky sharing.  
**Why distractors fail:** B/C/D unrelated.  
**Mapped skill:** 2.1 Data Loss Prevention  
⚠️ Trap: Labels ≠ DLP (different primary jobs).

---

### Q15. [D2][SC] Retention
Records must be retained five years then disposed. Which Purview area?

- A. Data Lifecycle Management / retention
- B. Defender antivirus definitions
- C. Teams dial pad
- D. App registration branding

**Correct:** A  
**Why correct:** Retention/disposal is DLM.  
**Why distractors fail:** B/C/D wrong.  
**Mapped skill:** 2.1 Classification, retention, DLM  
⚠️ Trap: Retention ≠ sensitivity label.

---

### Q16. [D2][MS] Purview matching
**Select 3.** Correct matches:

- A. Departing employee mass download risk → Insider Risk Management
- B. Inappropriate Teams chat review → Communication Compliance
- C. AI app data security posture → DSPM for AI
- D. Create mailboxes → DSPM for AI
- E. Assign Copilot licenses → Communication Compliance

**Correct:** A, B, C  
**Why correct:** Classic Purview tool-to-scenario map.  
**Why distractors fail:** D Exchange; E M365 licensing.  
**Mapped skill:** 2.1 Purview IP/DLP/IRM/Comm Compliance/DSPM/DLM  

---

### Q17. [D2][SC] Copilot ACL rule
User without site access asks Copilot for a confidential file on that site. Expected outcome?

- A. Copilot returns it via tenant super-user Graph rights
- B. Copilot should not return that file as authorized grounding for that user
- C. Copilot license grants Owner on all sites
- D. S/MIME is irrelevant but ACLs never apply to Copilot

**Correct:** B  
**Why correct:** Copilot respects existing permissions via Graph.  
**Why distractors fail:** A/C/D invent bypass.  
**Mapped skill:** 2.2 How Copilot accesses data / Graph  
⚠️ Trap: Copilot does not bypass ACL; license ≠ access.

---

### Q18. [D2][SC] Microsoft Graph role
Best description of Graph for Copilot:

- A. Stores LLM weights for all tenants
- B. API layer retrieving content the user is allowed to access to ground responses
- C. Replaces Entra authentication
- D. Auto-approves custom agents

**Correct:** B  
**Why correct:** Graph supplies permitted org context.  
**Why distractors fail:** A/C/D false.  
**Mapped skill:** 2.2 Microsoft Graph influences Copilot responses  

---

### Q19. [D2][MS] Control planes
**Select 2.** Accurate statements:

- A. M365 permissions are the primary gate for Copilot grounding
- B. Purview labels/DLP can add further constraints
- C. Defender alone is the main fix for Everyone sharing links
- D. Enabling Copilot disables Purview

**Correct:** A, B  
**Why correct:** ACL + Purview (+ Defender for threats). Oversharing ≠ malware-first.  
**Why distractors fail:** C/D traps.  
**Mapped skill:** 2.2 Permissions/controls in M365, Purview, Defender  
⚠️ Trap: Oversharing ≠ malware.

---

### Q20. [D2][SC] Responsible AI
Admin-aligned responsible AI practice:

- A. Hide that AI is involved and skip monitoring
- B. Least privilege, Purview/governance, monitor AI usage, keep humans accountable
- C. Grant Everyone write on all libraries for “better answers”
- D. Let Copilot approve all legal contracts unsupervised

**Correct:** B  
**Why correct:** Maps RAI themes to admin actions and accountability.  
**Why distractors fail:** A/C/D unsafe.  
**Mapped skill:** 2.2 Responsible AI principles  

---

### Q21. [D2][SC] Compliance Manager vs search
Posture recommendations vs finding specific emails for legal — correct pair?

- A. Compliance Manager; Content search
- B. Content search; mailbox creation in Teams
- C. Both only in Copilot Analytics
- D. Both only in Exchange DKIM

**Correct:** A  
**Why correct:** Posture vs content discovery.  
**Why distractors fail:** B/C/D wrong.  
**Mapped skill:** 2.3 Compliance Manager and Content search  
⚠️ Trap: Compliance Manager ≠ eDiscovery.

---

### Q22. [D2][SC] DLP alerts / activity explorer
Investigate recent DLP matches and sensitive info activity. Use:

- A. DLP alerts and activity explorer
- B. Teams holiday UI
- C. SharePoint color palette
- D. PIM only

**Correct:** A  
**Why correct:** Purview investigation surfaces for DLP/sensitive activity.  
**Why distractors fail:** B/C/D wrong.  
**Mapped skill:** 2.3 DLP alerts and activity explorer  

---

### Q23. [D2][SC] DSPM for AI
Need org visibility into AI usage and AI-related data security posture:

- A. DSPM for AI
- B. Exchange journaling alone
- C. Outlook signatures
- D. Entra company branding only

**Correct:** A  
**Why correct:** DSPM for AI targets AI posture/activity.  
**Why distractors fail:** B/C/D wrong class.  
**Mapped skill:** 2.3 DSPM for AI  
⚠️ Trap: Not “DLP only.”

---

### Q24. [D2][SC] Data Explorer
Explore where sensitive content exists to plan labeling:

- A. Data Explorer
- B. Teams dial plans
- C. Defender firewall profiles only
- D. Power Platform currency

**Correct:** A  
**Why correct:** Data Explorer supports sensitive content landscape exploration.  
**Why distractors fail:** B/C/D unrelated.  
**Mapped skill:** 2.3 Data Explorer  

---

### Q25. [D2][SC] IRM vs Comm Compliance
Potential data theft behaviors vs reviewing harassing chat language:

- A. Insider Risk Management; Communication Compliance
- B. Both → SharePoint themes
- C. Both → assign more Copilot seats
- D. Both → Exchange mail tips only

**Correct:** A  
**Why correct:** People-risk vs communication conduct tools.  
**Why distractors fail:** B/C/D miss map.  
**Mapped skill:** 2.3 IRM and Communication Compliance  

---

### Q26. [D2][SC] Oversharing + Copilot
Copilot suddenly surfaces many “secret” files users already had broad link access to. Best remediation framing?

- A. Copilot created new ACLs — uninstall Graph
- B. Remediate SharePoint oversharing (permissions/DAG/Advanced Management); Copilot amplified existing access
- C. Only delete saved prompts to revoke ACLs
- D. Turn off Conditional Access

**Correct:** B  
**Why correct:** Amplification of existing oversharing → SharePoint governance.  
**Why distractors fail:** A/C/D wrong fixes.  
**Mapped skill:** 2.4 Troubleshoot oversharing  

---

### Q27. [D2][SC] DAG reports
Report sites with EveryoneExceptExternal sharing patterns:

- A. Data access governance (DAG) reports
- B. Entra app gallery logos
- C. Teams room displays
- D. Copilot prompt delete-all

**Correct:** A  
**Why correct:** DAG reports are the SharePoint oversharing reporting tool.  
**Why distractors fail:** B/C/D wrong.  
**Mapped skill:** 2.4 Data access governance reports  

---

### Q28. [D2][SC] Advanced Management / RAC
Need advanced SharePoint restricted access control to limit oversharing:

- A. SharePoint Advanced Management / restricted access control (RAC)
- B. Outlook offline mode
- C. Teams dial plans
- D. Azure VM extensions only

**Correct:** A  
**Why correct:** Advanced Management / RAC is the exam-aligned advanced SharePoint control family.  
**Why distractors fail:** B/C/D wrong products.  
**Mapped skill:** 2.4 SharePoint Advanced Management / RAC  

---

### Q29. [D3][SC] Copilot vs custom agent
Need general Word/Outlook AI vs a department onboarding bot grounded on a specific site:

- A. Microsoft 365 Copilot for general productivity; custom agent for the scoped onboarding scenario
- B. Both require only Exchange connectors
- C. Both are Conditional Access policies
- D. Custom agents replace Entra ID

**Correct:** A  
**Why correct:** Copilot vs specialized custom agents.  
**Why distractors fail:** B/C/D nonsense.  
**Mapped skill:** 3.1 Copilot vs agents  

---

### Q30. [D3][SC] Researcher
Deep multi-step research with citations across many sources:

- A. Researcher
- B. Analyst
- C. DAG reports
- D. PIM

**Correct:** A  
**Why correct:** Researcher = deep research + citations.  
**Why distractors fail:** B = data analysis; C/D wrong.  
**Mapped skill:** 3.1 Researcher use cases  
⚠️ Trap: Researcher ≠ Analyst.

---

### Q31. [D3][SC] Analyst
Excel workbook outlier analysis and metric explanations:

- A. Analyst
- B. Researcher only
- C. Content search only
- D. Identity Secure Score

**Correct:** A  
**Why correct:** Analyst fits tabular/Excel-style analysis.  
**Why distractors fail:** B research; C/D wrong.  
**Mapped skill:** 3.1 Analyst use cases  

---

### Q32. [D3][MS] License vs PAYG
**Select 2.** Correct statements:

- A. Monthly Copilot licenses are per-user seats for licensed productivity experiences
- B. PAYG can meter eligible SharePoint agent usage for unlicensed users when configured
- C. PAYG silently replaces all Copilot app experiences for every scenario
- D. No license and no PAYG still allows SharePoint agent create/use for everyone

**Correct:** A, B  
**Why correct:** Seat vs metered SharePoint agent usage model.  
**Why distractors fail:** C/D overclaim.  
**Mapped skill:** 3.1 Monthly license vs PAYG including SharePoint  

---

### Q33. [D3][SC] Feature controls
Block Researcher without assuming all first-party tools disappear when “agents” are broadly disabled:

- A. Use dedicated Researcher allow/block controls
- B. Delete all Entra users
- C. Disable SharePoint Online entirely as the only option
- D. Remove MFA for all users

**Correct:** A  
**Why correct:** Dedicated controls for Researcher/Analyst vs generic agent toggles.  
**Why distractors fail:** B/C/D destructive/wrong.  
**Mapped skill:** 3.1 Enable/disable Copilot features  
⚠️ Trap: Disabling agents ≠ auto-remove Researcher/Analyst.

---

### Q34. [D3][SC] Assign licenses
Assign Microsoft 365 Copilot to a pilot group:

- A. Microsoft 365 admin center
- B. Purview Content search
- C. Defender device timeline only
- D. SharePoint term store

**Correct:** A  
**Why correct:** License assignment is M365 admin.  
**Why distractors fail:** B/C/D wrong.  
**Mapped skill:** 3.2 Assign licenses  

---

### Q35. [D3][SC] PAYG spend
Unlicensed SharePoint agent usage caused unexpected Azure cost. Review:

- A. PAYG billing policies and Azure Cost Management
- B. Teams holiday calendar
- C. Outlook stationery
- D. Entra company branding

**Correct:** A  
**Why correct:** Billing policy + Azure spend monitoring.  
**Why distractors fail:** B/C/D irrelevant.  
**Mapped skill:** 3.2 PAYG billing policies  
⚠️ Trap: Don’t “fix” spend by disabling CA.

---

### Q36. [D3][SC] Adoption insights
Executives want Copilot adoption/impact metrics:

- A. Copilot Analytics (and related M365 usage reports)
- B. Content search alone
- C. PIM role catalog alone
- D. Exchange DKIM alone

**Correct:** A  
**Why correct:** Analytics/adoption ≠ forensic search.  
**Why distractors fail:** B/C/D wrong purpose.  
**Mapped skill:** 3.2 Usage/adoption — Copilot Analytics  
⚠️ Trap: Analytics ≠ license assignment.

---

### Q37. [D3][SC] Prompts
Which is true about prompts?

- A. Users can save/share/schedule/delete prompts as supported; deleting prompts does not remove Copilot licenses
- B. Deleting prompts deletes the user account
- C. Prompt galleries replace DLP
- D. Only Global Admins may enter prompts

**Correct:** A  
**Why correct:** Prompt management vs entitlement controls.  
**Why distractors fail:** B/C/D false.  
**Mapped skill:** 3.2 Manage prompts  
⚠️ Trap: Deleting prompts ≠ revoke Copilot.

---

### Q38. [D3][SC] Agent approval
Maker submitted a custom agent for org Copilot availability. Admin approves where?

- A. Microsoft 365 admin center → Agents → Requests
- B. Exchange mail flow rules only
- C. Defender incidents only
- D. SharePoint recycle bin only

**Correct:** A  
**Why correct:** Agent Registry / requests approval path.  
**Why distractors fail:** B/C/D wrong centers.  
**Mapped skill:** 3.3 Agent approval process  
⚠️ Trap: Create ≠ org-approved.

---

### Q39. [D3][MS] Two-center monitoring
**Select 2.** Monitor Studio agents for store/lifecycle **and** capacity/consumption:

- A. Microsoft 365 admin center
- B. Power Platform admin center
- C. Exchange admin center for all Studio capacity
- D. Teams dial pad for Azure caps

**Correct:** A, B  
**Why correct:** Inventory/approval in M365; studio ops/capacity in Power Platform.  
**Why distractors fail:** C/D wrong.  
**Mapped skill:** 3.3 Monitor agents — M365 + Power Platform  
⚠️ Trap: Two centers often required.

---

### Q40. [D3][SC] Access layers for agents
Users report a published agent is missing. License and PAYG are fine. What else might block access?

- A. Agent allow/block policy, approval/publish state, audience scope, or data permissions — not only licensing
- B. Only missing Exchange litigation hold
- C. Only SharePoint site theme
- D. Only Defender exclusion lists for printers

**Correct:** A  
**Why correct:** Access is layered: entitlement + allow/block + approval/audience + ACLs (+ PP environment policies for studio).  
**Why distractors fail:** B/C/D miss the lifecycle layers.  
**Mapped skill:** 3.3 Configure user access to agents  

---

## Scoring key

| Q# | Answer | Domain |
|----|--------|--------|
| 1 | B | 1 |
| 2 | B | 1 |
| 3 | A | 1 |
| 4 | A, B | 1 |
| 5 | B | 1 |
| 6 | B | 1 |
| 7 | A | 1 |
| 8 | A | 1 |
| 9 | A | 1 |
| 10 | A, D | 1 |
| 11 | A | 1 |
| 12 | A | 1 |
| 13 | A | 2 |
| 14 | A | 2 |
| 15 | A | 2 |
| 16 | A, B, C | 2 |
| 17 | B | 2 |
| 18 | B | 2 |
| 19 | A, B | 2 |
| 20 | B | 2 |
| 21 | A | 2 |
| 22 | A | 2 |
| 23 | A | 2 |
| 24 | A | 2 |
| 25 | A | 2 |
| 26 | B | 2 |
| 27 | A | 2 |
| 28 | A | 2 |
| 29 | A | 3 |
| 30 | A | 3 |
| 31 | A | 3 |
| 32 | A, B | 3 |
| 33 | A | 3 |
| 34 | A | 3 |
| 35 | A | 3 |
| 36 | A | 3 |
| 37 | A | 3 |
| 38 | A | 3 |
| 39 | A, B | 3 |
| 40 | A | 3 |

**Domain totals:** Domain 1 = Q1–12 (12) · Domain 2 = Q13–28 (16) · Domain 3 = Q29–40 (12)

**Score:** ___ / 40 · **%:** ___ · **Pass practice bar:** ≥32/40 (≥80%)

**Weak-area follow-up**

| If you missed… | Drill |
|----------------|-------|
| Q1–4, admin centers | [`domain-1-questions.md`](./domain-1-questions.md) + [`admin-centers-cheatsheet.md`](../topics_details/reference/admin-centers-cheatsheet.md) |
| Q5–12, identity/Zero Trust | Domain 1 bank + topics 02–03 |
| Q13–28, Purview/Graph/oversharing | [`domain-2-questions.md`](./domain-2-questions.md) + [`exam-traps.md`](../topics_details/reference/exam-traps.md) |
| Q29–40, Copilot/agents | [`domain-3-questions.md`](./domain-3-questions.md) + topics 08–10 |
