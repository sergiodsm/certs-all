# GH-300 GitHub Copilot — Certification Prep & Practice Questions

> **Companion to** [GH300-Study-Guide.md](GH300-Study-Guide.md). This file refreshes the
> documentation against the **current official skills outline** and adds **10 exam-style
> questions with answers and explanations for every topic**.
>
> **Exam:** Microsoft **GH-300: GitHub Copilot**
> **Skills outline used:** *Skills measured as of **August 7, 2026*** (verified against Microsoft Learn)
> **Last verified:** 2026-07-09

---

## 0. What changed vs. the older study guide (read this first)

The existing [GH300-Study-Guide.md](GH300-Study-Guide.md) was written against a "January 2026"
outline. I verified the live Microsoft Learn study guide (skills measured **as of August 7, 2026**)
and corrected the following:

| Item | Old guide said | **Verified / corrected** |
|------|----------------|--------------------------|
| Skills outline date | January 2026 | **August 7, 2026** (current) |
| Certification validity | "2 years" / "1 year (verify)" | **Renews annually** — Microsoft associate/specialty certs expire yearly; renew via a **free online assessment on Microsoft Learn** |
| Passing score | 700/1000 | ✅ Correct — **700 on a 1000-point scale** |
| Question count | ~65 graded | ✅ Correct — **~65** (fluctuates slightly) |
| Time limit | 100 minutes | ✅ Correct — **100 minutes** |
| Localized-language delay | ~8 weeks | ✅ Correct — localized versions update **~8 weeks** after English; **+30 min** available if exam not in your language |
| Domain structure | 7 numbered domains | Official **"skills at a glance"** lists 7 lines, but **"Use GitHub Copilot features"** appears **twice at 25–30%** — treat features/admin as one combined **~50%** block |

### Official skills at a glance (verbatim weightings)

| Skill area | Weight |
|-----------|--------|
| Use GitHub Copilot responsibly | 15–20% |
| Use GitHub Copilot features | 25–30% |
| GitHub Copilot features *(listed a second time)* | 25–30% |
| Understand GitHub Copilot data and architecture | 10–15% |
| Apply prompt engineering and context crafting | 10–15% |
| Improve developer productivity with GitHub Copilot | 10–15% |
| Configure privacy, content exclusions, and safeguards | 10–15% |

**Study takeaway:** Features + CLI + org administration is the single largest scoring block
(~50%). Prioritize it, then Responsible AI, then everything else.

### Verified subtopics (from the live outline)

- **Responsible AI:** risks/limitations of GenAI, ethical use, harms + mitigations, need to
  validate output, operating Copilot responsibly.
- **Features — IDE:** enable in IDE; trigger via inline, chat, CLI, **agent mode**; configure
  content exclusions (app knowledge).
- **Features — CLI:** define Copilot CLI + benefits; install steps; key features/commands;
  interactive and session use; generate scripts / manage files.
- **Features — capabilities:** Agent Mode, Copilot Edits, **MCP**; Agent Sessions +
  **Sub-Agents** for context optimization; code review + coding assistance; **Spaces, Spark,
  PR summaries, instructions files**; Chat limits/options/feedback/commands + **prompt file reuse**.
- **Features — org settings:** org-wide policy management; **Copilot Code Review policies**;
  feature availability across IDEs and github.com; **audit log** events; **REST API** for subscriptions.
- **Data & architecture:** data usage/flow/sharing; input processing + prompt building; proxy
  filtering + post-processing; suggestion **lifecycle**; LLM/Copilot limitations.
- **Prompt engineering:** prompt structure + context; how context is determined; zero-shot vs
  few-shot; best practices; prompt engineering principles; prompt process flow + chat history.
- **Productivity:** code generation/refactoring/documentation; accelerate learning + reduce
  context switching; sample data + legacy modernization; unit/integration tests; edge cases +
  assertions; security improvements + performance optimizations.
- **Privacy & safeguards:** content exclusions + editor settings; ownership + limitations of
  outputs; **suggestions matching public code** filtering; troubleshoot suggestions/exclusions.

