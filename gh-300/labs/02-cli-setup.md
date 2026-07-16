# Lab 02 — Professionally Set Up GitHub Copilot CLI

**Goal:** Install Copilot CLI, authenticate, run interactive sessions, generate scripts, and understand exclusion limitations.

**Time:** 30–60 minutes  
**Prereqs:** GitHub CLI (`gh`) recommended; Copilot-enabled account

> CLI surfaces evolve. Treat command names below as **capability targets**. If a subcommand differs, use `gh copilot --help` / current docs and map to the same skills.

---

## Part A — Install GitHub CLI (if needed)

### Windows (winget)

```powershell
winget install --id GitHub.cli -e
gh --version
```

### macOS (Homebrew)

```bash
brew install gh
gh --version
```

### Linux

Follow [GitHub CLI installation](https://github.com/cli/cli#installation) for your distro.

---

## Part B — Authenticate

```bash
gh auth login
# Choose GitHub.com → HTTPS → Login with browser (or token)
gh auth status
```

Ensure the authenticated account **has Copilot**.

Install/enable Copilot CLI extension or bundled Copilot CLI per current docs, for example:

```bash
gh extension install github/gh-copilot
# or follow the current "GitHub Copilot CLI" install path from docs.github.com
gh copilot --help
```

---

## Part C — Core capabilities (hands-on)

### C1. Explain a command

```bash
gh copilot explain "find . -type f -name '*.log' -mtime -1 -print0 | xargs -0 tar -czf logs.tgz"
```

**Learning check:** Can you restate the pipeline in plain English without running it?

### C2. Suggest a command from intent

```bash
gh copilot suggest "list the 10 largest directories under the current folder"
```

**Professional habit:** Read the suggestion; do **not** pipe unknown commands to `sudo` blindly.

### C3. Interactive session

Start an interactive Copilot CLI session (command per current help):

```bash
gh copilot
# or: gh copilot session
```

Try a multi-turn task:

```text
Help me write a bash script that:
1) finds TODO comments in *.ts files
2) writes paths to todos.txt
3) exits non-zero if more than 50 hits
Ask me clarifying questions before writing the script.
```

### C4. Generate and manage a script file

Prompt:

```text
Create script scripts/check-todos.sh with set -euo pipefail.
Add usage help. Target bash 5. Do not overwrite without confirming.
```

Then:

1. Read the file.  
2. Run `shellcheck` if available.  
3. Execute on a sample tree.  
4. Commit only after review.

---

## Part D — Professional CLI safety rules

| Rule | Why |
|---|---|
| Never paste tokens/secrets into prompts | Prompt may be retained longer on CLI/agent paths |
| Prefer dry-run flags first | Destructive suggestions happen |
| Quote paths with spaces | Generated scripts often miss edge quoting |
| Pin tool versions in scripts | Reproducibility |
| Remember exclusions gap | **Content exclusions may not apply to CLI** |

---

## Part E — Exclusion awareness drill (exam-critical)

1. Add a dummy file `secrets/dummy.env` with fake keys in a test repo.  
2. Configure a content exclusion for `/secrets/**` (Lab 05) if you have Business/Enterprise.  
3. In IDE Chat on supported surfaces, confirm refusal/limited use.  
4. In CLI, observe that agentic/CLI behavior may still differ — document what you see.  
5. Write one paragraph: “Why exclusions alone are insufficient for CLI/Agent.”

---

## Part F — Acceptance checklist

- [ ] `gh auth status` shows correct user  
- [ ] Explain works on a non-trivial command  
- [ ] Suggest produces a reviewable command  
- [ ] Interactive multi-turn session completed  
- [ ] Generated script reviewed before execution  
- [ ] You can explain CLI vs IDE exclusion differences  

---

## Exam linkage

Primary benefit of Copilot CLI: brings assistant workflows into the **terminal** for scripting/file tasks — not replacing remotes or hosting databases.
