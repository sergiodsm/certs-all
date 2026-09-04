# 01 — Microsoft 365 Objects & Admin Centers

**Domain:** 1.1 Identify the core objects of Microsoft 365 services (part of **30–35%**)  
**Skills measured as of:** July 22, 2026

---

## 1. Official bullets covered

- Explain how **license types** assigned to users and groups affect access to Microsoft 365 features  
- Explore organization configurations in the **Microsoft 365 admin center** (domain names and org settings)  
- Identify objects to configure in the **Exchange admin center** (mailboxes and distribution groups)  
- Identify objects to configure in the **SharePoint admin center** (sites, libraries, and folders)  
- Identify appropriate **roles and permissions** for sites in SharePoint  
- Identify objects to configure in the **Teams admin center** (teams, channels, and policies)

---

## 2. Why it matters on the exam

AB-900 expects you to map a task to the **correct admin center and object** before you think about Copilot or Purview. Many stems are “where do you configure X?” or “which object enables Y?” License assignment is the gate for feature access — including Copilot — so “missing license” vs “wrong center” is a common distractor pair. If you confuse Exchange distribution lists with Teams, or SharePoint site roles with Entra roles, you lose easy Domain 1 points.

---

## 3. Core concepts

### Licenses and feature access

| Idea | Admin meaning |
|------|----------------|
| **License** | Entitlement that unlocks apps/services (Exchange mailbox, Teams, SharePoint, Copilot, etc.) |
| **Assigned to user** | Most common path — user gets features listed in the SKU |
| **Assigned to group** | Group-based licensing: members inherit licenses (Entra / M365 admin patterns) |
| **Service plan** | Fine-grained on/off inside a SKU (e.g., disable one app within a suite) |
| **No license** | User may authenticate but cannot use licensed workloads |

**Exam rule:** Feature missing → first check **license / service plan**, then policy/permissions, then admin-center config.

### Microsoft 365 admin center (tenant “front door”)

Primary place for:

- Users and groups (often with deep links into Entra)  
- **Licenses**  
- **Domains** (custom domain verification, DNS records)  
- **Org settings** (tenant-wide preferences, integrated apps, security defaults links, etc.)  
- Billing / subscriptions overview  
- High-level usage and health entry points  

URLs (typical): `admin.microsoft.com`

### Exchange Online objects

| Object | What it is |
|--------|------------|
| **User mailbox** | Primary mailbox for a licensed user |
| **Shared mailbox** | Mailbox without a signed-in user license (for shared scenarios; permissions granted to users) |
| **Distribution group / distribution list (DL)** | Mail-enabled group for email fan-out (not primarily a security principal for resource ACL) |
| **Mail-enabled security group** | Can be used for mail *and* permissions in some scenarios |
| **Microsoft 365 group** | Collaboration group with mailbox + SharePoint + Teams integration patterns |

Exchange admin center focuses on **mail flow, mailboxes, recipients, mail-enabled groups**.

### SharePoint Online objects

| Object | What it is |
|--------|------------|
| **Site** | Container for content (team site, communication site, etc.) |
| **Document library** | Collection of files/folders inside a site |
| **Folder / file** | Content items; inherit or break permission inheritance |
| **Site permissions / roles** | Who can do what on the site |

SharePoint admin center: site collections/sites, sharing settings, storage, and admin-level governance features (including paths into oversharing tools covered later in Domain 2).

### SharePoint site roles (fundamentals)

Classic / modern permission levels you’ll see in scenarios:

| Role / level | Typical capability |
|--------------|--------------------|
| **Site Owner** | Full control of site settings and permissions |
| **Site Member** | Contribute / edit content (often Edit) |
| **Site Visitor** | Read-only |
| **Full Control / Contribute / Read / Restricted View** | Permission levels that can be assigned to users/groups |

**Exam rule:** Owners manage the site; members collaborate; visitors consume. Breaking inheritance at folder/file level increases **oversharing risk** (Domain 2.4).

### Teams objects

