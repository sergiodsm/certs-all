# Lab 05 — Content Exclusions End-to-End

**Goal:** Configure, verify, troubleshoot, and document content exclusions professionally — including what they do **not** cover.

**Time:** 45–75 minutes  
**Prereqs:** Business or Enterprise Copilot; repo admin or org owner. Free/Pro users: complete simulation track.

---

## Part A — Design exclusion patterns (before clicking UI)

Create a short design doc:

```text
Repo: shop-api
Sensitive paths:
- .env, .env.*
- secrets/**
- **/*credentials*
- dumps/**/*.sql
- regulated/customer-exports/**
Keep allowed for context:
- src/contracts/** (public interfaces)
- docs/architecture.md
```

**Pattern tips**

- Prefer narrow globs over excluding the whole monorepo.  
- Exclude data dumps and key material; keep API contracts visible.  
- Align with `.gitignore` mentally — but exclusions are **not** gitignore.

---

## Part B — Configure at repository scope

1. Open the repository on GitHub.com.  
2. **Settings** → **Copilot** → **Content exclusion** (path may read “Excluded files” / similar).  
3. Add patterns, for example:

```text
**/.env
**/.env.*
**/secrets/**
**/*credentials*
**/dumps/**
```

4. Save.  
5. Record timestamp — propagation to already-open IDEs can take **up to ~30 minutes**.

---

## Part C — Configure at organization / enterprise scope

### Org

1. Org **Settings** → **Copilot** → Content exclusion.  
2. Add org-wide patterns for universal secrets paths.  
3. Document that repo rules combine with org rules per current docs.

### Enterprise

1. Enterprise Copilot content exclusion settings.  
2. Set enterprise standards (e.g., always exclude `**/*.pem`).  
3. Note precedence: **enterprise rules take precedence** when set.

**Roles check**

- Owner/admin: edit  
- Maintain: often view-only  
- Outside collaborators: typically cannot manage org exclusions  

---

## Part D — Verify on supported IDE surfaces

1. Reload VS Code window (or wait for propagation).  
2. Open an excluded file (`secrets/dummy.env`).  
3. Confirm **no inline suggestions** (or Copilot disabled indicator).  
4. In another allowed file, confirm completions still work.  
5. In Chat, ask to analyze the excluded file → expect refusal / inability to use that content (supported Chat).  
6. In an allowed file, ask a question that would require excluded secrets → Copilot should not leverage excluded content as context.

### Verification log template

| Test | Expected | Observed | Pass? |
|---|---|---|---|
| Inline in `.env` | No suggestions | | |
| Inline in `app.ts` | Suggestions OK | | |
| Chat analyze `.env` | Refuse / blocked | | |
| Context bleed from secrets | Should not | | |

---

## Part E — Prove the Agent/CLI gap (exam drill)

1. With exclusions active, start **Agent Mode** (if enabled) and ask it to summarize files under `secrets/` (use **fake** secrets only).  
2. Separately try **Copilot CLI** against the same paths.  
3. Record whether behavior differs from IDE inline/Chat.  
4. Write the exam sentence:

> Content exclusions are **not** a complete control for Agent Mode / CLI / coding agent surfaces.

5. List compensating controls you would propose to security:

- Separate secrets repo with no developer agent access  
- Disable Agent Mode org-wide for high-risk groups  
- Local file permissions / not checking secrets into the workspace  
- Secret scanning + push protection  
- Never paste secrets into prompts  

---

## Part F — Troubleshooting workshop

Break/fix these:

1. **Exclusions seem ignored** → wait 30m, reload IDE, confirm pattern syntax, confirm plan is Business+, confirm you’re in the right org repo.  
2. **Completions worse everywhere** → pattern too broad (`**/*`); narrow it; keep contracts visible.  
3. **SDK helpers “invisible”** → SDK path accidentally excluded; move public types to allowed path.  
4. **User tries rename to bypass** → stop; treat as policy violation.

---

## Part G — Public-code safeguard (same lab day)

While in Copilot policies:

1. Set **Suggestions matching public code** to **Blocked**.  
2. Explain to a teammate in 2 sentences what changed.  
3. Note this is distinct from content exclusion.

---

## Simulation track (no Business/Enterprise)

1. Read official docs on content exclusion.  
2. Memorize effects (three vectors) + non-effects.  
3. Memorize roles + ~30 minute propagation.  
4. Memorize Agent/CLI non-application gotcha.  
5. Answer Domain 6 questions in `../../gh-300-topics.md` until 10/10.

---

## Acceptance checklist

- [ ] Designed patterns before configuring  
- [ ] Configured repo and/or org exclusions  
- [ ] Verified inline + Chat behavior  
- [ ] Documented Agent/CLI limitation with evidence or docs citation  
- [ ] Set or described public-code **Block**  
- [ ] Produced a troubleshooting runbook for the team  