**Sources:**
[GH-300 study guide (Microsoft Learn)](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/gh-300) ·
[GitHub Copilot certification page](https://learn.microsoft.com/en-us/credentials/certifications/github-copilot/) ·
[Exam scoring & score reports](https://learn.microsoft.com/en-us/credentials/certifications/exam-scoring-reports) ·
[GitHub Trust Center (data handling)](https://github.com/trust-center) ·
[Content exclusion docs](https://docs.github.com/copilot/managing-copilot/configuring-and-auditing-content-exclusion)

---

## How to use the question banks below

- Each of the **7 topics** has **10 questions**, each with the **correct answer** and a
  **short explanation** of *why it's right and why the traps are wrong*.
- Cover the answer, commit to a choice, then reveal. Log misses by topic.
- Watch for the recurring exam traps flagged with ⚠️.

---

## Study order: hardest → easiest

Difficulty here is **how hard the topic is to study and keep straight on exam day** — not exam
weight. Weight still matters: spend extra time on anything that is both hard *and* high-scoring.

Study the hard topics first while attention is high. Revisit them after the easy ones so the
gotchas stick. Daily Copilot users can skim Topics 5–6; almost nobody should skim Topics 2, 3,
or 7.

| Rank | Difficulty | Topic | Weight | Why it is this hard (or easy) |
|------|------------|-------|--------|-------------------------------|
| 1 | Hardest | [Topic 2 — Features: IDE, Chat & Modes](#topic-2) | 25–30% | Huge product surface. Agent vs Edits vs Plan, MCP, Sub-Agents, Spaces, Spark, PR summaries, instructions files, prompt files, Chat commands. Names evolve; mode-selection traps are frequent. |
| 2 | Very hard | [Topic 7 — Privacy, exclusions & safeguards](#topic-7) | 10–15% | Highest *gotcha density*. Exclusions do **not** fully apply to Agent/CLI; public-code filter naming; ownership vs responsibility; plan-tier gating; troubleshooting. Easy to overgeneralize. |
| 3 | Hard | [Topic 3 — Features: CLI & org administration](#topic-3) | 25–30% | Separate CLI install + different data rules. Org policies, Code Review policies, audit logs, REST API for subscriptions. Many candidates never see the admin UI. |
| 4 | Hard | [Topic 4 — Data and architecture](#topic-4) | 10–15% | Abstract pipeline: prompt building → proxy filtering → model → post-processing → lifecycle. Retention/training depends on **plan + surface**; CLI/Agent ≠ IDE. Absolutist answers fail. |
| 5 | Moderate | [Topic 5 — Prompt engineering](#topic-5) | 10–15% | Small, stable concept set (structure, context, zero-shot vs few-shot, iteration, chat history). Overlaps Topic 2 on prompt/instructions files. Daily users already know most of it. |
| 6 | Easier | [Topic 1 — Responsible AI](#topic-1) | 15–20% | Short fact set: validate output, human accountability, hallucination, harms/mitigations, fairness vs inclusiveness. Concepts are simple; the trap is treating it as isolated trivia instead of a lens on every other domain. |
| 7 | Easiest | [Topic 6 — Developer productivity](#topic-6) | 10–15% | Maps to daily work: generate, refactor, docs, tests, sample data, legacy modernization, security/perf. Main trap (“tests passed ⇒ ship”) is really a Topic 1 overlay. |

### What to drill on the hard topics

1. **Topic 2** — Pick the right *surface* for the job (inline / Chat / Edits / Agent / CLI). Know
   MCP, Sub-Agents, instructions files vs prompt files, and what org policy can turn off.
2. **Topic 7** — Content exclusions: what they stop, **where they do not apply**, and that they
   are not a secret vault. Public-code matching = **Block**. GitHub does **not** claim ownership
   of suggestions; you remain responsible.
3. **Topic 3** — CLI is installed separately. Org/Enterprise: feature policies, Code Review
   policies, audit logs, subscription REST API. Recite plan-tier differences from memory.
4. **Topic 4** — Draw the suggestion lifecycle once from memory. Never pick “all plans train on
   private code” or “nothing is ever retained.” Check current docs for plan + surface.

### Suggested pass order (not the official outline order)

```text
Pass 1 (depth):  Topic 2 → Topic 7 → Topic 3 → Topic 4
Pass 2 (faster): Topic 5 → Topic 1 → Topic 6
Pass 3 (mix):    miss-log from the question banks + exam traps
```

Weight reminder: Topics 2 + 3 together are ~50% of the exam. Topic 1 is the next largest
(15–20%). Do not confuse “easier to study” with “safe to skip.”

---

<a id="topic-1"></a>

## Topic 1 — Use GitHub Copilot Responsibly (15–20%)

**Q1.** A developer accepts a Copilot-generated SQL query and deploys it straight to production.
What should have happened first?
- A) Nothing — Copilot is trained on high-quality code
- B) Human review, testing, and a security check before merge
- C) Disable Copilot for that developer
- D) Switch to a different model

**Answer: B.** The single most-tested Responsible-AI principle is that **AI output must be
validated by a human** for correctness, security, and licensing before shipping. "Trust the
brand" (A) is always wrong; disabling the tool (C) is disproportionate; the model (D) isn't the issue.

**Q2.** Which of the following is a genuine *limitation* of generative AI that Copilot inherits?
- A) It can only write Python
- B) It may **hallucinate** APIs, packages, or facts that don't exist
- C) It cannot run in an IDE
- D) It requires the internet only on Enterprise

**Answer: B.** Hallucination — confident but false output — is a core limitation, alongside stale
training data, limited context, and potential bias. The others are simply untrue.

**Q3.** In Responsible AI, what does **transparency** mean?
- A) Hiding which model version is used
- B) Helping users understand *how* suggestions are generated and filtered
- C) Always choosing the most popular IDE
- D) Removing documentation

