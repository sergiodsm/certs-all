# Domain 6 — Privacy, Content Exclusions & Safeguards (10–15%)

This domain + plan tiers separates **users** from **administrators**. Highest trap density on the exam.

---

## 6.1 Content exclusions — what they do

On **supported** surfaces, exclusions:

1. Disable **inline suggestions inside** excluded files.  
2. Prevent excluded content from being used as **context** for suggestions in other files.  
3. Cause Copilot Chat (where supported) to **refuse analyzing** excluded content.  
4. Extend to related review assistance where documented.

They do **not**:

- Delete files from Git history  
- Encrypt the laptop  
- Remove license obligations for accepted code  
- Replace IAM / branch protection  
- Guarantee secrets never appear if a human pastes them into Chat  

Full lab: **[labs/05-content-exclusions.md](./labs/05-content-exclusions.md)**

---

## 6.2 Who can configure exclusions

| Role | Typical capability |
|---|---|
| Enterprise owners | Enterprise-wide rules (highest precedence when set) |
| Organization owners | Org-level rules |
| Repository admins | Repo-level rules |
| Maintain | Often **view** settings, **not** edit |
| Individual Free/Pro users | **Cannot** configure org-style content exclusions (plan gate) |

**Propagation:** after changes, IDEs may take **up to ~30 minutes** to pick up exclusions already loaded — exam-relevant troubleshooting detail.

**Precedence:** enterprise rules override org when configured; otherwise org rules apply broadly per product docs.

---

## 6.3 Critical gotcha (memorize verbatim)

> **Content exclusion does not fully apply to Copilot CLI, the coding agent, or Agent Mode in Chat / Edit-style agentic surfaces.**

### Exam trap

**Q:** Team must stop Agent Mode from reading `/secrets`. Configure content exclusion?

**A:** **No** — exclusions are the wrong primary control for that agentic surface. Use different controls (permissions, not granting access, redaction, separate repos, agent guardrails, avoid opening secrets, policy disabling agent features, etc.—pick the option that matches docs/scenario).

This is one of the most-cited failure points in community pass reports.

---

## 6.4 Suggestions matching public code (duplication detection)

| Setting | Intent |
|---|---|
| **Allowed / warn** (wording varies) | May show matching public code with warnings |
| **Blocked** | Suppress completions that closely match public GitHub code |

**IP indemnity / IP protection exam language:** seek coverage by setting suggestions matching public code to **Blocked** (Business/Enterprise contexts). Distractors invent “enable license checking” toggles that aren’t the documented control name.

**Side effect:** fewer suggestions after Block → usually **filter working**, not revoked seats.

---

## 6.5 Ownership & limitations of outputs

Product-terms aligned statement:

> **GitHub does not claim ownership of suggestions. You remain responsible for code you accept and use.**

Implications:

- Still subject to license/security review  
- Public-code Block reduces risk; it does not erase review duties  
- Company policy still governs contribution standards  

---

## 6.6 Editor / personal safeguard settings

Professionals also configure locally (wording varies by IDE):

- Enable/disable inline suggestions  
- Show/hide public-code matching warnings (where available)  
- Chat/agent feature toggles allowed by org policy  

Org policy can override individual preference — if Agent Mode is disabled org-wide, local desire doesn’t matter.

---

## 6.7 Troubleshooting matrix

| Symptom | Check first |
|---|---|
| No suggestions inside `*.env` | Path excluded? Expected. |
| Other files “forget” internal SDK | Is SDK path excluded? |
| Chat refuses to analyze a file | Exclusion or policy |
| Agent still sees sensitive path | Exclusions may **not** apply — different control needed |
| Fewer completions after Block | Public-code filter working |
| Exclusions “not active” after admin change | Wait for propagation (~30 min); reload window; confirm scope |
| Poor quality after broad exclusions | You excluded needed reference code — narrow patterns; supply non-secret contracts |

---

## 6.8 Professional privacy setup (recommended order)

1. Choose **Business/Enterprise** if you need exclusions + indemnity + admin controls.  
2. Set **Suggestions matching public code: Blocked**.  
3. Define enterprise/org exclusion patterns for secrets, keys, dumps, regulated data.  
4. Disable or tightly govern **Agent Mode / CLI** if policy requires stronger isolation.  
5. Roll out instructions: never paste secrets; use synthetic data.  
6. Enable **audit log** review for Copilot admin events.  
7. Train developers on validation (Domain 1).  

---

## Worked scenario

**Scenario:** Inline completions in `app.ts` stopped using helpers from `internal/sdk/crypto.ts` after a security hardening sprint.

**Reasoning**

1. Check whether `internal/sdk/crypto.ts` or `/internal/sdk/**` was added to exclusions.  
2. If yes and intentional, expose a **non-secret** public interface file that remains allowed, or document APIs in an allowed markdown contract.  
3. Do **not** rename files solely to bypass policy.

---

## Domain 6 quick self-test

1. List three effects of exclusions on supported surfaces.  
2. Who can edit vs only view exclusions?  
3. Recite the Agent/CLI exclusion gotcha.  
4. What setting targets public-code matching for indemnity-style protection?  
5. Who owns accepted suggestions?
