# Lab 01 — Professionally Set Up GitHub Copilot in IDEs

**Goal:** Install, authenticate, verify, and tune Copilot in VS Code, Visual Studio, and JetBrains like a production-ready engineer.

**Time:** 45–90 minutes  
**Prereqs:** GitHub account with Copilot access (Free/Pro/Business/Enterprise seat)

---

## Part A — Pre-flight (all IDEs)

1. Confirm license:
   - GitHub.com → your avatar → **Copilot** / **Settings → Copilot**
   - Or ask an org admin to assign a seat
2. Confirm org policy isn’t blocking your IDE (Business/Enterprise).
3. Use a work repo **without** production secrets in the working tree for practice.
4. Sign out of stale GitHub sessions in the IDE if you previously used another account.

**Success criteria:** You know which plan you are on before installing anything.

---

## Part B — Visual Studio Code (primary exam IDE)

### B1. Install

1. Open VS Code.
2. Extensions view (`Ctrl+Shift+X` / `Cmd+Shift+X`).
3. Search **GitHub Copilot**.
4. Install **GitHub Copilot** (and **GitHub Copilot Chat** if listed separately in your build).
5. Reload if prompted.

### B2. Authenticate

1. Click the Copilot icon in the status bar, or Command Palette → **GitHub Copilot: Sign in**.
2. Complete browser OAuth to the **correct** GitHub account (the one with the seat).
3. Return to VS Code; wait until status shows Copilot is ready.

### B3. Verify inline suggestions

1. Open a new file `lab01.ts`.
2. Type:

```ts
// Return the sum of even numbers in an array of integers
function sumEven(nums: number[]): number {
```

3. Pause — ghost text should appear.
4. Practice:
   - **Tab** (or configured key) to accept
   - Dismiss / reject
   - Cycle alternate suggestions if available

### B4. Verify Chat

1. Open Copilot Chat.
2. Select the function; ask: `Explain this function and suggest 3 edge-case tests.`
3. Attach the file if not auto-included.
4. Confirm you can start a new thread (history hygiene).

### B5. Professional VS Code settings (examples)

Open Settings JSON and consider (names can vary slightly by version):

```json
{
  "github.copilot.enable": {
    "*": true,
    "plaintext": false,
    "markdown": true,
    "scminput": false
  },
  "editor.inlineSuggest.enabled": true
}
```

Also review UI toggles for:

- Completions on/off per language  
- Public code matching warnings (if exposed in your build)  
- Agent / Edit features availability (may be policy-gated)

### B6. Troubleshooting VS Code

| Problem | Fix |
|---|---|
| “Not signed in” | Sign out GitHub in VS Code Accounts, sign in again |
| Wrong account | Remove unauthorized session; sign into licensed account |
| No ghost text | Check `editor.inlineSuggest.enabled`; check org policy; check file not excluded |
| Chat empty/errors | Network/proxy; update extension; check Copilot service status |

---

## Part C — Visual Studio (Windows)

1. Use a supported Visual Studio version with Copilot workload/components installed (Installer → modify → GitHub Copilot components as listed for your VS version).
2. Sign in to Visual Studio with the Microsoft/GitHub identity linked to your Copilot seat (follow current VS Copilot sign-in docs).
3. Open a code file; confirm completions appear while typing.
4. Open Copilot Chat tool window; ask a repo-local question with selection context.
5. Check **Tools → Options** for Copilot-related settings (enable/disable, filters).

**Professional note:** Keep VS updated — Copilot features track IDE servicing releases.

---

## Part D — JetBrains (IntelliJ IDEA / Rider / etc.)

1. Settings → Plugins → Marketplace → install **GitHub Copilot**.
2. Restart IDE if required.
3. Tools / Copilot menu → **Login to GitHub**; complete device/OAuth flow.
4. Open a source file; verify inline completions.
5. Open Copilot Chat tool window; verify selection-based explain.

JetBrains-specific tips:

- Per-language enablement under Copilot settings  
- Ensure the project trusted/local permissions allow the plugin  
- Corporate proxy: configure IDE HTTP proxy explicitly

---

## Part E — Professional acceptance checklist

- [ ] Correct GitHub identity signed in  
- [ ] Inline suggestion accept/reject works  
- [ ] Chat answers with file/selection context  
- [ ] You know where to disable Copilot for sensitive files locally  
- [ ] You verified org policy isn’t silently blocking Agent/Chat  

---

## Exam linkage

Enabling Copilot “starts with installing the extension/plugin and authenticating to a licensed account” — classic Domain 2 first-step answer.