**Answer: B.** Transparency = users understand the system's behavior and limits. ⚠️ Don't confuse
it with "trust the vendor." A, C, D are distractors.

**Q4.** Agent Mode autonomously completes a multi-file change and runs the tests. What's the
responsible next step?
- A) Auto-merge because the agent ran tests
- B) Review the diff, run CI, and validate security before merging
- C) Delete the branch
- D) Turn off MCP

**Answer: B.** Autonomy is **not** approval to ship. Agentic tools need **more** oversight, not
less — review + CI + human accountability remain mandatory.

**Q5.** Which pairing best captures the pillars of responsible AI use with Copilot?
- A) Speed + brevity
- B) Accountability + transparency + fairness + safety/security
- C) Cost + coverage
- D) Popularity + familiarity

**Answer: B.** The human remains **accountable**; the system should be **transparent**, **fair/
inclusive**, and **safe/secure**. This framing recurs across scenario questions.

**Q6.** Copilot suggests a snippet that closely matches code from a public repository. The
responsible response is to:
- A) Ship it — public code is free to use
- B) Rely on **duplication detection / public-code matching**, review the license, and have a
  human decide
- C) Rename the variables and ship
- D) Disable Chat

**Answer: B.** Public-code matches raise **IP/license risk**. Use the public-code filter and human
review; superficial renaming (C) doesn't resolve licensing.

**Q7.** A team notices Copilot suggestions reflect a bias present in its training data. Best
mitigation?
- A) Ignore it unless users complain
- B) Validate outputs, apply org policies, and use diverse human review
- C) Only write longer prompts
- D) Disable inline suggestions permanently

**Answer: B.** Harm mitigation combines **validation + governance + human review**. Prompt length
alone (C) doesn't address bias; blanket disabling (D) is disproportionate.

**Q8.** Which statement about accountability for Copilot's output is correct?
- A) GitHub owns and is responsible for all generated code
- B) The LLM vendor is liable for correctness
- C) The **developer/organization using the output** is responsible for validating and using it
- D) No one is responsible for AI output

**Answer: C.** You own what you ship. Copilot assists; humans remain accountable for correctness,
security, and licensing.

**Q9.** What is the difference between **fairness** and **inclusiveness** as responsible-AI concepts?
- A) They are identical
- B) Fairness targets **equitable outcomes**; inclusiveness targets **broad representation/access**
- C) Fairness is a plan tier; inclusiveness is a filter
- D) Inclusiveness means faster suggestions

**Answer: B.** ⚠️ Both appear as distractors in the same question — know the distinction. Neither
is a product feature.

**Q10.** Why does Responsible AI "thread through" nearly every other GH-300 domain?
- A) It doesn't — it's isolated to one section
- B) Because governance, privacy, productivity, and features all require validating outputs and
  human oversight
- C) Because it's the only graded domain
- D) Because it replaces prompt engineering

**Answer: B.** Treat every governance/feature scenario as also having a responsible-use angle:
validate, oversee agents, respect licensing and privacy.

---

<a id="topic-2"></a>

## Topic 2 — Use GitHub Copilot Features: IDE, Chat & Modes (25–30%)

**Q11.** What are the four primary ways to trigger Copilot in the IDE per the official outline?
- A) Inline suggestions, chat, CLI, and **agent mode**
- B) Email, SMS, chat, and voice
- C) Git hooks, Actions, webhooks, and chat
- D) Only inline suggestions

**Answer: A.** The outline explicitly lists inline, chat, CLI, and agent mode as trigger surfaces.

**Q12.** In VS Code, how do you accept an inline (ghost-text) suggestion by default?
- A) Enter
- B) **Tab**
- C) Ctrl+S
- D) Right-click → Accept

**Answer: B.** Tab accepts inline suggestions; you can cycle alternatives with Alt+]/Alt+[.

**Q13.** Which mode is designed for **autonomous, multi-step** implement → run → fix loops with
tool use?
- A) Inline completion
- B) **Agent Mode**
- C) Plain Chat Q&A
- D) Edit Mode

**Answer: B.** Agent Mode plans and executes multi-step changes and can invoke tools. Edit Mode
(D) is for **targeted, scoped** multi-file edits — less autonomous.

**Q14.** A developer wants to rename a symbol and adjust three related files in one scoped
operation, without full autonomy. Best fit?
- A) Agent Mode
- B) **Copilot Edits / Edit Mode**
- C) Inline single-line completion
- D) Copilot CLI only

**Answer: B.** Copilot Edits applies targeted, reviewable edits across a defined set of files —
the right level of control for a scoped refactor.

