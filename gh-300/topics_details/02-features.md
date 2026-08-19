# Domain 2 — Use GitHub Copilot Features (25–30%)

Largest domain. Study as a **product surface map** + **plan/policy map**.

## Mental model: choose the right surface

| Need | Best surface |
|---|---|
| Next few lines while typing | Inline suggestions (ghost text) |
| Explain / generate / refactor with dialogue | Copilot Chat |
| Multi-file changes you review before apply | Edit Mode / Copilot Edits |
| Autonomous multi-step work (edit, run, fix) | Agent Mode |
| Terminal scripting / shell help | Copilot CLI |
| Structured reusable context for a project theme | Spaces |
| Lightweight app/prototype generation | Spark (know it exists; UI evolves) |
| PR narrative / review assistance | Copilot Code Review + PR summaries |
| External tools/data in agent workflows | MCP |
| Specialized delegated tasks | Sub-Agents |

---

## 2.1 IDE enablement (concepts)

Professional enablement always follows:

1. Licensed account / org seat  
2. Install Copilot extension/plugin for the IDE  
3. Sign in / authenticate to GitHub  
4. Confirm status (ready / error / policy blocked)  
5. Optionally tune editor settings (suggestions on/off, public-code warnings)

Step-by-step for VS Code, Visual Studio, and JetBrains: **[labs/01-ide-setup.md](./labs/01-ide-setup.md)**.

### Trigger patterns (exam language)

- **Inline:** type naturally; accept/reject/cycle suggestions  
- **Chat:** open Chat panel; attach files / selection; use commands  
- **CLI:** terminal assistant for commands/scripts  
- **Agent:** multi-step autonomous loop when policy allows  

---

## 2.2 GitHub Copilot CLI

**What it is:** Copilot assistance in the terminal — explain commands, suggest shell, generate scripts, work in interactive sessions.

**Why it matters on the exam:** productivity surface distinct from IDE; **content exclusions do not fully apply** here (Domain 6 trap).

Full install + command lab: **[labs/02-cli-setup.md](./labs/02-cli-setup.md)**.

### Example session goals

```bash
# Explain a dense pipeline
gh copilot explain "find . -name '*.ts' | xargs grep -l TODO | wc -l"

# Suggest a command from intent
gh copilot suggest "create a zip of all .log files modified today"
```

(Exact CLI entrypoints evolve — know *capabilities*: explain, suggest, interactive sessions, script/file help.)

---

## 2.3 Agent Mode vs Edit Mode vs Plan Mode

| Mode | Autonomy | Typical use | Review model |
|---|---|---|---|
| **Plan Mode** | Plans; limited/no edits until approved | Design approach first | Human approves plan |
| **Edit Mode / Copilot Edits** | Proposes multi-file edits | Controlled refactors | Selective accept/reject hunks |
| **Agent Mode** | Can edit, run tools/commands, iterate on failures | End-to-end tasks | Session review + PR review |

### Exam scenario mapping

- “Multi-step changes **including terminal** autonomously” → **Agent Mode**  
- “Multi-file changes I **review and selectively accept** without full terminal autonomy” → **Edit Mode**  
- “Outline steps first; don’t touch files yet” → **Plan Mode** / negative constraints in Agent prompts  

### Agent prompt boundaries (professional pattern)

```text
Goal: Add input validation to src/api/users.ts
Constraints:
- Do NOT modify database migrations
- Do NOT commit or push
- Run unit tests for users only
- Stop and summarize if any test fails twice
Out of scope: auth provider changes
```

---

## 2.4 MCP (Model Context Protocol)

**What:** Open standard for connecting agents to external tools/context (DBs, issue trackers, CI, docs systems) via protocolized servers.

**Exam answer shape:** MCP enables **standardized tool/context integrations** for Copilot agent workflows — not free Enterprise seats, not audit-log deletion.

Setup lab: **[labs/03-agent-mcp-setup.md](./labs/03-agent-mcp-setup.md)**.

---

## 2.5 Agent Sessions & Sub-Agents

- **Agent Session:** ongoing agentic work unit with history/tools.  
- **Sub-Agents:** delegate specialized subtasks with **optimized / isolated context** so the parent session stays focused.

**When to use Sub-Agents:** research docs, run a focused test fix, generate fixtures — without polluting the main context window.

---

## 2.6 Chat: commands, limits, feedback, prompt files

Know that Chat supports:

- Steering via **commands / options** (product-specific slash-style or UI actions)  
- **Context attachments** (selection, files, sometimes PRs/issues depending on surface)  
- **Feedback** under product/org policy (does **not** auto-publish private repos)  
- **Prompt files** for reusable instruction packs  

Customization lab: **[labs/06-instructions-prompts.md](./labs/06-instructions-prompts.md)**.

---

## 2.7 Spaces, Spark, PR summaries, instructions files

| Feature | Professional purpose |
|---|---|
| **Spaces** | Curate knowledge/context around a topic for better grounded conversations |
| **Spark** | Rapid prototype / lightweight app generation (know existence + use-case) |
| **PR summaries** | Prose summary of changeset (often Enterprise-associated on exam) |
| **Instructions files** | Encode team coding/review standards so Copilot follows norms |
| **Custom review standards** | Guide Copilot Code Review toward org rules |

**Instructions file example (concept):**

```markdown
# Project instructions
- Language: TypeScript strict
- Prefer pure functions; no `any`
- Tests: Vitest; name files `*.test.ts`
- Never invent APIs — ask if unsure
- Security: parameterized queries only
```

---

## 2.8 Organization-wide settings and policies

Admins control:

- Which Copilot features are available in **IDEs** and on **github.com**  
- **Code Review** policies  
- Seat/subscription management (including **REST API**)  
- Visibility via **audit log** events  

Full walkthrough: **[labs/04-org-policies.md](./labs/04-org-policies.md)**.

### Exam admin scenarios

| Need | Where |
|---|---|
| Restrict Agent Mode org-wide | Org Copilot policies / feature management |
| Compliance: who changed Copilot settings | Org/Enterprise **audit logs** |
| Automate seat assignment | Copilot subscriptions **REST API** |
| Enforce review assistance | Copilot Code Review policies |

---

## 2.9 Plan-tier awareness ( Domains 2 ↔ 6 )

Memorize with [reference/plan-tiers-cheatsheet.md](./reference/plan-tiers-cheatsheet.md). Highest-yield distinctions:

- **Content exclusions** → Business / Enterprise (not Individual)  
- **IP indemnity** → Business / Enterprise  
- **Fine-tuned / Knowledge Bases / some PR summary features** → often Enterprise  
- **SSO enforcement** → Business+  
- **Audit logs** → Business / Enterprise (detail may differ)

Distractor pattern on exam: answer is usually **one tier above** the tempting wrong option.

---

## Domain 2 quick self-test

1. Agent vs Edit vs Plan — one sentence each.  
2. What does MCP unlock?  
3. Why use Sub-Agents?  
4. Where do org admins restrict IDE vs github.com features?  
5. Name three Enterprise-leaning features commonly tested.
