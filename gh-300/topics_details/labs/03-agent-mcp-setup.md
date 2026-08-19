# Lab 03 — Agent Mode, Edit/Plan, MCP & Sub-Agents

**Goal:** Professionally configure and operate agentic Copilot workflows with boundaries, MCP tools, and delegated sub-agents.

**Time:** 60–90 minutes  
**Prereqs:** Lab 01 complete; org policy allowing Agent/Edit if on Business/Enterprise

---

## Part A — Choose the right mode (decision tree)

```text
Need a plan only? → Plan Mode / "plan without editing"
Need multi-file edits with selective accept? → Edit Mode
Need autonomous iterate (edit + run + fix)? → Agent Mode
Need external system context (DB, issues, CI)? → Agent + MCP
Need focused side task without polluting context? → Sub-Agent
```

---

## Part B — Plan Mode practice

In Copilot Chat / Agent UI, start a planning session:

```text
Plan how to add rate limiting to our Express API.
Constraints:
- Do not modify files yet
- Prefer existing middleware patterns in this repo
- List files you would touch and risks
- Output a step checklist I can approve
```

**Success:** You get a reviewable plan, no surprise diffs.

---

## Part C — Edit Mode practice

1. Open a small multi-file concern (e.g., rename a type used in 2–3 files).  
2. Start **Edit / Copilot Edits**.  
3. Prompt:

```text
Rename interface UserModel to UserDto across the selected files.
Keep exports stable via type alias if needed.
Do not change runtime behavior.
```

4. Review each proposed hunk.  
5. Accept only correct hunks; reject stylistic noise.  
6. Run tests.

**Exam mapping:** selective multi-file review **without** full terminal autonomy.

---

## Part D — Agent Mode practice (with guardrails)

### D1. Configure operational boundaries in the prompt

```text
GOAL: Add input validation to POST /api/orders using zod.
PERMISSIONS:
- You may edit files under src/api/orders/**
- You may run: npm test -- orders
- You may NOT edit .github/**, prisma/migrations/**, or package.json dependencies
- You may NOT commit, push, or force-push
- If tests fail twice, stop and summarize
DELIVERABLE: diff summary + how to verify manually
```

### D2. Run and observe the loop

Watch for:

- File edits  
- Terminal commands  
- Retry after failure  
- Final summary  

### D3. Human review gate

Before merge:

1. Read diff as if a junior authored it.  
2. Run full test suite.  
3. Check for secrets or broad permissions changes.  
4. Open PR; optionally request Copilot Code Review.

---

## Part E — MCP setup (professional pattern)

MCP connects Copilot agents to external tools via MCP servers.

### E1. Identify a safe local MCP use case

Examples:

- Read-only filesystem docs server  
- Issue tracker read access  
- Local DB schema introspection (non-prod)

### E2. Configure MCP in your Copilot/IDE MCP settings

Exact UI varies; typical professional steps:

1. Open Copilot / IDE **MCP** configuration (settings JSON or UI).  
2. Register a server with name, command, args, env.  
3. Restart Chat/Agent session.  
4. Verify tools appear as available to the agent.  
5. Test with a read-only prompt.

**Example shape (illustrative):**

```json
{
  "mcpServers": {
    "docs": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "./docs"],
      "env": {}
    }
  }
}
```

### E3. Security hardening for MCP

| Control | Practice |
|---|---|
| Least privilege | Read-only servers first |
| Secrets | Inject via env vaults; never hardcode in repo |
| Network | Prefer local/dev endpoints over prod |
| Approval | Require human approval for write tools |
| Inventory | Document approved MCP servers for the team |

**Exam definition:** MCP = protocolized integration of external tools/context into agent workflows.

---

## Part F — Sub-Agents

### When to delegate

- Generate fixtures while parent implements feature  
- Research a library API  
- Isolate a flaky test investigation  

### Example delegation prompt

```text
Parent task: implement CSV export for invoices.
Sub-agent A: propose column schema + 5 sample rows (fake data only).
Sub-agent B: draft unit tests for CSV escaping edge cases.
I will integrate results after review.
```

**Why:** optimized/isolated context; parent stays focused.

---

## Part G — Acceptance checklist

- [ ] Produced a Plan-only response with no unwanted edits  
- [ ] Completed an Edit Mode selective accept  
- [ ] Completed an Agent Mode task with explicit negative constraints  
- [ ] Configured or walked through an MCP server safely  
- [ ] Explained Sub-Agent value in one sentence  
- [ ] Documented that exclusions may not bind Agent the same as inline  

---

## Failure patterns to avoid (exam + real life)

1. Agent with no path constraints on a monorepo.  
2. MCP write access to production.  
3. Assuming content exclusions stop Agent Mode.  
4. Merging Agent output because “tests passed once.”