**Q15.** What does **MCP (Model Context Protocol)** provide?
- A) A replacement for Git
- B) A **standard protocol** to connect Copilot agents to external tools and data sources
- C) A way to bypass all content filters
- D) Automatic training on private repos

**Answer: B.** ⚠️ MCP is an **open standard** (Anthropic-origin) that Copilot uses for tool/data
integration — not Copilot-proprietary and not a filter bypass.

**Q16.** What problem do **Sub-Agents** in Agent Sessions primarily solve?
- A) Billing reconciliation
- B) **Context optimization** — delegating subtasks so the main agent's context stays focused
- C) Replacing CI pipelines
- D) Enforcing SSO

**Answer: B.** Sub-Agents let you delegate subtasks, keeping context lean and results organized
within Agent Sessions.

**Q17.** **Copilot Spaces** are best described as:
- A) A disk partition for repos
- B) **Shared, curated context/knowledge** that teams can reuse with Copilot
- C) A CLI session log
- D) An SSH tunnel

**Answer: B.** Spaces bundle relevant context (docs, code, instructions) so team responses are
consistent and grounded.

**Q18.** **GitHub Copilot Spark** is associated with:
- A) Database sharding
- B) **Building apps** with Copilot (app-building experience)
- C) DNS configuration
- D) Kernel tuning

**Answer: B.** Spark is GitHub's Copilot-powered app-building experience. Availability varies by plan.

**Q19.** What is the purpose of an **instructions file** (e.g., custom instructions / review
standards) for Copilot?
- A) A one-time throwaway prompt
- B) **Persistent, reusable project conventions** that shape Copilot's responses and review standards
- C) A billing manifest
- D) A replacement for `.gitignore`

**Answer: B.** Instructions files encode durable team standards so Copilot's suggestions and
code-review behavior stay consistent — related to **prompt file reuse**.

**Q20.** Which statement about **Copilot Code Review** on pull requests is correct?
- A) It automatically merges approved PRs
- B) It provides **automated review feedback**; humans still merge; org **policies** control
  availability
- C) It's available only on the Free plan
- D) It deletes failing branches

**Answer: B.** ⚠️ Copilot **never auto-merges**. It reviews/comments; a human merges. Code Review
availability is governed by org policy.

---

<a id="topic-3"></a>

## Topic 3 — Use GitHub Copilot Features: CLI & Org Administration (25–30%)

**Q21.** Which best describes the **GitHub Copilot CLI**?
- A) A browser extension
- B) A **terminal-based agent** for interactive sessions, script generation, and file management
- C) A billing dashboard
- D) A replacement for `git`

**Answer: B.** The CLI brings Copilot into the terminal for interactive help, session-based work,
generating scripts, and managing files.

**Q22.** How is the Copilot CLI obtained?
- A) It's bundled automatically with every IDE
- B) It requires a **separate installation** (its own setup step)
- C) It only exists on Linux from the 1990s
- D) It cannot be installed

**Answer: B.** The CLI is installed separately from the IDE extensions. ⚠️ It also has **different
data-handling rules** than inline IDE use (see Topic 4).

**Q23.** Can the Copilot CLI be used **interactively and in sessions**?
- A) **Yes** — interactive use and sessions are supported
- B) No, it's batch-only
- C) Only via webhooks
- D) Only on Enterprise

**Answer: A.** The outline explicitly covers interactive and session-based CLI usage, plus script
generation and file management.

**Q24.** ⚠️ Does **content exclusion** protect files from the **Copilot CLI**?
- A) Yes, always
- B) **No** — content exclusion does not apply to the CLI (or the coding agent / Agent Mode in Chat)
- C) Only on Free
- D) Only for `.env` files

**Answer: B.** This is the highest-frequency trap on the exam. Content exclusion covers inline/
chat context in the IDE — **not** CLI, coding agent, or Agent Mode. Use other controls there.

**Q25.** An admin needs to turn Copilot Code Review on for **all repositories** in the org. This
is done via:
- A) Each developer's personal settings
- B) **Organization-wide policy management** (Code Review policy)
- C) A `git config` flag
- D) It's impossible

**Answer: B.** Org owners manage feature availability and Code Review policies centrally across
IDEs and github.com.

**Q26.** Which tool answers "**who changed a Copilot policy, and when?**"
- A) `git blame`
- B) The **audit log** (Business/Enterprise)
- C) The README
- D) Chat history

**Answer: B.** Audit log events record administrative actions on Copilot settings. Available on
Business/Enterprise-tier organizations.

**Q27.** An organization wants to **automate seat/subscription management** for Copilot. The
correct mechanism is:
- A) The **REST API** for Copilot subscriptions
- B) Editing each user's `.gitconfig`
- C) A Slack bot only
- D) Manual spreadsheet, no API exists

