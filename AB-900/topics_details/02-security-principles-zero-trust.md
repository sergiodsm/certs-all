# 02 — Security Principles & Zero Trust

**Domain:** 1.2 Understand the Microsoft 365 security principles (part of **30–35%**)  
**Skills measured as of:** July 22, 2026

---

## 1. Official bullets covered

- Explain the core **Zero Trust** principles  
- Understand **authorization**  
- Understand **authentication** methods  
- Understand **threat protection** and **threat intelligence**  
- Understand features and capabilities of **Microsoft Defender XDR**

---

## 2. Why it matters on the exam

Domain 1.2 is conceptually short but feeds almost every later security question. Exam items test whether you can tell **authentication** (prove who you are) from **authorization** (what you’re allowed to do), and whether you apply Zero Trust language correctly: verify explicitly, least privilege, assume breach. Defender XDR appears at a **fundamentals** level — know the unified incident / signal story, not deep hunting KQL. Mix-ups with Purview (compliance) vs Defender (threat protection) are frequent distractors.

---

## 3. Core concepts

### Zero Trust — core principles

Microsoft’s Zero Trust guidance centers on:

| Principle | Plain language | M365 / Entra example |
|-----------|----------------|----------------------|
| **Verify explicitly** | Always authenticate and authorize based on all available signals | MFA + Conditional Access using user, device, location, risk |
| **Use least privilege access** | Limit rights; prefer just-in-time / just-enough | PIM for admins; scoped roles; app permissions minimized |
| **Assume breach** | Design as if attackers are already inside | Segment access, monitor with Defender XDR, reduce blast radius |

**Memorize:** Zero Trust is a **strategy**, not a single product toggle labeled “Zero Trust = On.”

### Authentication (AuthN)

**Authentication** = proving identity.

Common methods in Microsoft 365 / Entra contexts:

| Method | Notes |
|--------|-------|
| Password | Alone is weak; often combined with MFA |
| **MFA** (Authenticator app, FIDO2/security key, Windows Hello for Business, SMS/voice where allowed) | Second factor after primary auth |
| Passwordless | Passkeys / FIDO2, Hello, phone sign-in patterns |
| Certificate-based / federated | Org-specific; still AuthN |
| OAuth / OpenID Connect tokens | App and user session authentication |

**Exam rule:** MFA and Conditional Access **enforce** stronger AuthN / access decisions — they are not authorization ACLs on a SharePoint file.

### Authorization (AuthZ)

**Authorization** = deciding what an authenticated identity may do.

Examples:

- SharePoint site role (Owner / Member / Visitor)  
- Exchange mailbox Full Access  
- Entra role (Global Reader, Exchange Administrator)  
- Group membership that grants access to a Team  
- App permissions / scopes on an enterprise application  

**Order of operations:** Authenticate → then authorize. A user can pass MFA and still be denied a library (AuthZ failure).

### Threat protection

**Threat protection** = detecting, preventing, and responding to attacks (malware, phishing, compromised accounts, suspicious cloud apps, endpoint threats).

In the Microsoft 365 ecosystem this is primarily the **Microsoft Defender** family and related signals — not Purview sensitivity labels.

### Threat intelligence

**Threat intelligence** = curated knowledge about attackers, campaigns, indicators of compromise (IOCs), and tactics — used to improve detection and response.

Defender / Microsoft security services consume and surface intelligence so defenders can prioritize real threats. On AB-900, recognize it as **input to protection and investigation**, not a separate admin center you “assign licenses to users” for collaboration.

### Microsoft Defender XDR (fundamentals)

**Microsoft Defender XDR** (extended detection and response) unifies security signals across domains so analysts see **incidents** that correlate alerts from multiple products, for example:

| Signal domain (examples) | Typical product family |
|--------------------------|------------------------|
| Email & collaboration | Defender for Office 365 |
| Endpoints | Defender for Endpoint |
| Identities | Defender for Identity / Entra risk signals (related identity protection story) |
| Cloud apps | Defender for Cloud Apps |
| Cloud / resource posture (broader Microsoft security) | Adjacent Defender / security portals |

**Capabilities to know at fundamentals level:**

- Correlated **incidents** across workloads  
- Investigation and response from a unified security portal experience  
- Automated investigation / remediation features where licensed and enabled  
- Integration with threat intelligence to prioritize alerts  

**AB-900 depth:** Identify *what XDR is for* (cross-signal threat detection/response). You are not expected to write advanced hunting queries.

---

## 4. How it works (admin-center oriented)

### Zero Trust in day-to-day admin decisions

1. **Verify explicitly:** Prefer Conditional Access policies that require MFA, compliant devices, or trusted locations based on risk — not “VPN alone = trusted forever.”  
2. **Least privilege:** Prefer standard user accounts daily; elevate with **PIM** when admin work is needed (Topic 03).  
3. **Assume breach:** Enable monitoring (Defender XDR / security portal), review risky sign-ins, limit standing admin roles, segment guest and external sharing.

### Authentication vs authorization workflow

```text
User signs in
    → Authentication (password/passwordless + MFA as required)
    → Token issued (Entra ID)
    → Access request to Teams / SharePoint / Exchange / Copilot
    → Authorization (roles, group membership, ACLs, app permissions)
    → Allow / deny
```

Copilot (Domain 2) still rides this model: Copilot uses the **user’s authorized Graph access** — it does not bypass AuthZ.