| Object | What it is |
|--------|------------|
| **Team** | Collaboration space backed by a Microsoft 365 group |
| **Channel** | Topic space inside a team (standard, private, shared — know they differ in membership scope) |
| **Policies** | Admin-enforced settings (messaging, meeting, app, live events, etc.) applied to users |

Teams admin center: manage teams/channels at scale, assign **policies**, app permission policies, and org-wide Teams settings — not the same as creating a site in SharePoint admin center (though a team creates a connected SharePoint site).

---

## 4. How it works (admin-center oriented)

### A. License → feature path

1. Purchase / assign subscription in Microsoft 365 admin center.  
2. Assign license to **user** or **group**.  
3. Confirm required **service plans** are on.  
4. User signs in → apps appear based on license + admin policies.  
5. For Copilot (Domain 3): Copilot SKU / PAYG is a separate entitlement decision — still rooted in “does this identity have access?”

### B. Domains and org settings

1. Open **Microsoft 365 admin center** → Settings → Domains.  
2. Add domain → prove ownership with DNS (TXT/MX/CNAME as directed).  
3. Set default domain for new users if needed.  
4. Review **Org settings** for tenant-wide toggles (services, security, integration).  
5. Domain/email problems → often DNS + Exchange; “users can’t get the right UPN” → domains + Entra user attributes.

### C. Exchange: mailboxes and DLs

1. Open **Exchange admin center**.  
2. Recipients → mailboxes / groups.  
3. Create shared mailbox or distribution list as needed.  
4. Grant **Send As / Full Access** on shared mailboxes to users (not the same as SharePoint Contribute).  
5. Mail-enabled DL ≠ Teams team ≠ SharePoint Visitors group — pick by **communication vs collaboration vs file ACL**.

### D. SharePoint: sites, libraries, folders, roles

1. Open **SharePoint admin center** → Active sites (create / manage sites).  
2. Inside a site: create libraries and folders.  
3. Assign Owners / Members / Visitors (or custom SharePoint groups + permission levels).  
4. Prefer group-based access; avoid unique permissions explosion.  
5. Tenant sharing defaults (anyone links, new/existing guests) live at SharePoint admin / org sharing — feeds oversharing scenarios later.

### E. Teams: teams, channels, policies

1. Open **Teams admin center**.  
2. Teams & channels — manage structure; policies — control user experience.  
3. Assign messaging/meeting/app policies to users or groups.  
4. Creating a team typically provisions the Microsoft 365 group + SharePoint site + mailbox — but **day-2 policy control** is still Teams admin center.  
5. Channel type matters: standard = team-wide; private = subset; shared = cross-team collaboration patterns.

---

## 5. Compare / choose

### Admin-center chooser

| You need to… | Go to |
|--------------|--------|
| Assign licenses, manage domains, org settings, users at tenant level | **Microsoft 365 admin center** |
| Mailboxes, shared mailboxes, distribution lists, mail flow | **Exchange admin center** |
| Sites, libraries, sharing defaults, site storage, site-level governance | **SharePoint admin center** |
| Teams, channels, Teams policies (meeting/messaging/apps) | **Teams admin center** |
| Users/groups as identity, Conditional Access, MFA, PIM | **Microsoft Entra admin center** (Topic 03) |
| Sensitivity labels, DLP, retention, eDiscovery | **Microsoft Purview** (Domain 2) |
| Agent lifecycle / Power Platform side of agents | **Power Platform admin center** (+ M365) (Domain 3) |

### Object chooser

| Need | Prefer |
|------|--------|
| Email a set of people (no deep collaboration) | Distribution list / mail-enabled group |
| Chat + files + Planner-style collaboration | Team (Microsoft 365 group) |
| Intranet / document workspace | SharePoint site + library |
| Shared departmental inbox | Shared mailbox |
| Enforce meeting recording rules for users | Teams **policy** |
| Unlock Outlook / Teams / Copilot apps | Correct **license** |

### License vs permission vs policy

| Control | Question it answers |
|---------|---------------------|
| License | *Are they allowed to use the product at all?* |
| Permission (SharePoint / mailbox ACL) | *What content can they open?* |
| Policy (Teams / CA) | *Under what rules can they use it?* |