**Answer: A.** The outline lists managing subscriptions **using the REST API** (assign/remove
seats, query usage) as an admin skill.

**Q28.** A required feature works in Visual Studio but is **disabled in VS Code** for the same
user. Most likely cause?
- A) The LLM is down
- B) **Admin-managed feature availability** differs per IDE surface
- C) The keyboard is broken
- D) The repo was deleted

**Answer: B.** Admins can manage feature availability **across IDEs and github.com**, so a feature
can be enabled on one surface and not another.

**Q29.** Scenario: a startup needs **org-wide policy management, SAML SSO enforcement, and content
exclusion** for `**/credentials/**`. What is the **lowest** plan that satisfies all requirements?
- A) Pro
- B) Pro+
- C) **Business**
- D) Free

**Answer: C.** ⚠️ Content exclusion, IP indemnity, org policy management, and SAML SSO enforcement
start at **Business**. Enterprise is only required if they also need fine-tuned models, Knowledge
Bases, advanced PR summaries, or Bing-grounded web search. Pick the **lowest tier meeting all
requirements** — Enterprise here would be over-provisioning.

**Q30.** Which capability is typically **Enterprise-only** (not Business)?
- A) Basic inline completion
- B) Copilot Chat
- C) **Fine-tuned models / Knowledge Bases**
- D) Accepting suggestions with Tab

**Answer: C.** Fine-tuned models and Knowledge Bases (and advanced PR summaries / Bing-grounded
web search) sit at the **Enterprise** tier; the basics exist on every plan.

---

<a id="topic-4"></a>

## Topic 4 — Understand GitHub Copilot Data and Architecture (10–15%)

**Q31.** In the Copilot request pipeline, where does the **proxy** sit?
- A) Inside the IDE only
- B) **Between the client (IDE/CLI) and the LLM**, handling pre- and post-processing
- C) After the code is merged
- D) In the git remote

**Answer: B.** The proxy (GitHub/Azure) is central: it pre-processes the request and post-processes
the response — it is **not** optional decoration.

**Q32.** Which is an example of **pre-processing** by the proxy?
- A) Merging the PR
- B) **Toxicity and relevance checks** / prompt building before the LLM sees it
- C) `npm install`
- D) Deleting the repo

**Answer: B.** Pre-processing builds/filters the prompt (toxicity, relevance, policy) before it
reaches the model.

**Q33.** Which happens during **post-processing**?
- A) Public-code matching, security/quality checks, and possible discard/truncation of the suggestion
- B) Increasing developer salary
- C) Rotating SSH keys
- D) Auto-starring the repo

**Answer: A.** After generation, the proxy applies security scanning, quality checks, and
**public-code matching**, and may block/truncate/discard the suggestion.

**Q34.** A developer gets **no inline suggestion**, but Chat works and the file isn't excluded.
What's the *best first* hypothesis?
- A) "The LLM is permanently down"
- B) **Post-processing blocked it** (e.g., public-code match) or an editor/extension/empty-context issue
- C) The repo was deleted
- D) SSO expired

**Answer: B.** Empty/insufficient context or a post-processing block is far more likely than a
model outage. Diagnose context, filters, and extension state first.

**Q35.** For **Business/Enterprise IDE** usage, how are prompts and suggestions retained for model
training?
- A) Retained forever
- B) **Not retained for training** — zero data retention after processing under the enterprise policy
- C) Retained 10 years
- D) Retained only on weekends

**Answer: B.** Business/Enterprise IDE prompts/suggestions are **not used to train models** and are
not retained after processing.

**Q36.** ⚠️ How does data handling for **CLI / agent workflows** differ from inline IDE use?
- A) It's identical
- B) CLI/agent data may be retained **~28 days for abuse monitoring** (not model training)
- C) CLI data is retained forever
- D) CLI data is never processed

**Answer: B.** The exam tests that interfaces differ: IDE (Business+) is zero-retention, while
CLI/agent flows keep data ~28 days for **abuse/misuse monitoring**, distinct from training.

**Q37.** For **individual (Free/Pro)** users, can prompts be used to improve the product/models?
- A) Never under any setting
- B) It **depends on user settings** — individuals can opt out of their data being used for training
- C) Always, with no control
- D) Only on Enterprise

**Answer: B.** Individual plans expose a training/telemetry **opt-out** in settings; enterprise
plans don't train on customer prompts at all.

**Q38.** How does **telemetry** retention typically compare to prompt retention?
- A) Telemetry is deleted instantly
- B) Telemetry (usage analytics) is retained **longer** (e.g., ~2 years) and is a separate policy
  from prompt/suggestion handling
- C) They're the same policy
- D) Telemetry is never collected

**Answer: B.** ⚠️ Keep **telemetry ≠ prompt retention** straight — they follow different policies
and timelines.

