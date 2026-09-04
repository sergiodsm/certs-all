# 03 — Entra Identity & Access

**Domain:** 1.3 Identify the core security features of Microsoft 365 services (part of **30–35%**)  
**Skills measured as of:** July 22, 2026

---

## 1. Official bullets covered

- Understand features and capabilities of **Microsoft Entra ID**  
- Understand **Conditional Access** policies  
- Understand the purpose and benefits of **SSO**  
- Identify the appropriate security object to use (**users** and **groups**)  
- Identify tools to troubleshoot common sign-in issues (**MFA**, **Conditional Access**, **risky sign-ins**)  
- Interpret **Identity Secure Score** in Microsoft Entra ID  
- Use appropriate tools to review **audit logs** for user and admin activity  
- Identify the role of **Privileged Identity Management (PIM)**  
- Understand **App registrations** and **Enterprise apps**

---

## 2. Why it matters on the exam

Identity is the control plane for Microsoft 365 and Copilot: no correct Entra configuration means no reliable access decisions. AB-900 tests whether you pick the right **object** (user vs group), the right **control** (MFA vs Conditional Access vs PIM), and the right **log** when sign-in fails. App registration vs Enterprise application is a classic fundamentals trap. Strong Domain 1.3 performance also supports Domain 2 reasoning: Copilot and Graph calls run as the signed-in user under these same identity rules.

---

## 3. Core concepts

### Microsoft Entra ID

**Microsoft Entra ID** (formerly Azure AD) is the cloud identity and access management directory for Microsoft 365.

Core capabilities (fundamentals):

| Capability | What it gives you |
|------------|-------------------|
| Directory of users, groups, devices | Identity objects for M365 |
| Authentication | Sign-in, MFA, passwordless methods |
| SSO to SaaS and Microsoft apps | One identity, many apps |
| Conditional Access | Adaptive access policies |
| Roles & admin units | Delegated administration |
| App registrations / enterprise apps | Application identity and assignments |
| Identity protection / risk | Risky users and sign-ins (license-dependent features) |
| Identity Secure Score | Improvement recommendations |
| Audit & sign-in logs | Who did what / who signed in |

Admin center: **Microsoft Entra admin center** (`entra.microsoft.com`) — also reachable from Microsoft 365 admin center identity blades.

### Users and groups (security objects)

| Object | Use when |
|--------|----------|
| **User** | Individual human (or some service scenarios); license assignment target; sign-in identity |
| **Security group** | Grant access to resources; assign licenses (group-based); assign CA policies; role-assignable groups where applicable |
| **Microsoft 365 group** | Collaboration (mailbox, site, Teams) plus membership |
| **Distribution list** | Email fan-out (Exchange) — weak choice as *security* object for resource ACL |
| **Dynamic group** | Membership from rules (department, title) — scales better than manual lists |

**Exam rule:** Prefer **groups** for access assignment at scale; use **users** for individual exceptions, licensing one-offs, or troubleshooting a single identity.

### Single sign-on (SSO)

**SSO** = authenticate once to Entra, then access multiple applications without separate passwords for each app.

Benefits:

- Fewer passwords → fewer resets and weaker reuse  
- Centralized Conditional Access / MFA enforcement  
- Faster user experience across M365 and integrated SaaS  
- Central disable/offboarding when employment ends  

SSO is an **outcome of federation / modern app protocols** (SAML, OIDC/OAuth) with Entra — not a SharePoint permission setting.

### Conditional Access (CA)

**Conditional Access** = policy engine: *when these signals match, require these controls or block access*.

Typical building blocks:

| Part | Examples |
|------|----------|
| **Assignments** | Users/groups, guest types, directory roles |
| **Cloud apps / actions** | Office 365, Exchange, SharePoint, admin portals, all cloud apps |
| **Conditions** | Sign-in risk, user risk, device platform, location, client apps |
| **Grant controls** | Require MFA, compliant device, hybrid joined, password change, block |
| **Session controls** | Limited experience / frequency (where applicable) |

**Exam rule:** CA decides *whether and how* a session is allowed. It does not replace SharePoint ACLs or Exchange mailbox permissions.

### MFA in troubleshooting context

MFA challenges can fail because:

- Method not registered  
- User denied the Authenticator prompt  
- Policy requires a method the user doesn’t have  
- Legacy authentication client cannot complete MFA  
- CA policy newly enforced without user registration window  

### Risky sign-ins / Identity Protection signals

**Risky sign-ins** and **risky users** flag anomalous authentication (unfamiliar location, atypical travel, malware-linked IP, leaked credentials — feature availability depends on licensing).

Admins investigate in Entra Identity Protection / risk reports and may require password reset, MFA, or block via CA based on risk level.

