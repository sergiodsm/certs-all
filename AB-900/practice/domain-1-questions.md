# Domain 1 practice — Core features and objects of Microsoft 365

**Exam:** AB-900 · Microsoft 365 Copilot and Agent Administration Fundamentals  
**Weight:** 30–35% · Skills measured as of **July 22, 2026**  
**Coverage:** Topics 01–03 (admin centers/objects, Zero Trust, Entra identity & access)

**How to use:** Cover the **Correct / Why** blocks (or scroll past them) and answer closed-book first. These are **unofficial study aids** — not Microsoft exam dumps. Prefer GA behaviors from the official study guide.

**Question types:** single-choice · multi-select · which admin center / tool

---

### Q1. New hire mailbox ownership
An admin needs to create a mailbox and a distribution group for a new department. Which admin center should they use?

- A. SharePoint admin center
- B. Teams admin center
- C. Exchange admin center
- D. Microsoft Purview portal

**Correct:** C  
**Why correct:** Mailboxes and distribution groups are Exchange Online recipient objects managed in the Exchange admin center.  
**Why distractors fail:** A manages sites/libraries; B manages teams, channels, and Teams policies; D is for protection, retention, and compliance tools — not mailbox creation.  
**Mapped skill:** 1.1 Identify objects in the Exchange admin center  

---

### Q2. Site library permissions
Users report they cannot upload files to a department document library even though they can open the SharePoint site home page. Which admin center is the primary place to investigate site roles and library permissions?

- A. Exchange admin center
- B. SharePoint admin center
- C. Microsoft Defender portal
- D. Power Platform admin center

**Correct:** B  
**Why correct:** Sites, libraries, folders, and site permission models are owned by SharePoint administration.  
**Why distractors fail:** A is mail-centric; C is threat protection; D governs Power Platform environments and Copilot Studio ops — not SharePoint library ACLs.  
**Mapped skill:** 1.1 Identify objects in the SharePoint admin center  

---

### Q3. Teams messaging policy
An admin needs to restrict who can create private channels and apply a messaging policy for a pilot group. Where should they configure this?

- A. Microsoft 365 admin center → Domains
- B. Teams admin center
- C. SharePoint admin center → Active sites
- D. Entra admin center → Conditional Access

**Correct:** B  
**Why correct:** Teams, channels, and Teams policies (messaging, meeting, apps, etc.) are managed in the Teams admin center.  
**Why distractors fail:** A is org/domain settings; C is site inventory, not Teams channel policy; D enforces identity access conditions, not Teams messaging policy.  
**Mapped skill:** 1.1 Identify objects in the Teams admin center  

---

### Q4. License and domain settings (multi-select)
**Select 2.** An organization onboarding Microsoft 365 needs to complete foundational tenant setup. Which tasks are primarily done in the **Microsoft 365 admin center**?

- A. Assign Microsoft 365 licenses to users or groups
- B. Author a sensitivity label encryption policy
- C. Manage custom domain names and org settings
- D. Create a Conditional Access policy requiring MFA
- E. Hunt a cross-workload malware incident in XDR

**Correct:** A, C  
**Why correct:** The M365 admin center is the home for licenses, domains, and org-level settings (and later Copilot license/agent admin entry points).  
**Why distractors fail:** B is Purview Information Protection; D is Entra Conditional Access; E is Microsoft Defender.  
**Mapped skill:** 1.1 Identify objects in the Microsoft 365 admin center  
⚠️ Trap: Don’t send every “tenant setup” task to M365 admin — identity CA and Purview labels live elsewhere.

---

### Q5. Zero Trust principle
Leadership asks how Zero Trust should guide Copilot rollout. Which statement best reflects Zero Trust principles?

- A. Trust the corporate network; skip MFA for on-premises users
- B. Verify explicitly, use least privilege, and assume breach
- C. Buy a single security product that replaces all other controls
- D. Grant Global Admin to all help desk staff for faster support

**Correct:** B  
**Why correct:** Zero Trust is a set of principles — verify explicitly, least privilege, assume breach — implemented with many layered controls.  
**Why distractors fail:** A contradicts verify explicitly; C treats Zero Trust as a single SKU; D violates least privilege.  
**Mapped skill:** 1.2 Describe Zero Trust principles  
⚠️ Trap: Zero Trust ≠ “buy one product.”

---

### Q6. Authentication vs authorization
Users report they completed MFA successfully but still cannot open a SharePoint site. Which statement best explains the situation?

- A. Authentication failed; MFA never proves identity
- B. Authentication succeeded; authorization (permissions/roles) is likely blocking access
- C. SSO always grants SharePoint Owner rights after MFA
- D. Conditional Access cannot apply after successful MFA

**Correct:** B  
**Why correct:** Authentication proves who the user is (here MFA succeeded); authorization decides what they can access — site membership/permissions may still deny them.  
**Why distractors fail:** A contradicts the stem; C invents an SSO privilege grant; D is false — CA can still evaluate sessions/controls beyond the MFA prompt.  
**Mapped skill:** 1.2 Describe authorization and authentication methods  

---

### Q7. Defender XDR vs oversharing
Security reports that many SharePoint links are shared with “Everyone except external users,” and Copilot is surfacing those files to broad audiences. Which tool is the **best first fit** for threat hunting malware across email, identity, and endpoints?

- A. SharePoint Data access governance (DAG) reports
- B. Microsoft Defender XDR
- C. Communication Compliance
- D. Copilot Analytics