### Threat protection + intelligence loop

1. Signals collected (email, endpoint, identity, cloud apps…).  
2. Detections enriched with **threat intelligence**.  
3. Related alerts grouped into **incidents** in Defender XDR.  
4. Analyst / automated response contains the threat.  
5. Lessons feed back into stricter AuthN/AuthZ (e.g., require MFA, block legacy auth).

### Where admins look

| Goal | Typical portal |
|------|----------------|
| MFA methods, CA, risky users/sign-ins | Microsoft Entra admin center |
| Incidents, Defender XDR investigation | Microsoft Defender security portal |
| Sensitivity / DLP / retention | Microsoft Purview (not XDR) |

---

## 5. Compare / choose

### Authentication vs authorization

| | Authentication | Authorization |
|--|----------------|---------------|
| Question | Who are you? | What may you do? |
| Failure example | Bad password / MFA denied | Access denied to site despite successful sign-in |
| Typical controls | Password, MFA, passwordless, Conditional Access grant controls | RBAC, SharePoint roles, group membership, app roles |
| Zero Trust link | Verify explicitly | Least privilege |

### Zero Trust vs “trust the network”

| Old model | Zero Trust |
|-----------|------------|
| Inside corporate network = trusted | Every request verified with signals |
| Broad standing admin rights | JIT / least privilege (PIM) |
| Perimeter firewall as main defense | Assume breach + continuous monitoring (XDR) |

### Defender XDR vs Microsoft Purview

| | Defender XDR | Purview |
|--|--------------|---------|
| Primary job | Threat detection & response | Data governance, compliance, information protection |
| Example alert | Phish campaign, malware, compromised account | DLP policy match, retention, insider risk policy |
| Exam trap | Using XDR to “fix oversharing labels” | Using DLP alone to stop endpoint ransomware |

### Threat protection vs threat intelligence

| | Threat protection | Threat intelligence |
|--|--------------------|---------------------|
| Role | Controls and response that stop/contain attacks | Knowledge that informs detections and prioritization |
| Example | Quarantine malicious mail, isolate device | Known bad sender/IP/campaign TTPs |

---

## 6. Exam traps

- ⚠️ **AuthN ≠ AuthZ:** “User failed MFA” is authentication; “User is Visitor not Member” is authorization.  
- ⚠️ **Zero Trust is not one checkbox:** Scenarios expect principles applied via CA, MFA, PIM, monitoring — not a mythical single switch.  
- ⚠️ **Least privilege ≠ remove MFA:** Least privilege reduces *rights*; MFA strengthens *verification*.  
- ⚠️ **Defender XDR ≠ Purview:** Oversharing / sensitivity / retention → Purview / SharePoint governance; malware / phish / incident correlation → Defender.  
- ⚠️ **Threat intelligence alone does not grant access:** It informs protection; it is not a license or permission.  
- ⚠️ **Assume breach ≠ “ignore prevention”:** It means add detection/response and reduce blast radius *in addition* to prevent controls.  
- ⚠️ **Conditional Access is not SharePoint ACL:** CA decides whether the session is allowed under policy; site permissions still apply afterward.

---

## 7. Hands-on checklist

- [ ] Read Microsoft’s Zero Trust principles page once; write the three principles from memory  
- [ ] Entra admin center: browse **Authentication methods** policy (do not weaken production)  
- [ ] Entra: open **Conditional Access** — note a policy that requires MFA (or report-only)  
- [ ] Entra: **Sign-in logs** — find a success and a failure; classify AuthN vs later AuthZ issues  
- [ ] Microsoft Defender portal: open **Incidents** — observe correlated alerts (lab tenant)  
- [ ] Verbally explain to yourself: “Purview labels don’t replace Defender incident response”  
- [ ] Map one admin task to each Zero Trust principle (verify / least privilege / assume breach)

---

## 8. Checkpoint

1. Name the three core Zero Trust principles.  
2. A user signs in with MFA but cannot open a SharePoint library. AuthN or AuthZ problem?  
3. Which is the better fit for correlating a phishing email with an endpoint alert: Purview DLP or Defender XDR?  
4. Is “threat intelligence” primarily a permission model or knowledge that improves detection?  
5. How does “least privilege” show up for Global Administrators in modern Entra practice?

### Answers

1. **Verify explicitly**, **use least privilege access**, **assume breach**.  
2. **Authorization** (permissions/roles) — authentication already succeeded.  
3. **Microsoft Defender XDR** (cross-signal incident correlation).  
4. **Knowledge / intel** that improves detection and prioritization — not a permission model.  
5. Prefer **eligible roles via PIM** (just-in-time elevation) instead of standing Global Admin for daily work.

---

## 9. Learn links

| Topic | URL |
|-------|-----|
| Zero Trust deployment / principles | https://learn.microsoft.com/en-us/security/zero-trust/ |
| Zero Trust identity pillar | https://learn.microsoft.com/en-us/security/zero-trust/deploy/identity |
| Authentication methods | https://learn.microsoft.com/en-us/entra/identity/authentication/concept-authentication-methods |
| Conditional Access (overview) | https://learn.microsoft.com/en-us/entra/identity/conditional-access/overview |
| Microsoft Defender XDR | https://learn.microsoft.com/en-us/defender-xdr/ |
| Microsoft 365 security docs | https://learn.microsoft.com/en-us/microsoft-365/security/ |
| AB-900 study guide | https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ab-900 |
