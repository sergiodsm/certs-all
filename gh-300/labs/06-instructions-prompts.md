# Lab 06 — Instructions Files, Prompt Files & Customization

**Goal:** Standardize Copilot behavior across a team using instructions, prompt files, and review standards.

**Time:** 45–60 minutes  
**Docs:** [Customization cheat sheet](https://docs.github.com/en/copilot/reference/customization-cheat-sheet)

> Exact filenames/locations evolve (`.github/copilot-instructions.md`, path-specific instructions, prompt files in `.github/prompts/`, IDE prompt libraries, Spaces). Learn the **concepts** and verify current paths in docs before exam day.

---

## Part A — Instructions file (always-on team norms)

### A1. Create project instructions

Create (or update) a repository instructions file, commonly:

```text
.github/copilot-instructions.md
```

### A2. Starter template

```markdown
# Copilot instructions — payments-api

## Stack
- Node 22, TypeScript strict, Express, Zod, Vitest, Prisma

## Coding standards
- No `any`; prefer explicit DTOs
- Pure functions when possible
- Parameterized queries only; never string-concat SQL
- Do not invent third-party APIs; ask if unsure

## Testing
- Vitest; files named `*.test.ts`
- Include edge cases: null, empty, auth failure, boundary

## Security
- Never suggest hardcoding secrets
- Log redaction for tokens and PII

## Output preferences
- Prefer small diffs
- Explain non-obvious tradeoffs briefly
```

### A3. Verify

1. Start a **new** Chat thread.  
2. Ask: `Add a healthcheck endpoint consistent with this repo.`  
3. Confirm style matches instructions (naming, test file patterns).  
4. Ask something that should trigger “ask if unsure” when context is missing.

---

## Part B — Path-specific instructions (optional)

If supported in your environment, add path-scoped instructions (e.g., stricter rules under `src/auth/**`).

Example intent:

```markdown
# src/auth/** instructions
- Prefer existing AuthService; do not create parallel auth stacks
- All new routes require authz checks
- Add threat notes in PR description for auth changes
```

---

## Part C — Prompt files (reusable task packs)

Create reusable prompts for recurring work, e.g.:

```text
.github/prompts/add-endpoint.prompt.md
.github/prompts/threat-model.prompt.md
.github/prompts/write-vitest.prompt.md
```

### Example: `write-vitest.prompt.md`

```markdown
---
description: Generate Vitest unit tests for the selected TypeScript function
---
Write Vitest unit tests for the selected function.

Requirements:
- Mirror existing test style in neighboring *.test.ts files
- Cases: happy path, null/undefined, empty collection, boundary, error path
- Use descriptive test names
- Do not mock unless necessary
- Output only the test file content
```

### Example: `threat-model.prompt.md`

```markdown
Review the selected code for security issues.
Return a table: severity | issue | location | exploit sketch | remediation.
Check injection, authn/authz, secret handling, SSRF, unsafe deserialization.
Do not recommend disabling TLS or hardcoding credentials.
```

### Use them

Invoke via Copilot Chat prompt picker / command that loads prompt files (per current UI). Run both prompts on a sample handler.

---

## Part D — Custom review standards for Copilot Code Review

Combine Lab 04 + this lab:

1. Put review expectations in instructions or a dedicated review standards doc.  
2. Open a PR with a deliberate small flaw (e.g., SQL concat in a branch).  
3. Request Copilot review.  
4. Tune standards until noise is acceptable.

---

## Part E — Spaces (concept practice)

If Copilot Spaces are available on your plan:

1. Create a Space for a domain (e.g., “Billing rules”).  
2. Attach key docs/contracts (non-secret).  
3. Ask domain questions grounded in that Space.  
4. Compare answer quality vs Chat without Space context.

**Exam purpose of Spaces:** curated context for better grounded conversations.

---

## Part F — Team rollout playbook

1. Draft instructions in a PR — don’t silent-push.  
2. Socialize: 15-minute demo for the team.  
3. Add CONTRIBUTING blurb: “Prefer prompt files for X/Y/Z.”  
4. Revisit quarterly after framework upgrades.  
5. Keep secrets **out** of instructions/prompt files.

---

## Acceptance checklist

- [ ] Instructions file merged or drafted  
- [ ] At least two prompt files created and executed  
- [ ] Verified Chat follows stack constraints  
- [ ] Linked review standards to Code Review  
- [ ] Can explain instructions vs prompt files in one sentence each  

---

## Exam one-liners

- **Instructions files** customize recurring coding/review standards.  
- **Prompt files** reuse task-specific prompts for consistency.  
- Neither guarantees zero hallucinations — humans still validate.