**Correct:** B  
**Why correct:** Defender XDR correlates threat protection and intelligence across security workloads — the exam’s home for malware/phishing/incident-style scenarios.  
**Why distractors fail:** A and C address governance/oversharing or communication conduct — important but not XDR threat hunting; D measures Copilot adoption/impact.  
**Mapped skill:** 1.2 Describe Microsoft Defender XDR capabilities  
⚠️ Trap: Oversharing is governance (SharePoint/Purview), not “run Defender malware scan first” — this stem asks specifically for XDR.

---

### Q8. Conditional Access and SSO
An admin needs to require MFA when users access Microsoft 365 from untrusted locations, while keeping single sign-on to SaaS apps. Which Entra capability primarily enforces the MFA condition?

- A. Privileged Identity Management (PIM)
- B. Conditional Access
- C. Identity Secure Score recommendations only
- D. App registration client secrets

**Correct:** B  
**Why correct:** Conditional Access evaluates signals (user, device, location, risk) and enforces controls such as MFA. SSO reduces sign-in friction across apps; CA adds the conditions.  
**Why distractors fail:** A is JIT privileged role elevation; C is a posture score, not the enforcement engine; D is app credential config, not workforce MFA policy.  
**Mapped skill:** 1.3 Describe Conditional Access and SSO  
⚠️ Trap: SSO is not Conditional Access — they solve different problems.

---

### Q9. Risky sign-in troubleshooting
Users report intermittent sign-in failures. Sign-in logs show some attempts flagged as risky and blocked. Which admin center should the admin use to investigate risky sign-ins and related identity signals?

- A. Exchange admin center
- B. Teams admin center
- C. Microsoft Entra admin center
- D. SharePoint admin center

**Correct:** C  
**Why correct:** Users/groups, Conditional Access, MFA registration, risky sign-ins, and identity logs are Entra identity surfaces.  
**Why distractors fail:** A/B/D own mail, Teams policies, and sites — not identity risk investigation.  
**Mapped skill:** 1.3 Troubleshoot identity and access, including MFA, Conditional Access, and risky sign-ins  

---

### Q10. PIM vs day-to-day MFA (multi-select)
**Select 2.** Which statements correctly describe Privileged Identity Management (PIM)?

- A. PIM provides just-in-time elevation for privileged directory roles
- B. PIM replaces Conditional Access MFA for all standard users
- C. Eligible admins activate roles when needed instead of standing permanent Global Admin
- D. PIM is configured primarily in the SharePoint admin center
- E. PIM is only used to assign Microsoft 365 Copilot licenses

**Correct:** A, C  
**Why correct:** PIM is for privileged access — eligible/JIT activation rather than always-on highly privileged roles.  
**Why distractors fail:** B confuses PIM with workforce MFA/CA; D wrong center (Entra); E is M365 license assignment, unrelated to PIM.  
**Mapped skill:** 1.3 Describe Privileged Identity Management  
⚠️ Trap: PIM ≠ MFA for everyone.

---

### Q11. Identity Secure Score and audit
Compliance asks for a prioritized list of identity posture improvements and evidence of recent admin changes to Conditional Access. Which pair of Entra-related capabilities fits best?

- A. Identity Secure Score and Entra audit / sign-in logs
- B. Copilot Analytics and SharePoint DAG reports
- C. Defender Secure Score only and Exchange mail flow rules
- D. Purview Content search and Teams messaging policies

**Correct:** A  
**Why correct:** Identity Secure Score surfaces identity improvement actions; audit/sign-in logs support investigation of configuration and authentication events.  
**Why distractors fail:** B is adoption/oversharing; C mixes scores/workloads incorrectly for this stem; D is eDiscovery + Teams policy — not identity posture.  
**Mapped skill:** 1.3 Describe Identity Secure Score and audit logs  

---

### Q12. App registration vs enterprise app
A developer registers a new line-of-business app that will use Microsoft Graph. The identity admin must later assign users and configure SSO for that app in the tenant. Which statement is most accurate?

- A. App registration and Enterprise application are identical objects with different UI names
- B. App registration defines the application identity; the Enterprise application is the tenant’s instance used for assignment and SSO
- C. Enterprise applications are created only in the Exchange admin center
- D. App registrations replace Conditional Access for all cloud apps

**Correct:** B  
**Why correct:** At fundamentals level: app registration = app identity definition; enterprise app = tenant instance for permissions, assignment, and SSO.  
**Why distractors fail:** A treats them as interchangeable; C wrong center; D invents a CA replacement.  
**Mapped skill:** 1.3 Describe app registrations and enterprise applications  
⚠️ Trap: App registration ≠ Enterprise app (interchangeable).

---

### Domain 1 answer key

| Q# | Answer | Focus |
|----|--------|--------|
| 1 | C | Exchange — mailboxes/DGs |
| 2 | B | SharePoint — sites/libraries |
| 3 | B | Teams — policies/channels |
| 4 | A, C | M365 admin — licenses/domains |
| 5 | B | Zero Trust principles |
| 6 | B | AuthN vs AuthZ |
| 7 | B | Defender XDR |
| 8 | B | Conditional Access |
| 9 | C | Entra risky sign-ins |
| 10 | A, C | PIM |
| 11 | A | Identity Secure Score + logs |
| 12 | B | App reg vs enterprise app |

**Suggested pass bar:** ≥10/12 before moving on. Revisit [`../topics_details/01-m365-objects-admin-centers.md`](../topics_details/01-m365-objects-admin-centers.md), [`02`](../topics_details/02-security-principles-zero-trust.md), [`03`](../topics_details/03-entra-identity-access.md).