---

## 6. Exam traps

- ⚠️ **Wrong admin center:** Creating a DL in Teams admin center, or managing Teams meeting policies in Exchange.  
- ⚠️ **License vs permission:** User has SharePoint Contribute but no Teams license — still cannot use Teams.  
- ⚠️ **DL ≠ security group for SharePoint:** Distribution lists are for mail; use security / M365 groups for site access.  
- ⚠️ **Team already has a SharePoint site:** Don’t assume you must “also create” a separate site for every team unless the scenario asks for a standalone site.  
- ⚠️ **Owners vs Members:** Visitors cannot change site settings; Members are not automatically Owners.  
- ⚠️ **Policies apply to users:** Teams policies are typically assigned to people — not “configured once inside one channel” as the only control.  
- ⚠️ **Shared mailbox ≠ shared SharePoint library:** Different objects, different admin centers, different permission models.  
- ⚠️ **Org settings ≠ Conditional Access:** Tenant org toggles are not a substitute for Entra Conditional Access policies.

---

## 7. Hands-on checklist

In a lab / trial tenant:

- [ ] Microsoft 365 admin center: locate **Licenses**, assign a license to a test user  
- [ ] Confirm a service plan can be toggled within a license (where available)  
- [ ] Domains: view DNS records for your custom or default domain  
- [ ] Org settings: browse 3–5 tenant settings categories (do not break production)  
- [ ] Exchange admin center: create a **shared mailbox** and a **distribution list**; grant a user access  
- [ ] SharePoint admin center: create a site; open site permissions; identify Owners / Members / Visitors  
- [ ] Create a library and folder; note inheritance  
- [ ] Teams admin center: view a team and its channels; open **Messaging** or **Meeting** policies and see assignment  
- [ ] Mentally map each click to the chooser table above  

---

## 8. Checkpoint

1. A user cannot open Outlook on the web but can sign in to the Microsoft 365 portal. What should you check first?  
2. You need a shared inbox for finance@contoso.com with three delegates. Which object and admin center?  
3. You must prevent users from scheduling meetings that allow anonymous join (policy-level). Where do you configure this?  
4. Marketing needs a document library with Owners, editors, and read-only viewers. Which center and which roles pattern?  
5. Contoso adds `fabrikam.com` as an email domain. Where do you start domain setup?

### Answers

1. **License / Exchange Online service plan** for the mailbox — before digging into mailbox permissions.  
2. **Shared mailbox** in the **Exchange admin center**; grant Full Access / Send As as needed.  
3. **Teams admin center** → meeting (or related) **policies**, assigned to users.  
4. **SharePoint** site (admin center to create/manage; site permissions for Owners / Members / Visitors or equivalent permission levels).  
5. **Microsoft 365 admin center** → Domains (verify DNS), then complete Exchange/mail setup as required.

---

## 9. Learn links

| Topic | URL |
|-------|-----|
| Microsoft 365 admin center | https://learn.microsoft.com/en-us/microsoft-365/admin/ |
| Assign licenses | https://learn.microsoft.com/en-us/microsoft-365/admin/manage/assign-licenses-to-users |
| Domains | https://learn.microsoft.com/en-us/microsoft-365/admin/setup/add-domain |
| Exchange Online admin | https://learn.microsoft.com/en-us/exchange/exchange-online |
| Shared mailboxes | https://learn.microsoft.com/en-us/microsoft-365/admin/email/create-a-shared-mailbox |
| SharePoint admin | https://learn.microsoft.com/en-us/sharepoint/sharepoint-admin-role |
| Site permissions | https://learn.microsoft.com/en-us/sharepoint/customize-sharepoint-site-permissions |
| Teams admin center | https://learn.microsoft.com/en-us/microsoftteams/manage-teams-in-modern-portal |
| Teams policies overview | https://learn.microsoft.com/en-us/microsoftteams/teams-policies-overview |
| AB-900 study guide | https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ab-900 |