**Q39.** Which is a real **limitation of the LLM** behind Copilot that appears on the exam?
- A) It has infinite context
- B) It **doesn't know your private/undeclared context** unless that context is provided
- C) It's always license-aware with no configuration
- D) It cannot generate tests

**Answer: B.** Models are bounded by context window and training data; private code/intent must be
**supplied**. It's not automatically license-aware — that's what public-code filtering is for.

**Q40.** Which diagram best captures the suggestion lifecycle?
- A) `IDE → LLM → IDE` (no intermediary)
- B) `IDE → Proxy (pre: toxicity/relevance/policy) → LLM → Proxy (post: security/public-code/quality) → IDE`
- C) `IDE → GitHub Actions → IDE`
- D) `LLM → IDE → Proxy`

**Answer: B.** Context is gathered, pre-processed, sent to the LLM, post-processed (including
public-code matching), then delivered. The proxy is on both legs.

---

<a id="topic-5"></a>

## Topic 5 — Apply Prompt Engineering and Context Crafting (10–15%)

**Q41.** What does **zero-shot** prompting mean?
- A) Prompting with **no examples** — relying on a clear instruction
- B) Prompting with three examples
- C) Prompting without an internet connection
- D) Prompting without an IDE

**Answer: A.** Zero-shot = instruction only, no examples. Best for standard, well-defined tasks.

**Q42.** When is **few-shot** prompting the better choice?
- A) For a trivial `for` loop
- B) When the desired pattern is **unusual or stylistic** and 1–3 examples clarify intent
- C) When you're offline
- D) Never — it's deprecated

**Answer: B.** Provide examples when the pattern is non-obvious (e.g., an odd internal JSON
envelope). ⚠️ Few-shot for a standard loop is overkill.

**Q43.** The "Four Ss" of effective prompts are:
- A) Speed, Size, Style, Syntax
- B) **Single, Specific, Short, Surrounded**
- C) Simple, Safe, Secure, Static
- D) Search, Scan, Sort, Ship

**Answer: B.** One task (Single), clear constraints/stack (Specific), concise but complete (Short),
and provide code context (Surrounded).

**Q44.** Copilot keeps suggesting the **wrong framework/version**. The most likely fix is:
- A) The proxy is offline
- B) Add the **framework/version and file context** the prompt is missing
- C) Reinstall the OS
- D) The Tab key is broken

**Answer: B.** Missing context is the usual culprit. State the framework, version, and relevant
surrounding code or `@`-references.

**Q45.** How does Copilot **determine context** for a suggestion?
- A) Only from the current line
- B) From **open files, the current selection, comments, and referenced files** (per settings/exclusions)
- C) From your email
- D) From random public repos

**Answer: B.** Context comes from the working set — open tabs, selection, nearby comments, and
explicit references — subject to content-exclusion settings.

**Q46.** The prompt-engineering principle **"Single"** means:
- A) One programming language per repository
- B) **One clear task per prompt**
- C) One character per line
- D) One user per org

**Answer: B.** Split multi-task "walls of text" into focused, single-objective prompts for higher-
quality output.

**Q47.** Rewrite this weak prompt for best results: *"Add error handling."*
- A) "Fix everything"
- B) "In `UserService.create()`, add try/catch for `DbException`, log with a correlation ID, and
  return `Result.Fail`, following the existing `OrderService` pattern"
- C) "Make it better"
- D) "Handle errors sometime"

**Answer: B.** It's **Specific + Surrounded + Single**: names the method, the exception, the
logging, the return contract, and an existing pattern to mirror.

**Q48.** What role does **chat history** play in a Copilot Chat session?
- A) It replaces git history
- B) It provides **conversational context** within the session (but can dilute focus if overly long)
- C) It deletes content exclusions
- D) It enables IP indemnity

**Answer: B.** History threads context across turns; keep it relevant — long, off-topic history
reduces answer quality.

**Q49.** How do **instructions files / prompt files** improve prompt engineering at team scale?
- A) They randomize responses
- B) They enable **reuse of consistent conventions/prompts** so responses are repeatable across the team
- C) They disable Chat
- D) They increase font size

**Answer: B.** Reusable prompt/instruction files encode standards once and apply them everywhere,
giving consistent Copilot behavior.

**Q50.** When Copilot output is poor, what should you check **first**?
- A) Your keyboard layout
- B) **Context**, then **specificity** — is the right code/framework/intent present in the prompt?
- C) The GitHub logo color
- D) The day of the week

**Answer: B.** Diagnose context and specificity before anything else; that resolves most poor
suggestions.

---

<a id="topic-6"></a>

## Topic 6 — Improve Developer Productivity (10–15%)

**Q51.** Which is the strongest **unit-test** prompt?
- A) "test this"
- B) "Generate xUnit tests for `CalculateTax` covering zero income, negative income, and a bracket
  boundary, with explicit assertions"
- C) "delete tests"
- D) "merge the PR"

