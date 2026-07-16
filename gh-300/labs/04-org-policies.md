# Lab 04 — Organization Policies, Code Review, Audit Logs & REST API

**Goal:** Configure Copilot like an enterprise admin: policies, feature availability, Code Review, audit, subscriptions API.

**Time:** 60–120 minutes  
**Prereqs:** Org owner / enterprise owner permissions (or read-only shadowing an admin). If you lack access, complete the **simulation track** at the end.

---

## Part A — Locate Copilot admin surfaces

### Organization

1. GitHub.com → Organization profile  
2. **Settings** → **Copilot** (wording: Policies / Access / Features)  
3. Inventory toggles for:
   - Copilot availability for org members  
   - IDE feature allowances  
   - github.com Copilot features  
   - Chat / Agent / CLI related controls (as exposed)  
   - Suggestions matching public code  
   - Copilot Code Review policies  

### Enterprise (if applicable)

1. Enterprise account → Settings → Copilot  
2. Note **enterprise-level** policies that override orgs  
3. Confirm which settings are enterprise-only

**Deliverable:** Write a 1-page inventory of every Copilot toggle you can see and whether it is org or enterprise scoped.

---

## Part B — Professional policy baseline (recommended)

Configure (or propose) this baseline for a regulated team:

| Policy | Recommended starting point | Rationale |
|---|---|---|
| Seat assignment | Controlled by admins | Cost + least privilege |
| Suggestions matching public code | **Blocked** | IP risk reduction / indemnity path |
| Content exclusions | Enabled + patterns (Lab 05) | Secrets/regulated data |
| Agent Mode | On for trusted teams / Off for high-risk orgs | Autonomy risk |
| Copilot on github.com | Match IDE posture | Consistency |
| Code Review assistance | Enabled with standards | PR quality |
| Dual control | Changes via change ticket | Auditability |

---

## Part C — Feature availability across IDEs and github.com

1. Identify settings that separately affect:
   - IDE extensions  
   - github.com Chat / PR features  
2. Disable one low-risk preview feature in a test org (if allowed).  
3. Verify a member no longer sees it (or sees disabled state).  
4. Re-enable and verify restore.

**Exam mapping:** “Restrict features in IDEs and on github.com” → **organization-wide Copilot policy / feature management**.

---

## Part D — Copilot Code Review policies

1. Open Copilot Code Review policy settings for the org.  
2. Enable review assistance for target repos or org-wide per docs.  
3. Attach or reference **instructions / review standards** (Lab 06).  
4. Open a test PR and request Copilot review.  
5. Evaluate comments for false positives; refine instructions.

**Example review standard snippet**

```markdown
When reviewing:
- Flag missing tests for new public functions
- Flag hardcoded secrets
- Flag SQL string concatenation
- Do not nitpick import order
- Prefer actionable fixes over style lectures
```

---

## Part E — Audit logs

1. Org/Enterprise → **Audit log**.  
2. Filter for Copilot-related events (policy changes, seat changes, feature toggles, agent admin events as available).  
3. Export or save a sample event for your notes.  
4. Create a monthly review ritual: who changed Copilot policies?

**Exam mapping:** compliance visibility → **organization audit log events related to Copilot**.

---

## Part F — Manage subscriptions via REST API

Professional automation uses GitHub REST endpoints for Copilot business/enterprise seat management.

### F1. Create a fine-scoped token / GitHub App

- Least privilege: only Copilot seat management + org read as required  
- Store in a secret manager; never commit  

### F2. Example: list Copilot seat assignments (shape)

```bash
# Illustrative — confirm current endpoint in GitHub REST docs
gh api orgs/ORG/copilot/billing/seats
```

### F3. Example: add/remove a user seat (shape)

```bash
# Illustrative POST/DELETE against current Copilot subscription endpoints
gh api -X POST orgs/ORG/copilot/billing/selected_users -f users[]='octocat'
```

**Lab task:** Using official docs for your plan date, write the exact endpoints you would use to:

1. List seats  
2. Assign a seat  
3. Remove a seat  
4. Handle pagination/errors  

---

## Part G — Simulation track (no admin rights)

If you cannot access settings, still learn for the exam:

1. Read GitHub docs: managing Copilot policies for orgs/enterprises.  
2. Draw a diagram: Enterprise policy → Org policy → Repo exclusion → User IDE.  
3. Memorize which features need Business vs Enterprise ([cheatsheet](../reference/plan-tiers-cheatsheet.md)).  
4. Practice scenario answers from Domain 2/6 in `../../gh-300-topics.md`.

---

## Acceptance checklist

- [ ] Can navigate to org Copilot settings blindfolded  
- [ ] Can explain public-code **Block** purpose  
- [ ] Can enable/describe Code Review policy  
- [ ] Can find Copilot events in audit log  
- [ ] Can describe REST seat management flow  
- [ ] Knows enterprise vs org precedence at a high level  
