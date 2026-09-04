# Domain 3 practice — Copilot and agent administration

**Exam:** AB-900 · Microsoft 365 Copilot and Agent Administration Fundamentals  
**Weight:** 25–30% · Skills measured as of **July 22, 2026**  
**Coverage:** Topics 08–10 (features/licensing, Copilot admin tasks, agent lifecycle)

**How to use:** Memorize license vs PAYG, Researcher vs Analyst vs custom, and the access → create → **approve** → monitor path across **M365 + Power Platform** admin centers. Cover answers while practicing. **Unofficial study aids** — not exam dumps.

**Question types:** single-choice · multi-select · which admin center / capability

---

### Q1. Copilot vs agents
A department wants everyday AI help drafting email and summarizing meetings across Microsoft 365 apps. Separately, they want a specialized HR policy helper grounded on an HR SharePoint site. How should an admin classify these needs?

- A. Both are only solved by disabling web grounding
- B. General productivity → Microsoft 365 Copilot; specialized scoped helper → a custom agent
- C. Both require Exchange mail flow rules
- D. Specialized helpers must be built only as Conditional Access policies

**Correct:** B  
**Why correct:** Copilot covers broad work productivity; agents extend Copilot for focused scenarios with instructions/knowledge (custom agents for org-specific cases).  
**Why distractors fail:** A/C/D misuse unrelated controls.  
**Mapped skill:** 3.1 Compare built-in capabilities of Copilot and agents  

---

### Q2. Researcher use case
A strategy analyst needs multi-step research across many work documents and (if enabled) the web, with structured findings and citations. Which first-party capability fits best?

- A. Analyst
- B. Researcher
- C. SharePoint site theme
- D. PIM role activation

**Correct:** B  
**Why correct:** Researcher is the deep, multi-step research agent with citations — not spreadsheet modeling.  
**Why distractors fail:** A is data/Excel-style analysis; C/D are unrelated.  
**Mapped skill:** 3.1 Identify use cases for Researcher  
⚠️ Trap: Researcher ≠ Analyst.

---

### Q3. Analyst use case
Finance users want Copilot help exploring an Excel workbook, finding outliers, and explaining metric trends. Which capability fits best?

- A. Analyst
- B. Researcher only
- C. Communication Compliance
- D. Data access governance reports

**Correct:** A  
**Why correct:** Analyst is oriented to tabular/quantitative and Excel-style analysis.  
**Why distractors fail:** B is literature-style deep research; C/D are Purview/SharePoint governance tools.  
**Mapped skill:** 3.1 Identify use cases for Analyst  

---

### Q4. Monthly license vs PAYG
Unlicensed users need to **use** SharePoint agents on a project site. Licensed makers will still create agents. Which billing approach enables unlicensed usage?

- A. Identity Secure Score only
- B. Pay-as-you-go (PAYG) billing with an appropriate billing policy / Azure subscription linkage
- C. Disabling Conditional Access tenant-wide
- D. Assigning Exchange Online Archiving alone

**Correct:** B  
**Why correct:** PAYG meters eligible agent usage (notably SharePoint agents for unlicensed users) when configured with Azure + billing policy; monthly seats cover licensed Copilot productivity.  
**Why distractors fail:** A/C/D do not meter SharePoint agent usage for unlicensed users.  
**Mapped skill:** 3.1 Compare monthly license model to pay-as-you-go, including SharePoint  
⚠️ Trap: PAYG is not a silent full replacement for every licensed Copilot capability.

---

### Q5. SharePoint agents entitlement (multi-select)
**Select 2.** Which statements about SharePoint agents are accurate?

- A. With no Copilot license and no PAYG, users generally cannot create or use SharePoint agents
- B. Creating SharePoint agents typically requires a Copilot license for the maker
- C. Approving an agent in M365 admin grants all users Owner on the site
- D. PAYG always replaces the need for any Microsoft 365 base licenses

**Correct:** A, B  
**Why correct:** Entitlement matrix: neither → no access; create usually needs Copilot license; use can be license or PAYG. Approval does not widen ACLs; PAYG does not erase base licensing needs.  
**Why distractors fail:** C/D invent capabilities.  
**Mapped skill:** 3.1 Monthly license vs PAYG including SharePoint  

---

### Q6. Enable/disable features
An admin wants to block Researcher for the tenant but keep other Copilot experiences available. Which approach aligns with exam guidance?

- A. Use dedicated allow/block controls for Researcher; do not assume “disable all agents” removes Researcher/Analyst from core Tools
- B. Delete all user mailboxes
- C. Turn off Entra ID entirely
- D. Remove all SharePoint sites

**Correct:** A  
**Why correct:** First-party tools like Researcher/Analyst have dedicated admin controls; broadly disabling “agents” is not the same switch.  
**Why distractors fail:** B/C/D are destructive and irrelevant.  
**Mapped skill:** 3.1 Identify which Copilot features can be enabled or disabled  
⚠️ Trap: Disabling “agents” does not automatically remove Researcher/Analyst.

---