### Identity Secure Score

**Identity Secure Score** (in Entra) scores identity posture and recommends improvements (e.g., enable MFA, block legacy auth, use PIM, restrict admin consent).

Use it to **prioritize hardening**, not as a real-time incident queue. Separately, Microsoft Secure Score in Defender covers a broader security posture — don’t confuse the two names on the exam if both appear.

### Audit logs vs sign-in logs

| Log | Answers |
|-----|---------|
| **Sign-in logs** | Did authentication succeed/fail? Which CA policies applied? MFA result? Client app? Location? |
| **Audit logs** | What directory *change* happened? Who created a user, updated a group, consented an app, changed a CA policy? |

Both live in Entra monitoring. Unified audit log in Purview covers broader M365 workload activities (Domain 2) — for **identity directory** changes and **sign-ins**, start in Entra.

### Privileged Identity Management (PIM)

**PIM** provides **just-in-time** privileged access:

- Make admin roles **eligible** instead of permanently **active**  
- Require activation (MFA, justification, approval, time-limited)  
- Access reviews of privileged roles  
- Reduces standing admin risk (Zero Trust least privilege)

**PIM ≠ MFA for all users.** MFA is broad authentication strength; PIM is for **privileged roles**.

### App registrations vs Enterprise applications

| | **App registration** | **Enterprise application** |
|--|----------------------|------------------------------|
| What it is | Application’s identity definition (client ID, credentials, redirect URIs, API permissions requested) | The **instance** of an app in *your tenant* (service principal) used for SSO, assignment, and consent |
| Typical question | “Register a custom app / configure permissions & secrets” | “Assign users/groups to the app / configure SSO / see who has access” |
| Relationship | Creating an app registration in your tenant also creates a corresponding enterprise app (service principal) | Gallery / multi-tenant apps appear as enterprise apps when added/consented |

**Short memory aid:** *Registration = blueprint of the app. Enterprise app = how that app shows up and is assigned in your directory.*

---

## 4. How it works (admin-center oriented)

### A. Day-to-day identity objects

1. Create **users** (cloud-only or synced from on-premises).  
2. Add users to **groups** for licenses and access.  
3. Assign Microsoft 365 licenses (often via group-based licensing).  
4. Users access apps via **SSO** to M365 workloads.  
5. Harden with CA + MFA; elevate admins via **PIM**.

### B. Conditional Access policy reasoning

```text
IF user in Finance
AND cloud app = Exchange Online
AND location = outside trusted countries
THEN grant = require MFA
ELSE IF sign-in risk = high
THEN block
```

Admin path: Entra admin center → Protection → Conditional Access → Policies.

### C. Troubleshoot sign-in (exam workflow)

| Symptom | First places to look |
|---------|----------------------|
| “MFA required / failed” | Sign-in log → Authentication details / MFA result; Authentication methods registration |
| “Blocked by Conditional Access” | Sign-in log → **Conditional Access** tab — which policy failed |
| “Unusual / risky activity” | Risky sign-ins / risky users reports; Identity Protection |
| User exists but apps missing | Licenses / group membership (Topic 01) after confirming AuthN success |
| Admin action disputed | **Audit logs** — who changed CA, roles, or group membership |

**Order:** Confirm identity exists → read **sign-in log** → classify MFA vs CA vs risk → fix registration/policy/risk → only then chase app/license issues if sign-in succeeded.

### D. PIM activation (conceptual)

1. Admin is **eligible** for Exchange Administrator.  
2. Activates role in PIM for 2 hours with MFA + justification.  
3. Performs mail tasks.  
4. Access expires — least privilege restored.

### E. Apps

1. Developer/admin creates **App registration** (permissions, secrets/certificates, redirect URIs).  
2. Admin grants **admin consent** if required.  
3. **Enterprise application** shows in tenant; assign users/groups; configure SSO (SAML/OIDC).  
4. CA can target that enterprise app like any other cloud app.

---

## 5. Compare / choose

### User vs group

| Scenario | Choose |
|----------|--------|
| One contractor needs temporary Teams access | User (plus time-bound group membership preferred) |
| Entire department needs the same SharePoint site + license | **Security / M365 group** |
| Email-only announcement list | Distribution list (not primary security object) |
| CA policy for all finance staff | **Group** assignment in CA |

### MFA vs Conditional Access vs PIM

| Need | Control |
|------|---------|
| Second factor at sign-in | **MFA** (often enforced *through* CA) |
| “MFA only outside office / only for Admins / block legacy” | **Conditional Access** |
| Temporary Global Admin elevation | **PIM** |
| Improve posture recommendations | **Identity Secure Score** |

