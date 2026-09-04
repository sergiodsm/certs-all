# AB-900 Glossary

Short admin-oriented definitions for Exam **AB-900** (skills as of **July 22, 2026**). Prefer Microsoft Learn for the latest product wording.

| Term | Definition |
|------|------------|
| **Activity explorer** | Purview view of labeled/classified content activities and related user actions for investigation and governance. |
| **Analyst** | First-party Microsoft 365 Copilot agent optimized for **data / Excel-style analysis** (tabular exploration, quantitative reasoning). Not a substitute for Researcher. |
| **App registrations** | Entra ID objects representing apps you develop/register; define identity, permissions (API scopes), and credentials for sign-in and Graph access. |
| **Authentication** | Proving identity (who you are) — passwords, MFA, passkeys, certificate, etc. |
| **Authorization** | What an authenticated identity is allowed to do (roles, permissions, Conditional Access grant controls). |
| **Compliance Manager** | Purview solution that scores compliance posture and tracks improvement actions/recommendations against regulations and standards. |
| **Conditional Access (CA)** | Entra policy engine: if signal conditions match, require controls (MFA, compliant device, block, etc.) before access. |
| **Content search** | Purview eDiscovery tool to search mailboxes, sites, and other locations for files/emails during investigations. |
| **Copilot Analytics** | Adoption and impact analytics for Microsoft 365 Copilot (e.g. Copilot Dashboard via Viva Insights) beyond basic admin-center charts. |
| **Custom agents** | Org-built agents (Agent Builder, Copilot Studio, SharePoint agents, etc.) with instructions, knowledge, and skills for a business scenario; usually need admin approval for broad Copilot availability. |
| **DAG report** | **Data access governance** report in SharePoint — surfaces oversharing / broad access patterns for governance remediation. |
| **Data Explorer** | Purview capability to explore and identify sensitive information across the estate for risk awareness. |
| **Defender XDR** | Microsoft Defender extended detection and response — correlates signals across endpoints, identities, email, cloud apps for threat protection. |
| **DLM** | **Data Lifecycle Management** (Purview) — retention/deletion governance for content (retain, delete, or both) per policy. |
| **DLP** | **Data Loss Prevention** — policies that detect and protect sensitive information (block, warn, encrypt, alert) across locations. |
| **DSPM for AI** | **Data Security Posture Management for AI** — discover and manage AI activity/risk posture (not “generic DLP only”). |
| **Enterprise apps** | Entra gallery/registered applications used in the tenant for SSO and assignment; the admin view of apps consuming directory identities. |
| **Entra (Microsoft Entra ID)** | Cloud identity and access directory (formerly Azure AD): users, groups, apps, Conditional Access, PIM, Secure Score, sign-in logs. |
| **Graph (Microsoft Graph)** | Unified API/data fabric Copilot uses to ground responses in work data the user is permitted to access (mail, files, chats, etc.). |
| **Insider Risk Management (IRM)** | Purview solution to detect risky user activities (exfiltration patterns, etc.) using signals and policies — people-risk focused. |
| **Information Protection (IP)** | Purview capabilities to classify and protect data (sensitivity labels, encryption, marking) across M365 and beyond. |
| **Communication Compliance** | Purview policies to detect regulatory/conduct issues in communications (harassment, threat, sensitive sharing patterns, etc.). |
| **PAYG** | **Pay-as-you-go** metered billing (Azure-backed) for eligible Copilot agent/chat consumption — especially SharePoint agents for unlicensed users. |
| **PIM** | **Privileged Identity Management** — just-in-time, time-bound privileged role activation with approval/MFA as configured; not “MFA for all users.” |
| **RAC** | **Restricted Access Control** (SharePoint Advanced Management) — limits who can access SharePoint/OneDrive content beyond ordinary sharing mistakes. |
| **Researcher** | First-party Copilot agent for **deep, multi-step research** with citations across work (and optionally web) sources. Not Analyst. |
| **Retention** | Policies/labels that keep or delete content for a period to meet legal/compliance needs (lifecycle), distinct from sensitivity labels. |
| **Sensitivity labels** | Classification + protection labels (visual marking, encryption, access restrictions) applied to documents/emails/containers. |
| **SharePoint Advanced Management** | Advanced SharePoint governance toolkit (including reporting and controls such as restricted access control) to reduce oversharing risk. |
| **SSO** | **Single sign-on** — authenticate once to access multiple apps via a trusted identity provider (Entra). |
| **Zero Trust** | Security model: verify explicitly, least privilege, assume breach — never trust by network location alone. |

## Quick disambiguation

| Confused pair | Remember |
|---------------|----------|
| Sensitivity label vs DLP | Label **classifies/protects**; DLP **detects/restricts sharing** of sensitive info |
| IRM vs DLP | IRM = **user risk** patterns; DLP = **data** exfil/policy on content |
| DSPM for AI vs DLP | DSPM for AI = **AI posture/activity**; DLP = broader sensitive-data controls |
| PIM vs MFA | PIM = **privileged JIT access**; MFA = authentication factor (often required by CA for everyone) |
| App registration vs Enterprise app | Registration = **app identity definition**; Enterprise app = **tenant instance / assignment** |
| Copilot Analytics vs Purview audit | Analytics = **adoption/impact**; audit = **who did what** for compliance |
| Researcher vs Analyst | Research synthesis vs **data/Excel** analysis |
| Monthly license vs PAYG | Seat for Copilot features vs **metered** eligible agent usage |