### Q7. Assign Copilot licenses
IT needs to give Microsoft 365 Copilot to a pilot security group. Where is license assignment primarily performed?

- A. Microsoft 365 admin center
- B. Microsoft Purview Content search
- C. SharePoint theme gallery
- D. Defender hunting advanced queries only

**Correct:** A  
**Why correct:** Copilot seat assignment is an M365 admin center licensing task.  
**Why distractors fail:** B/C/D are wrong centers for seat assignment.  
**Mapped skill:** 3.2 Assign licenses  

---

### Q8. PAYG billing policy
Finance reports unexpected Azure charges after SharePoint agent usage by unlicensed users. What should the admin review first for metering controls?

- A. Copilot / PAYG billing policies (M365) and Azure Cost Management
- B. Teams holiday calendars
- C. Outlook signature HTML only
- D. Entra custom banned password list only

**Correct:** A  
**Why correct:** PAYG spend is managed via billing policy configuration (from M365 Copilot cost/billing experiences) and monitored in Azure Cost Management.  
**Why distractors fail:** B/C/D do not control agent metering.  
**Mapped skill:** 3.2 Manage pay-as-you-go billing policies  
⚠️ Trap: High PAYG spend → billing limits/scope (or seats) — not “turn off Conditional Access.”

---

### Q9. Usage and adoption
Leadership wants impact and adoption insights for Copilot — not a forensic audit of a single DLP incident. Which experience is the best fit?

- A. Copilot Analytics (adoption/impact dashboards)
- B. Purview Content search alone
- C. Exchange message recall only
- D. PIM eligible role catalog only

**Correct:** A  
**Why correct:** Copilot Analytics / related admin usage reports measure adoption and impact; audit/search serve investigation.  
**Why distractors fail:** B/C/D are not adoption dashboards.  
**Mapped skill:** 3.2 Manage usage and adoption with Copilot Analytics / M365 admin center  
⚠️ Trap: Copilot Analytics ≠ license assignment; audit log ≠ adoption dashboard.

---

### Q10. Manage prompts
A user asks how prompts work in Copilot experiences. Which admin-relevant statement is correct?

- A. Users can save, share, schedule, and delete prompts as supported by the product; deleting prompts does not revoke Copilot licensing
- B. Deleting a saved prompt permanently removes the user’s Microsoft 365 account
- C. Prompt galleries replace Conditional Access
- D. Only Global Admins may type prompts

**Correct:** A  
**Why correct:** Prompt management (save/share/schedule/delete) is a user/productivity admin awareness topic; license/feature/agent controls govern access — not prompt deletion alone.  
**Why distractors fail:** B/C/D invent false effects.  
**Mapped skill:** 3.2 Manage prompts  
⚠️ Trap: Deleting prompts does not revoke Copilot.

---

### Q11. Agent approval path
A maker built a custom agent and submitted it for organization-wide availability in Copilot. Where does an admin typically approve or publish the request?

- A. Microsoft 365 admin center → Agents → Requests (Agent Registry)
- B. Exchange admin center → Mail flow → Connectors only
- C. Defender portal → Incidents only
- D. SharePoint admin center → Term store only

**Correct:** A  
**Why correct:** Custom agent store/org publish path goes through M365 admin Agents / requests approval — not Defender or Exchange.  
**Why distractors fail:** B/C/D are wrong ownership.  
**Mapped skill:** 3.3 Understand the approval process for agents  
⚠️ Trap: Create ≠ approved for org.

---

### Q12. Monitor agents across two centers (multi-select)
**Select 2.** An admin must monitor custom Copilot Studio agents for org inventory/approval state and for environment capacity/consumption. Which centers are both typically required?

- A. Microsoft 365 admin center (Agent Registry / lifecycle, allow/block, requests)
- B. Power Platform admin center (environments, studio governance, capacity/consumption analytics)
- C. Exchange admin center for all Studio message packs
- D. Teams dial pad configuration for Azure spend caps

**Correct:** A, B  
**Why correct:** Lifecycle story uses **both** M365 (inventory/approval) and Power Platform (studio ops/capacity).  
**Why distractors fail:** C/D misassign ownership.  
**Mapped skill:** 3.3 Monitor agents via Microsoft 365 and Power Platform admin centers  
⚠️ Trap: Monitoring agents can need two centers — stem saying both is a hint.

---

### Domain 3 answer key

| Q# | Answer | Focus |
|----|--------|--------|
| 1 | B | Copilot vs agents |
| 2 | B | Researcher |
| 3 | A | Analyst |
| 4 | B | PAYG |
| 5 | A, B | SharePoint agents entitlement |
| 6 | A | Feature enable/disable |
| 7 | A | Assign licenses |
| 8 | A | PAYG billing |
| 9 | A | Copilot Analytics |
| 10 | A | Manage prompts |
| 11 | A | Agent approval |
| 12 | A, B | M365 + Power Platform monitor |

**Suggested pass bar:** ≥10/12. Revisit [`08`](../topics_details/08-copilot-features-licensing.md)–[`10`](../topics_details/10-agent-admin-lifecycle.md).