**Answer: B.** Name the **framework**, enumerate **edge cases**, and ask for **assertions** — the
outline's testing best practice.

**Q52.** For an **integration-test** prompt, you must include:
- A) Only the function name
- B) **External dependencies, mock strategy, and expected inputs/outputs**
- C) The user's password
- D) A license key

**Answer: B.** Integration tests exercise collaborators — specify deps, mocks/fakes, and expected
IO so the generated tests are meaningful.

**Q53.** How does Copilot **reduce context switching** while learning a codebase?
- A) By auto-deploying to production
- B) By **explaining unfamiliar code in-editor**, so you stay in flow instead of searching docs
- C) By replacing CI
- D) By deleting the wiki

**Answer: B.** In-editor explanations accelerate learning and cut back-and-forth to external docs.

**Q54.** A good approach to **refactoring** with Copilot is to:
- A) Ask it to refactor the whole repo blindly
- B) **Select a scoped block and specify the desired pattern** (extract, rename, apply pattern)
- C) Empty the chat and hope
- D) Disable Copilot

**Answer: B.** Small, scoped selections plus an explicit target pattern yield safe, reviewable
refactors.

**Q55.** The recommended strategy for **legacy modernization** is:
- A) A single blind full rewrite
- B) **Incremental refactors with validation** at each step, describing the target stack
- C) Delete the legacy code
- D) Skip tests to move faster

**Answer: B.** Modernize in validated increments; a one-shot rewrite without review is high-risk
and contradicts responsible-use principles.

**Q56.** Copilot can generate **sample/fixture data**. This is:
- A) Forbidden by the exam
- B) A **legitimate productivity use case** — generate fixtures under stated constraints
- C) Illegal
- D) Only possible in Java

**Answer: B.** Generating constrained sample data (for tests/demos) is an endorsed productivity use.

**Q57.** When using Copilot for **security improvements**, you should:
- A) Ship its suggestions directly
- B) **Review suggestions and run security tooling/SAST** alongside them
- C) Disable all filters
- D) Paste secrets into the prompt for context

**Answer: B.** Copilot can suggest input validation, parameterized queries, and OWASP-aligned
fixes — but combine with human review and scanners. Never paste secrets (D).

**Q58.** For **performance optimization**, an effective prompt asks Copilot to:
- A) "make it fast"
- B) **Identify likely bottlenecks/hotspots and propose specific optimizations** for the given code
- C) Rewrite in assembly always
- D) Buy more RAM

**Answer: B.** Ask for bottleneck analysis and concrete, contextual optimizations you can measure.

**Q59.** Which task is **out of scope** for Copilot's role?
- A) Generating docstrings
- B) Suggesting edge-case tests
- C) **Automatically approving and merging PRs** on the developer's behalf
- D) Explaining selected code

**Answer: C.** ⚠️ Copilot **assists** with review/summaries but does **not** approve or merge — a
human owns the merge decision.

**Q60.** Best practice when Copilot **generates tests**?
- A) Trust them without running
- B) **Run them and review** — generated tests can be wrong or miss cases
- C) Delete them if they're green
- D) Never write assertions

**Answer: B.** Generated tests are a starting point; execute and review them before relying on the
coverage they claim.

---

<a id="topic-7"></a>

## Topic 7 — Configure Privacy, Content Exclusions, and Safeguards (10–15%)

**Q61.** What does a **content exclusion** rule do (where it applies)?
- A) Deletes the file from git
- B) **Prevents Copilot from using excluded paths** — no inline suggestions in the file and the
  content isn't used as context elsewhere; Chat refuses to analyze it
- C) Encrypts the repository
- D) Blocks all internet access

**Answer: B.** Exclusions stop Copilot from reading/suggesting in the matched paths (e.g.,
`**/*.env`, `/secrets/**`) within supported surfaces.

**Q62.** ⚠️ Content exclusion does **NOT** apply to which of the following?
- A) Inline suggestions in the IDE
- B) Chat context in the IDE
- C) **Copilot CLI, the coding agent, and Agent Mode in Chat**
- D) Using excluded files as context in other IDE files

**Answer: C.** The most repeated safeguard trap: exclusions cover IDE inline/chat context, **not**
CLI/coding-agent/Agent-Mode. Protect those with agent instructions, secret scanning, and RBAC.

**Q63.** An admin updates exclusions, but a developer still sees suggestions in the excluded file.
Why?
- A) Exclusions never work
- B) **Propagation delay** — changes can take up to ~30 minutes; restarting the IDE session helps
- C) The developer is an owner
- D) The file was deleted

**Answer: B.** Exclusion changes aren't always instant; allow for propagation (~30 min) and refresh
the editor session.

**Q64.** Who is allowed to **edit** content-exclusion patterns?
- A) Any repository contributor
- B) **Repository admin, organization owner, or enterprise owner**
- C) Users with the Triage role
- D) The Copilot support bot