### Sign-in logs vs audit logs

| Question | Log |
|----------|-----|
| Why was Alex blocked at 09:14? | **Sign-in logs** |
| Who added Alex to Global Administrator yesterday? | **Audit logs** |
| Which CA policy failed? | **Sign-in logs** → CA tab |
| Who consented to a new enterprise app? | **Audit logs** |

### App registration vs Enterprise app

| Task | Object |
|------|--------|
| Create client ID and redirect URI for a custom LOB app | **App registration** |
| Assign “Sales” group to Salesforce SSO | **Enterprise application** |
| Configure API permissions / expose an API | **App registration** |
| See which users can launch the app | **Enterprise application** (users and groups) |

### SSO vs Conditional Access

| | SSO | Conditional Access |
|--|-----|--------------------|
| Goal | Convenience + central identity | Adaptive security decisions |
| Alone enough? | No — still need AuthZ and often MFA/CA | No — apps still need SSO/integration and permissions |

---

## 6. Exam traps

- ⚠️ **PIM is not MFA for everyone** — it manages privileged role activation.  
- ⚠️ **CA failure ≠ wrong SharePoint role** — check sign-in logs’ Conditional Access tab before changing site Members.  
- ⚠️ **App registration ≠ Enterprise app** — assignment and gallery SSO are enterprise-app tasks.  
- ⚠️ **Identity Secure Score ≠ incident response** — it’s a posture/recommendation score, not Defender XDR incidents.  
- ⚠️ **Audit log ≠ sign-in log** — directory changes vs authentication events.  
- ⚠️ **SSO does not grant SharePoint permissions** — it authenticates; AuthZ still required.  
- ⚠️ **Distribution list as “security object”** — prefer security / M365 groups for access control scenarios.  
- ⚠️ **Risky sign-in remediation** — often password reset / MFA / CA based on risk — not “create a new DL.”

---

## 7. Hands-on checklist

- [ ] Entra admin center: create a test user and a security group; add the user to the group  
- [ ] Assign a license via user and (if available) via group-based licensing  
- [ ] Open **Conditional Access** — read one policy’s users, apps, conditions, grant controls  
- [ ] Open **Sign-in logs** — inspect MFA and Conditional Access details on one event  
- [ ] Open **Audit logs** — find a group or user update event  
- [ ] Locate **Identity Secure Score** and note 2 improvement actions  
- [ ] Browse **PIM** (Roles) — see Eligible vs Active (lab tenant / sufficiently licensed)  
- [ ] Open **App registrations** and **Enterprise applications** — compare blades for the same app  
- [ ] Trace one failed sign-in using the troubleshooting table above  

---

## 8. Checkpoint

1. Users report “You cannot access this right now” only when off-network. Which Entra feature most likely enforces that?  
2. A Global Admin should not have standing privileges. Which feature?  
3. You need to know who deleted a Conditional Access policy. Sign-in log or audit log?  
4. You must assign the HR group to a gallery SaaS app for SSO. App registration or Enterprise application?  
5. Sign-in succeeds (MFA passed) but OneDrive is empty/unavailable for a new hire. What’s the next check after identity?

### Answers

1. **Conditional Access** (location-based grant/block or require controls).  
2. **Privileged Identity Management (PIM)** — eligible, time-bound activation.  
3. **Audit log** (directory / policy configuration change).  
4. **Enterprise application** (user/group assignment for SSO).  
5. **License / service plan / group membership** for OneDrive/SharePoint — AuthN already worked; this is entitlement/AuthZ provisioning.

---

## 9. Learn links

| Topic | URL |
|-------|-----|
| Microsoft Entra ID documentation | https://learn.microsoft.com/en-us/entra/identity/ |
| Conditional Access overview | https://learn.microsoft.com/en-us/entra/identity/conditional-access/overview |
| MFA | https://learn.microsoft.com/en-us/entra/identity/authentication/concept-mfa-howitworks |
| SSO overview | https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/what-is-single-sign-on |
| Identity Secure Score | https://learn.microsoft.com/en-us/entra/identity/monitoring-health/concept-identity-secure-score |
| Sign-in logs | https://learn.microsoft.com/en-us/entra/identity/monitoring-health/concept-sign-ins |
| Audit logs | https://learn.microsoft.com/en-us/entra/identity/monitoring-health/concept-audit-logs |
| PIM | https://learn.microsoft.com/en-us/entra/id-governance/privileged-identity-management/pim-configure |
| App registrations | https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-register-app |
| Enterprise apps | https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/what-is-application-management |
| Identity Protection / risk | https://learn.microsoft.com/en-us/entra/id-protection/overview-identity-protection |
| AB-900 study guide | https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ab-900 |