**Answer: B.** Only admin/owner roles configure exclusions. ⚠️ The **Maintain** role can **view**
settings but **not edit** them.

**Q65.** The **Maintain** role's relationship to content exclusions is:
- A) It can edit patterns
- B) **View-only** — it cannot change exclusion settings
- C) It can delete the enterprise
- D) It manages billing

**Answer: B.** Maintain = read/view; editing exclusions requires admin/owner.

**Q66.** Which setting provides the **strongest IP protection** against reproducing public code?
- A) Enable all languages
- B) Set **"Suggestions matching public code" to Blocked**
- C) Disable Chat
- D) Increase the font size

**Answer: B.** Blocking (not merely warning) prevents suggestions that match public code — the
strongest safeguard, tied to IP indemnity on Business+.

**Q67.** What is the difference between **duplication detection (warn)** and **block public code**?
- A) They're identical
- B) **Warn alerts** you to a public-code match; **Block prevents** the matching suggestion from
  being shown
- C) Warn deletes the repo; block encrypts it
- D) Block is weaker than warn

**Answer: B.** ⚠️ Warn = notification; Block = prevention. Blocking is the stronger control.

**Q68.** A security team excluded `/secrets`, yet **Agent Mode in Chat** still reads files there.
The correct fix is:
- A) Add more exclusion patterns
- B) **Use agent instructions/boundaries, secret scanning, and access control (RBAC)** — exclusion
  doesn't cover Agent Mode
- C) Delete the org
- D) Nothing — it's impossible

**Answer: B.** Since exclusions don't apply to Agent Mode, protect secrets with agent guardrails,
scanning, and least-privilege access — not exclusion alone.

**Q69.** Who **owns** the code Copilot suggests, and what's the key limitation to communicate?
- A) GitHub owns it; no limitations
- B) The **user/organization owns and is responsible** for accepted output; outputs may be
  imperfect and must be validated (correctness, security, licensing)
- C) The LLM owns it
- D) It's public domain automatically

**Answer: B.** Ownership and accountability sit with the user; outputs carry limitations that
require validation — this ties privacy/safeguards back to Responsible AI.

**Q70.** When **enterprise** and **organization** exclusion rules interact:
- A) **Enterprise-level rules can take precedence** over org rules
- B) Repository rules are always ignored
- C) There's no relationship
- D) Individual users decide everything

**Answer: A.** Policy hierarchy flows enterprise → org → repo; higher-scope enterprise rules can
override, so troubleshoot with **scope** in mind.

---

## Quick self-scoring

| Topic | Questions | Your score |
|-------|-----------|------------|
| 1 — Responsible AI | Q1–Q10 | ___ / 10 |
| 2 — Features: IDE/Chat/Modes | Q11–Q20 | ___ / 10 |
| 3 — Features: CLI/Org admin | Q21–Q30 | ___ / 10 |
| 4 — Data & architecture | Q31–Q40 | ___ / 10 |
| 5 — Prompt engineering | Q41–Q50 | ___ / 10 |
| 6 — Productivity | Q51–Q60 | ___ / 10 |
| 7 — Privacy & safeguards | Q61–Q70 | ___ / 10 |

**Readiness bar:** ≥ 8/10 on every topic and ≥ 85% overall on the practice exams in
[GH300-Study-Guide.md](GH300-Study-Guide.md) before scheduling.

## Highest-yield traps to memorize (⚠️)

1. **Content exclusion does NOT cover CLI, coding agent, or Agent Mode in Chat.**
2. **Copilot never auto-merges/approves PRs** — it reviews/summarizes; humans merge.
3. **Business+** for content exclusion, IP indemnity, SAML SSO, org policy, audit logs; pick the
   **lowest tier meeting all requirements**.
4. **Enterprise-only:** fine-tuned models, Knowledge Bases, advanced PR summaries, Bing-grounded
   web search.
5. **Data differs by interface:** Business+ IDE = zero retention; CLI/agent = ~28-day abuse
   monitoring; telemetry retained longer (~2 years).
6. **Warn ≠ Block** for public-code matching; **Maintain = view-only** on exclusions.
7. **Always validate AI output** before production — the answer to most Responsible-AI scenarios.
8. Poor suggestion? Fix **context first, then specificity**. Few-shot only for unusual patterns.

**Sources:**
[GH-300 study guide (Microsoft Learn)](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/gh-300) ·
[GitHub Copilot certification page](https://learn.microsoft.com/en-us/credentials/certifications/github-copilot/) ·
[GitHub Copilot plans](https://docs.github.com/copilot/about-github-copilot/plans-for-github-copilot) ·
[Content exclusion docs](https://docs.github.com/copilot/managing-copilot/configuring-and-auditing-content-exclusion) ·
[GitHub Trust Center](https://github.com/trust-center)
