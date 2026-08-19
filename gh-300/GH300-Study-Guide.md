# GH300 Certification Study Guide (Complete)

> **Exam:** Microsoft **GH-300: GitHub Copilot** (January 2026 skills outline)  
> **Audience:** Beginner → competent developer/admin who can pass on first attempt with disciplined study  
> **How to use this guide:** Read Section 1, study one domain per day (Section 2), drill daily (Section 3), take one practice exam per week (Section 4), finish with Section 5–6.

---

## Assumptions / Fill-in Blanks

Most GH-300 details are published. Fill these if your booking differs:

| Item | Official / Best Evidence | Your Notes |
|------|--------------------------|------------|
| Exam code | **GH-300** (GitHub Copilot) | |
| Question count | **~65 graded** + ~10 ungraded (community reports) | |
| Time limit | **100 minutes** | |
| Passing score | **700 / 1000** (scaled) | |
| Question types | Multiple choice, multiple response, scenario-based | |
| Sections | **2 sections** — cannot return to Section 1 after advancing | |
| Cost | ~$99 USD (varies by region) | |
| Validity | 2 years; free renewal assessment on Learn | |
| Prerequisites | GitHub fundamentals + 1+ programming language | |
| Hands-on tools | VS Code / Visual Studio / JetBrains + github.com | |

**Study sources (official):**
- [GH-300 study guide (Microsoft Learn)](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/gh-300)
- [GitHub Copilot certification page](https://learn.microsoft.com/en-us/credentials/certifications/github-copilot/)
- Learning paths: *GitHub Copilot Fundamentals Part 1 & 2*
- [How GitHub Copilot works](https://docs.github.com/en/copilot/concepts/completions)
- [Content exclusion](https://docs.github.com/en/copilot/managing-copilot/managing-github-copilot-in-your-organization/configuring-content-exclusions-for-github-copilot)
- [Responsible use of GitHub Copilot](https://docs.github.com/en/copilot/responsible-use-of-github-copilot)

---

## 1. Exam Overview

### 1.1 Format, Time, and Scoring

| Element | What to expect |
|---------|----------------|
| Delivery | Online proctored (Pearson VUE) or test center |
| Duration | 100 minutes for ~65 scored questions |
| Passing | **700+** on a 1000-point scale (you do not need 70% of questions correct — scoring is scaled) |
| Style | Scenario-first: “A team needs X — what should they do?” |
| Trap types | Plan-tier boundaries, governance scope, “almost right” feature names |
| Section rule | **Review all Section 1 answers before submitting** — no going back |

**Question types**
- **Single-answer multiple choice** — one best governance or feature answer
- **Multiple response** — select all that apply; partial credit may not exist
- **Scenario caselets** — 2–3 sentences of context, then 1–2 questions

### 1.2 Domains and Weighting (January 2026)

| # | Domain | Weight |
|---|--------|--------|
| 1 | Use GitHub Copilot responsibly | 15–20% |
| 2 | Use GitHub Copilot features | 25–30% |
| 3 | GitHub Copilot features (overlap/detail) | 25–30% |
| 4 | Understand GitHub Copilot data and architecture | 10–15% |
| 5 | Apply prompt engineering and context crafting | 10–15% |
| 6 | Improve developer productivity with GitHub Copilot | 10–15% |
| 7 | Configure privacy, content exclusions, and safeguards | 10–15% |

> **Note:** Microsoft lists two “Use GitHub Copilot features” groups at 25–30% each. Treat **features + plans + admin** as one combined ~50% study block.

### 1.3 What “Passing” Requires — Skills + Knowledge Checklist

**You must be able to:**

- [ ] Explain responsible AI risks and **validate every AI output** before shipping
- [ ] Enable and use Copilot in IDE, Chat, CLI, Agent Mode, Edit Mode, Plan Mode
- [ ] Distinguish **Free / Pro / Pro+ / Business / Enterprise** features
- [ ] Describe the **proxy pipeline** (pre-process → LLM → post-process)
- [ ] Craft **specific, contextual prompts** (zero-shot vs few-shot)
- [ ] Use Copilot for tests, docs, refactoring, security review
- [ ] Configure **content exclusions**, duplication detection, and editor safeguards
- [ ] Know **what content exclusion does NOT cover** (CLI, Agent Mode, coding agent)
- [ ] Manage org policies, audit logs, Code Review policies, REST subscription APIs (concept level)

**Minimum hands-on bar (do all before exam day):**
1. Install Copilot in VS Code; use inline, Chat, and at least one Agent/Edit session
2. Install and run **Copilot CLI** interactively
3. Read org settings for content exclusion (even in a trial org or docs walkthrough)
4. Complete Microsoft Learn practice assessment for GH-300

---

## 2. Study Guide by Topic

---

### Domain 1: Use GitHub Copilot Responsibly (15–20%)

#### Must-know concepts

| Concept | Definition | Why it matters on the exam |
|---------|------------|----------------------------|
| Responsible AI | Use AI transparently, fairly, securely, with human accountability | Scenarios ask which principle applies |
| Validation | Human review of correctness, security, license, and fit | “Ship without review” is always wrong |
| Limitations | Hallucinations, stale training, context gaps, bias | Explains bad suggestions |
| Transparency | Users understand *how* suggestions are produced/filtered | Not the same as “trust the brand” |
| Fairness vs inclusiveness | Fair = equitable outcomes; inclusive = broad representation | Both appear as distractors |
| Mitigation | Testing, exclusions, policies, oversight for Agent Mode | Links to governance domains |

#### Typical scenarios

- Junior dev pastes Copilot SQL directly into production → **validate, test, security review**
- Copilot suggests code similar to public repo → discuss **duplication detection / public code matching**
- Agent Mode runs autonomously → require **boundaries, review, audit**

#### Common pitfalls

| Pitfall | Avoid by |
|---------|----------|
| “Copilot is always right” | Default answer: validate first |
| Ignoring license/IP risk | Tie to public code matching and org policies |
| Treating ethics as isolated | Every governance question has a responsible-AI angle |

#### Cheat sheet

- **Never** skip human validation for production code
- Responsible AI = accountability + transparency + safety + fairness
- Agentic tools need **more** oversight, not less
- Document **why** AI was used when org policy requires it

#### Quick practice (Domain 1)

1. **A developer accepts a Copilot suggestion without reading it. Best response?**  
   **A)** Encourage speed — Copilot is trained on quality code  
   **B)** Require code review and testing before merge  
   **C)** Disable Copilot for that user  
   **D)** Switch to a different LLM  
   **Answer: B** — Validation is mandatory; disabling is disproportionate.

2. **Which is a limitation of generative AI in coding?**  
   **A)** Cannot syntax-highlight  
   **B)** May hallucinate APIs that do not exist  
   **C)** Only works in Python  
   **D)** Requires internet only on Enterprise  
   **Answer: B** — Hallucination is a core exam theme.

3. **Transparency in responsible AI means:**  
   **A)** Hiding model version from users  
   **B)** Explaining how suggestions are generated and filtered  
   **C)** Using the most popular IDE  
   **D)** Avoiding documentation  
   **Answer: B**

4. **Agent Mode completes a multi-file change. What should the team do?**  
   **A)** Auto-merge because the agent ran tests  
   **B)** Review diff, run CI, validate security  
   **C)** Delete the branch  
   **D)** Disable MCP  
   **Answer: B** — Autonomy ≠ approval to ship.

5. **Mitigation for biased training data in suggestions?**  
   **A)** Ignore unless users complain  
   **B)** Validate outputs, use policies, diverse review  
   **C)** Use longer prompts only  
   **D)** Disable Chat only  
   **Answer: B**

---

### Domain 2 & 3: Use GitHub Copilot Features (combined ~50%)

#### Must-know concepts

| Concept | Definition | Why it matters |
|---------|------------|----------------|
| Inline completion | Ghost text as you type in IDE | Trigger: type; accept: Tab |
| Copilot Chat | Conversational assistance in IDE/github.com | Commands, context, history |
| Agent Mode | Autonomous multi-step coding (edit, run, retry) | Governance + boundaries |
| Edit Mode | Targeted edits across files from Chat | Less autonomous than Agent |
| Plan Mode | Plan before executing changes | Exam: structure work first |
| Copilot CLI | Terminal agent for scripts, files, sessions | Separate install; different data rules |
| MCP | Model Context Protocol — connect external tools/data | Standardized agent integrations |
| Sub-Agents | Delegate subtasks for context efficiency | Agent Sessions management |
| Copilot Spaces | Shared context/knowledge for teams | Enterprise collaboration |
| Spark | GitHub’s app-building experience with Copilot | Feature availability by plan |
| PR summaries | AI summary of pull request changes | Enterprise feature (verify current docs) |
| Code Review | Automated review on PRs | Org policies control availability |

#### Plan tiers (memorize)

| Feature / control | Free | Pro | Pro+ | Business | Enterprise |
|-------------------|------|-----|------|----------|------------|
| Basic inline + Chat | ✓ | ✓ | ✓ | ✓ | ✓ |
| Content exclusion | — | — | — | ✓ | ✓ |
| IP indemnity | — | — | — | ✓ | ✓ |
| Org-wide policy management | — | — | — | ✓ | ✓ |
| SAML SSO enforcement | — | — | — | ✓ | ✓ |
| Fine-tuned models / Knowledge Bases | — | — | — | — | ✓ |
| PR summaries (advanced) | — | — | — | — | ✓ |
| Web search (Bing-grounded) | — | — | — | — | ✓ |

> **Exam pattern:** Scenario states a requirement → pick the **lowest tier that satisfies all requirements**. Distractor is usually one tier too low.

#### Typical scenarios

- Company needs to block Copilot from `/.env` files org-wide → **Business or Enterprise** + content exclusion
- Developer wants autonomous fix-build-test loop → **Agent Mode** with explicit constraints
- Admin must audit who changed Copilot policies → **audit log** (Business/Enterprise)
- Team needs consistent review standards → **instructions files** + Code Review policies

#### Common pitfalls

| Pitfall | Truth |
|---------|-------|
| Content exclusion blocks Agent Mode | **False** — exclusion does not apply to CLI, coding agent, or Agent Mode in Chat |
| All plans have IP indemnity | **Business+ only** |
| Copilot merges PRs automatically | **No** — summarizes/reviews; human merges |
| MCP is Copilot-only | Open standard (Anthropic-origin); Copilot uses it |

#### Cheat sheet

- **Largest domain** — study plans + interfaces together
- Agent Mode: set **negative constraints** (“plan only, no file writes”)
- CLI: `copilot` interactive sessions; file/script generation
- Org admin: Code Review policies, feature flags per IDE, REST API for seats
- Maintain role: **view** exclusions, not edit

#### Quick practice (Domains 2–3)

6. **Which plan is required for organization-wide content exclusion?**  
   **A)** Pro  
   **B)** Business  
   **C)** Free  
   **D)** Pro+  
   **Answer: B** (or Enterprise)

7. **Agent Mode is best for:**  
   **A)** Renaming one variable  
   **B)** Multi-step implement-test-fix with tool use  
   **C)** Disabling suggestions  
   **D)** Billing reports only  
   **Answer: B**

8. **MCP enables Copilot to:**  
   **A)** Replace Git entirely  
   **B)** Connect to external tools via a standard protocol  
   **C)** Bypass all filters  
   **D)** Train on private repos by default  
   **Answer: B**

9. **Who can edit content exclusion patterns?**  
   **A)** Any repo contributor  
   **B)** Repo admin, org owner, enterprise owner  
   **C)** Users with Triage role only  
   **D)** Copilot support bot  
   **Answer: B**

10. **PR summary feature is typically available on:**  
    **A)** Free  
    **B)** Pro only  
    **C)** Enterprise  
    **D)** All tiers equally  
    **Answer: C** (confirm in current docs)

---

### Domain 4: Understand GitHub Copilot Data and Architecture (10–15%)

#### Must-know concepts

| Stage | What happens |
|-------|----------------|
| Context gathering | IDE sends surrounding code, open files, comments (per settings) |
| Proxy (GitHub/Azure) | Pre-processing: toxicity, relevance, policy checks |
| LLM | Generates completion/chat response |
| Post-processing | Toxicity filter, quality checks, security scan, **public code matching**, truncate/discard |
| Delivery | Suggestion shown in IDE or Chat |

**Data retention (high-yield)**

| Context | Retention pattern (study current docs) |
|---------|----------------------------------------|
| Business/Enterprise IDE | **Zero retention** of prompts/suggestions after processing |
| CLI / Agent workflows | **~28 days** for abuse monitoring (not model training) |
| Individual plans | May contribute to training unless user opts out |
| Telemetry | Longer retention (e.g., ~2 years) for product analytics |

#### Typical scenarios

- “Why no suggestion returned?” → post-processing blocked, exclusion, filter, or empty context
- “Where does prompt go?” → **GitHub proxy**, not direct to random endpoint
- “Is my code used to train?” → depends on **plan + settings + interface**

#### Common pitfalls

- Assuming all interfaces have identical retention (CLI ≠ inline IDE)
- Thinking proxy is optional — it’s central to filtering and enterprise controls

#### Cheat sheet

```
IDE → Proxy (pre) → LLM → Proxy (post) → IDE
         ↑ toxicity, policy    ↑ security, public code match, quality
```

#### Quick practice (Domain 4)

11. **Prompts from Business plan IDE sessions are retained for model training?**  
    **A)** Yes, always  
    **B)** No — zero retention after processing (per enterprise policy)  
    **C)** 28 days  
    **D)** Forever  
    **Answer: B**

12. **Public code matching in post-processing can:**  
    **A)** Speed up Git push  
    **B)** Block or warn on verbatim public code matches  
    **C)** Delete the repository  
    **D)** Disable MCP  
    **Answer: B**

13. **28-day retention applies especially to:**  
    **A)** Static README viewing  
    **B)** CLI and Agent Mode workflows  
    **C)** Git clone only  
    **D)** GitHub Issues  
    **Answer: B**

14. **Why use a proxy instead of direct IDE→LLM?**  
    **A)** Marketing  
    **B)** Centralized filtering, policy, security processing  
    **C)** Slower UX only  
    **D)** To store all code permanently  
    **Answer: B**

15. **LLM limitation tested on exam:**  
    **A)** Infinite context  
    **B)** May not know your private undeclared context  
    **C)** Always license-aware without configuration  
    **D)** Cannot generate tests  
    **Answer: B**

---

### Domain 5: Apply Prompt Engineering and Context Crafting (10–15%)

#### Must-know concepts

| Technique | When to use |
|-----------|-------------|
| Zero-shot | Straightforward task; clear intent |
| Few-shot | Pattern is unusual; include 1–3 examples in prompt |
| Context injection | Open files, selections, `@` references, instructions files |
| Single-task prompt | One objective per message |
| Chat history | Continues thread; can dilute focus if too long |

**Four Ss (exam-friendly framework)**

1. **Single** — one task  
2. **Specific** — language, framework, constraints, format  
3. **Short** — no rambling (but include necessary detail)  
4. **Surrounded** — provide surrounding code/context

#### Typical scenarios

- Vague prompt → poor suggestion → fix: **add specificity + context**
- Need consistent API style across files → **few-shot** examples
- Wrong library version used → prompt missing **version/framework context**

#### Common pitfalls

| Bad prompt | Fix |
|------------|-----|
| “Write tests” | “Write pytest unit tests for `parse_date()` covering null, ISO, invalid” |
| Multi-task wall of text | Split into steps |
| No file context | Select code or `@file` reference |

#### Cheat sheet

- Poor output? First check **context**, then **specificity**
- Few-shot > zero-shot when pattern is non-obvious
- Instructions files = persistent project conventions for Copilot

#### Quick practice (Domain 5)

16. **Best approach to enforce naming conventions:**  
    **A)** Zero-shot “write code”  
    **B)** Few-shot with examples + instructions file  
    **C)** Empty prompt  
    **D)** Disable inline  
    **Answer: B**

17. **Copilot suggests wrong framework because:**  
    **A)** User banned Java  
    **B)** Context lacked framework/version info  
    **C)** Proxy offline  
    **D)** Tab key broken  
    **Answer: B**

18. **Zero-shot is appropriate when:**  
    **A)** Task is standard and well-defined  
    **B)** Pattern is rare and stylistic  
    **C)** You need 5 examples always  
    **D)** Never appropriate  
    **Answer: A**

19. **“Single” in prompt crafting means:**  
    **A)** One programming language per repo  
    **B)** One clear task per prompt  
    **C)** One character per line  
    **D)** One user per org  
    **Answer: B**

20. **Chat history primarily:**  
    **A)** Replaces git history  
    **B)** Provides conversational context within the session  
    **C)** Deletes exclusions  
    **D)** Enables IP indemnity  
    **Answer: B**

---

### Domain 6: Improve Developer Productivity (10–15%)

#### Must-know concepts

| Use case | Copilot approach |
|----------|------------------|
| Unit tests | Prompt with function + edge cases + framework |
| Integration tests | Specify dependencies, mocks, external systems |
| Documentation | Docstrings, README sections, API docs from signatures |
| Refactoring | Select code; ask for rename, extract, pattern apply |
| Legacy modernization | Explain target stack; incremental migration steps |
| Sample data | Generate fixtures with constraints |
| Security | Ask for threat review, input validation, OWASP checks |
| Performance | Ask for bottleneck analysis and optimizations |

#### Typical scenarios

- Increase test coverage → prompt for **edge cases and assertions**, not only happy path
- Onboard to repo → Copilot explains selected code (**learning**, less context switching)
- Security audit → suggest validation, parameterized queries, secret handling

#### Common pitfalls

- Trusting generated tests without running them
- Asking Copilot to **merge** or **approve** PRs (out of scope)
- Integration test prompt missing mock strategy

#### Cheat sheet

- Tests: name framework, name edge cases, ask for assertions
- Refactor: small scoped selection + desired pattern
- Security: combine Copilot suggestions with SAST/review

#### Quick practice (Domain 6)

21. **Best prompt for unit tests:**  
    **A)** “test this”  
    **B)** “Generate xUnit tests for `CalculateTax` with cases: zero income, negative, bracket boundary”  
    **C)** “delete tests”  
    **D)** “merge PR”  
    **Answer: B**

22. **Copilot helps reduce context switching by:**  
    **A)** Explaining unfamiliar code in-editor  
    **B)** Replacing GitHub Actions  
    **C)** Removing need for CI  
    **D)** Auto-deploying prod  
    **Answer: A**

23. **Integration test prompt must include:**  
    **A)** Only function name  
    **B)** External deps, mocks, expected IO  
    **C)** User’s password  
    **D)** License key  
    **Answer: B**

24. **For security improvements, you should:**  
    **A)** Ship Copilot output directly  
    **B)** Review suggestions + run security tooling  
    **C)** Disable all filters  
    **D)** Publish secrets for context  
    **Answer: B**

25. **Legacy modernization strategy:**  
    **A)** One-shot full rewrite without review  
    **B)** Incremental refactors with validation  
    **C)** Delete legacy code  
    **D)** Ignore tests  
    **Answer: B**

---

### Domain 7: Configure Privacy, Content Exclusions, and Safeguards (10–15%)

#### Must-know concepts

| Control | Purpose |
|---------|---------|
| Content exclusion | Block Copilot access to paths (e.g., `**/*.env`, `/secrets/**`) |
| Duplication detection | Warn when suggestion matches public code |
| Block public code | Stronger IP protection; ties to indemnity |
| Editor settings | Per-user suggestion behavior, extensions |
| Propagation delay | Exclusion changes may take **~30 minutes** in open IDEs |

**Content exclusion effects (when it applies)**

- Inline suggestions **disabled** in excluded files  
- Excluded content **not used as context** elsewhere  
- Chat **refuses** to analyze excluded content  

**Does NOT apply to:** Copilot CLI, coding agent, Agent Mode in Chat

#### Typical scenarios

- Secrets folder still read by Agent Mode → exclusion **won’t help**; use agent boundaries, secrets scanning, access control
- Need IP indemnity → **Business/Enterprise** + block public code matching
- Admin changed exclusions; dev still sees suggestions → wait **propagation**, restart IDE session

#### Common pitfalls

| Wrong | Right |
|-------|-------|
| “Exclude path” for CLI leak | CLI needs different controls |
| Warning = blocked | Warning alerts; blocking prevents match |
| Any member edits exclusions | Admin/owner only |

#### Cheat sheet

- Exclusion = IDE/inline/chat context path — **not agentic CLI/Agent Mode**
- IP indemnity: Business+ and **block suggestions matching public code**
- Troubleshoot: policy scope, role, propagation time, correct interface

#### Quick practice (Domain 7)

26. **Content exclusion applies to Copilot CLI?**  
    **A)** Yes  
    **B)** No  
    **Answer: B** — High-frequency exam trap.

27. **After updating exclusions, suggestions may persist until:**  
    **A)** Instant always  
    **B)** Up to ~30 minutes / IDE refresh  
    **C)** Next year  
    **D)** Never changes  
    **Answer: B**

28. **Setting for strongest public-code IP protection:**  
    **A)** Enable all languages  
    **B)** Suggestions matching public code: **blocked**  
    **C)** Disable Chat  
    **D)** Increase font size  
    **Answer: B**

29. **Maintain role on content exclusions can:**  
    **A)** Edit patterns  
    **B)** View settings only  
    **C)** Delete enterprise  
    **D)** Change billing  
    **Answer: B**

30. **Enterprise vs org exclusion rules:**  
    **A)** Enterprise rules can take precedence  
    **B)** Repo rules always ignored  
    **C)** No relationship  
    **D)** Only users decide  
    **Answer: A**

---

## 3. Skill-Building Drills

### 3.1 Flashcards (90 Q/A)

Study: cover the answer column, score yourself daily, repeat misses.

| # | Question | Answer |
|---|----------|--------|
| 1 | GH-300 exam name? | GitHub Copilot |
| 2 | Passing score? | 700/1000 |
| 3 | Time limit? | 100 minutes |
| 4 | Approx. graded questions? | ~65 |
| 5 | Can you return to Section 1? | No |
| 6 | Largest exam domains? | Copilot features (×2 groups) |
| 7 | First step with AI code? | Validate / review |
| 8 | Hallucination? | Confident but wrong output |
| 9 | Transparency means? | Explain how AI works/filters |
| 10 | Agent Mode autonomy? | Multi-step; needs oversight |
| 11 | Accept inline suggestion key? | Tab (VS Code default) |
| 12 | Copilot Chat purpose? | Conversational coding help |
| 13 | Edit Mode? | Targeted multi-file edits |
| 14 | Plan Mode? | Plan before executing |
| 15 | Copilot CLI? | Terminal-based agent |
| 16 | MCP stands for? | Model Context Protocol |
| 17 | MCP purpose? | Standard external tool connections |
| 18 | Sub-Agents? | Delegated tasks in agent sessions |
| 19 | Copilot Spaces? | Shared team context |
| 20 | Five Copilot tiers? | Free, Pro, Pro+, Business, Enterprise |
| 21 | Content exclusion minimum plan? | Business |
| 22 | IP indemnity minimum plan? | Business |
| 23 | SAML SSO enforcement? | Business+ |
| 24 | Fine-tuned models / KB? | Enterprise |
| 25 | Bing web search in Copilot? | Enterprise |
| 26 | PR summaries (advanced)? | Enterprise |
| 27 | Who edits exclusions? | Repo admin, org/enterprise owner |
| 28 | Maintain role on exclusions? | View only |
| 29 | Exclusion propagation time? | Up to ~30 minutes |
| 30 | Exclusion applies to CLI? | No |
| 31 | Exclusion applies to Agent Mode Chat? | No |
| 32 | Exclusion blocks inline in file? | Yes |
| 33 | Exclusion blocks context from file? | Yes |
| 34 | Chat on excluded file? | Refuses |
| 35 | Proxy sits where? | Between client and LLM |
| 36 | Pre-processing examples? | Toxicity, relevance |
| 37 | Post-processing examples? | Security scan, public code match |
| 38 | Business IDE prompt retention? | Zero after processing |
| 39 | CLI retention (~)? | 28 days abuse monitoring |
| 40 | Individual plan training opt-out? | Settings — may keep features |
| 41 | Telemetry retention (~)? | ~2 years product analytics |
| 42 | Zero-shot? | Prompt without examples |
| 43 | Few-shot? | Prompt with examples |
| 44 | Four Ss — Single? | One task per prompt |
| 45 | Four Ss — Specific? | Clear constraints/stack |
| 46 | Four Ss — Short? | Concise but complete |
| 47 | Four Ss — Surrounded? | Provide code context |
| 48 | Instructions files? | Persistent project guidance |
| 49 | Poor suggestion first fix? | Add context/specificity |
| 50 | Unit test prompt should include? | Framework + edge cases |
| 51 | Integration tests need? | Mocks, deps, IO |
| 52 | Copilot auto-merge PRs? | No |
| 53 | Code Review on PRs? | Policy-configurable feature |
| 54 | Audit logs for Copilot admin? | Business/Enterprise |
| 55 | Duplication detection? | Warn on public code match |
| 56 | Block public code? | Stronger than warn |
| 57 | IP protection setting keyword? | Suggestions matching public code: blocked |
| 58 | Org Code Review policies? | Admin configures |
| 59 | REST API for Copilot? | Subscription/seat management |
| 60 | Enable Copilot in IDE? | Sign in + extension + policy |
| 61 | JetBrains supported? | Yes |
| 62 | Visual Studio supported? | Yes |
| 63 | VS Code supported? | Yes |
| 64 | github.com Copilot? | Yes (Chat/features vary) |
| 65 | Preview features on exam? | Possible if commonly used |
| 66 | GA features? | Majority of exam |
| 67 | Renewal method? | Free Learn assessment |
| 68 | Cert validity? | 1 year (Microsoft associate pattern — verify) |
| 69 | Responsible AI: accountability? | Human responsible for output |
| 70 | Bias mitigation? | Review + policy + diverse testing |
| 71 | Agent negative constraint example? | “Plan only; no writes” |
| 72 | Prompt file reuse? | Consistent team responses |
| 73 | Sample data generation? | Productivity use case |
| 74 | Legacy modernization? | Incremental with validation |
| 75 | Refactoring pattern? | Select code + instruct pattern |
| 76 | Security prompt example? | Check OWASP, injection |
| 77 | Performance prompt? | Profile hotspots, suggest fix |
| 78 | Edge case testing prompt? | Enumerate boundaries |
| 79 | Assertions in tests? | Ask explicitly in prompt |
| 80 | Context window limit? | LLM limitation |
| 81 | Private undeclared code? | Not magic — must be in context |
| 82 | Enterprise org policies? | Feature availability control |
| 83 | Copilot Spark? | App building with Copilot |
| 84 | SAM enforcement? | Business+ |
| 85 | Multiple-response strategy? | Select all fully correct |
| 86 | Scenario tie-breaker? | Governance/plan tier logic |
| 87 | Section 1 strategy? | Flag uncertain; review all |
| 88 | Public code match discard? | Post-processing can drop |
| 89 | Secrets in prompts? | Avoid; use exclusions |
| 90 | Exam date after Jan 2026? | Study Agent Mode + MCP |

---

### 3.2 Worked Examples (12)

#### Example 1 — Plan tier selection

**Scenario:** Startup needs SAML SSO, org-wide Copilot policies, and content exclusion for `**/credentials/**`.  
**Work:** Need Business minimum (Enterprise if they also need fine-tuned models / PR summaries).  
**Answer:** **GitHub Copilot Business** (or Enterprise if extra Enterprise-only features listed).

#### Example 2 — Content exclusion trap

**Scenario:** Security team excluded `/secrets`. Agent Mode in Chat still reads files there.  
**Work:** Exclusion does not apply to Agent Mode.  
**Answer:** Use agent instructions forbidding that path, secrets scanning, RBAC — not exclusion alone.

#### Example 3 — Proxy pipeline debug

**Scenario:** Inline suggestion never appears; Chat works. File is not excluded.  
**Work:** Check post-processing (public code block), extension conflict, language support, empty context.  
**Answer:** Likely **blocked post-processing** or **editor/extension** issue — not “LLM down” first.

#### Example 4 — Prompt fix

**Bad:** “Add error handling.”  
**Good:** “In `UserService.create()`, add try/catch for `DbException`; log with correlation ID; return `Result.Fail` — follow existing `OrderService` pattern.”  
**Why:** Specific, surrounded, single task.

#### Example 5 — Zero vs few-shot

**Task:** Generate API clients matching odd internal JSON envelope.  
**Answer:** **Few-shot** — provide two sample requests/responses.

#### Example 6 — Data retention

**Question:** Business dev uses IDE inline only. Are prompts stored for training?  
**Answer:** **No** — zero retention after processing (enterprise policy).

#### Example 7 — CLI retention

**Question:** Same org uses Copilot CLI for deploy scripts. Retention?  
**Answer:** **~28 days** for abuse monitoring — not the same as IDE zero retention.

#### Example 8 — IP indemnity

**Requirement:** Microsoft/GitHub IP indemnity for Copilot suggestions.  
**Answer:** **Business or Enterprise** + configure **block public code matching**.

#### Example 9 — Test generation

**Prompt:** “Using Jest, generate tests for `validateEmail`: empty string, missing @, valid, unicode local-part. Include `expect` assertions.”  
**Outcome:** Productivity domain best practice.

#### Example 10 — Responsible AI

**Scenario:** Copilot suggests GPL-licensed snippet match.  
**Answer:** Do not ship blindly; enable **duplication detection**; consider **block**; human review.

#### Example 11 — MCP integration

**Scenario:** Copilot must query internal ticket system during agent task.  
**Answer:** Configure **MCP server** for tickets; define agent scope.

#### Example 12 — Section 1 exam strategy

**Scenario:** 40 minutes left in Section 1, 8 flagged questions.  
**Answer:** Answer all unflagged first, revisit flags, **never submit Section 1** until all reviewed.

---

### 3.3 “If You See X, Think Y” Heuristics

| If you see… | Think… |
|-------------|--------|
| SAML SSO + org policies | Business or Enterprise |
| Content exclusion | Business+; admins only |
| Agent Mode + secrets path | Exclusion **won’t work** |
| IP indemnity | Business+ + block public code |
| “Validate before production” | Always yes |
| Vague prompt → bad code | Add context + specificity |
| Rare coding pattern | Few-shot prompting |
| “Why no suggestion?” | Post-process, exclusion, context |
| IDE Business user data | Zero retention processing |
| CLI / Agent session data | ~28-day monitoring retention |
| PR auto-merge | Wrong — Copilot advises, humans merge |
| Maintain role | View, not edit |
| Enterprise vs org policy conflict | Enterprise precedence |
| MCP in question | External tools via standard protocol |
| Multiple answers “work” | Pick Microsoft governance doc answer |
| Section advance button | Final review Section 1 first |
| Audit who changed Copilot settings | Audit log Business+ |
| Duplication **warning** vs **block** | Warning alerts; block prevents |
| Instructions file | Team coding standards for Copilot |
| Sub-Agents | Context optimization in Agent Mode |

---

## 4. Practice Exams

**Instructions:** Timed 90 minutes each. Mark multiple-response accordingly. Review diagnostics after each exam.

---

### Practice Exam 1 (40 Questions)

**1.** Primary certification focus of GH-300?  
A) GitHub Actions B) **GitHub Copilot** C) GitHub Admin D) Advanced Security  
**2.** Passing score?  
A) 500 B) 600 C) **700** D) 800  
**3.** Responsible AI: who owns output?  
A) Microsoft B) LLM vendor C) **The human/developer** D) No one  
**4.** First action with generated prod code?  
A) Deploy B) **Review and test** C) Tweet D) Delete repo  
**5.** Hallucination is:  
A) Hardware failure B) **Plausible false output** C) VPN error D) Merge conflict  
**6.** Agent Mode best for:  
A) Typing one line B) **Multi-step autonomous workflow** C) Billing D) SSH keys  
**7.** MCP purpose:  
A) Git replacement B) **External tool integration standard** C) Markdown D) DNS  
**8.** Content exclusion available on:  
A) Free B) Pro C) **Business** D) Student pack only  
**9.** Exclusion applies to CLI?  
A) Yes B) **No**  
**10.** Minimum plan for org SAML SSO (typical):  
A) Free B) **Business** C) Personal C) None  
**11.** IP indemnity requires (typical):  
A) Free B) **Business+** C) Any fork D) Wiki only  
**12.** Proxy pre-processing includes:  
A) Git fetch B) **Toxicity/relevance checks** C) npm install D) Docker build  
**13.** Post-processing can:  
A) **Block public code matches** B) Increase salary C) Merge PR D) Rotate keys automatically  
**14.** Business IDE prompt storage for training:  
A) Forever B) **Not retained after processing** C) 28 days D) 1 hour  
**15.** CLI sessions retention (~):  
A) Zero always B) **28 days** C) 10 years D) 1 minute  
**16.** Zero-shot means:  
A) No examples in prompt B) No computer C) No Git D) No IDE  
**17.** Few-shot helps when:  
A) Pattern is unusual B) Keyboard broken C) Offline D) Never  
**18.** “Single” prompt principle:  
A) One task B) One employee C) One disk D) One language globally  
**19.** Poor suggestion fix first:  
A) Reinstall OS B) **Improve context/specificity** C) Delete repo D) Change username  
**20.** Instructions files provide:  
A) **Persistent project guidance** B) VPN C) Licenses D) CPU  
**21.** Unit test prompt should name:  
A) **Framework and edge cases** B) CEO C) Office D) Color theme  
**22.** Copilot merges PRs automatically?  
A) Yes B) **No**  
**23.** Generate integration tests requires:  
A) Only “test it” B) **Deps, mocks, expected IO** C) Password in prompt D) Nothing  
**24.** Refactor prompt best practice:  
A) Select code + desired pattern B) Empty chat C) Random file D) Disable Copilot  
**25.** Security suggestions should be:  
A) Shipped blindly B) **Reviewed + scanned** C) Ignored D) Published  
**26.** Duplication detection:  
A) **Warns on public matches** B) Deletes git C) Blocks all AI D) Removes SSO  
**27.** Strongest IP setting keyword:  
A) Dark mode B) **Block public code suggestions** C) Font 12 D) Emoji  
**28.** Who edits exclusions?  
A) Anyone B) **Repo admin / org owner** C) Anonymous D) Bot only  
**29.** Maintain role:  
A) Edit exclusions B) **View exclusions** C) Delete org D) Bill  
**30.** Propagation delay after exclusion change (~):  
A) 0s B) **30 min** C) 30 days D) Never  
**31.** Enterprise exclusion vs org:  
A) **Enterprise can take precedence** B) Org always loses C) Random D) User vote  
**32.** Audit logs for Copilot admin actions:  
A) Free only B) **Business+** C) Never D) Public web  
**33.** Copilot Code Review policies set by:  
A) Intern B) **Org admin** C) Customer support D) Random dev  
**34.** Sub-Agents used for:  
A) **Delegating agent subtasks** B) Git LFS C) DNS D) Laptop sleep  
**35.** Copilot Spaces:  
A) **Shared context** B) Disk partition C) SSH D) Compiler  
**36.** Plan Mode emphasizes:  
A) **Planning before execution** B) Deleting tests C) No AI D) VPN  
**37.** Edit Mode vs Agent Mode:  
A) Edit is more targeted; Agent more autonomous B) Identical C) Opposite of Copilot D) CLI only  
**38.** PR summary feature tier (typical):  
A) Free B) **Enterprise** C) None D) Random  
**39.** Web search in Copilot (Bing) tier (typical):  
A) Pro B) **Enterprise** C) Free D) All  
**40.** Section 1 submitted — can you return?  
A) Yes anytime B) **No**

#### Practice Exam 1 — Answer Key

| Q | Ans | Rationale |
|---|-----|-----------|
| 1 | B | GH-300 = GitHub Copilot |
| 2 | C | Official passing score 700 |
| 3 | C | Human accountability |
| 4 | B | Validation required |
| 5 | B | Hallucination definition |
| 6 | B | Agent Mode scope |
| 7 | B | MCP standard |
| 8 | C | Business+ feature |
| 9 | B | Major exam trap |
| 10 | B | Business SSO enforcement |
| 11 | B | IP indemnity Business+ |
| 12 | B | Proxy pre-process |
| 13 | A | Post-process filtering |
| 14 | B | Enterprise zero retention IDE |
| 15 | B | CLI/agent monitoring |
| 16 | A | Zero-shot definition |
| 17 | A | Non-obvious patterns |
| 18 | A | Four Ss |
| 19 | B | Prompt engineering |
| 20 | A | Instructions files |
| 21 | A | Test prompts |
| 22 | B | No auto-merge |
| 23 | B | Integration context |
| 24 | A | Refactor practice |
| 25 | B | Security validation |
| 26 | A | Duplication detection |
| 27 | B | IP block setting |
| 28 | B | Admin roles |
| 29 | B | Maintain = view |
| 30 | B | Propagation delay |
| 31 | A | Policy hierarchy |
| 32 | B | Audit logs |
| 33 | B | Admin policies |
| 34 | A | Sub-Agents |
| 35 | A | Spaces |
| 36 | A | Plan Mode |
| 37 | A | Mode distinction |
| 38 | B | Enterprise feature |
| 39 | B | Enterprise search |
| 40 | B | Section lock |

#### Practice Exam 1 — Diagnostic Rubric

| If you missed… | Review |
|----------------|--------|
| Q1–5 | Domain 1 Responsible AI |
| Q6–11, 34–39 | Domains 2–3 Features & plans |
| Q12–15 | Domain 4 Architecture |
| Q16–20 | Domain 5 Prompting |
| Q21–25 | Domain 6 Productivity |
| Q26–33 | Domain 7 Privacy |
| Q40 | Section 1 strategy (Sec 6) |

---

### Practice Exam 2 (45 Questions)

**1.** Transparency principle:  
A) Hide model B) **Explain processing/filters** C) Skip docs D) Disable logs  
**2.** Fairness in AI:  
A) Equitable outcomes B) Faster CPU C) More RAM D) Git forks  
**3.** Agent completes build — next step?  
A) Auto-release B) **Human review + CI** C) Delete branch D) Disable Git  
**4.** Enable Copilot IDE steps include:  
A) Extension + auth + policy B) Only reboot C) Only Docker D) VPN only  
**5.** Copilot CLI install:  
A) Required for all exams physically B) **Separate CLI setup** C) Impossible D) Only Linux 1990  
**6.** Interactive CLI sessions:  
A) Supported B) Not supported  
**7.** Feature: block Copilot from `.env` in IDE:  
A) Branch protection B) **Content exclusion** C) README D) Stars  
**8.** Prevent Agent reading secrets via exclusion alone:  
A) Always works B) **Does not apply to Agent Mode**  
**9.** Bing-grounded search plan:  
A) Free B) Enterprise C) None D) Random  
**10.** Fine-tuned models:  
A) Enterprise B) Free C) Everyone D) None  
**11.** Knowledge Bases tier:  
A) Enterprise B) Pro C) Free D) All  
**12.** Copilot Spark relates to:  
A) App building B) Database only C) DNS D) SSH  
**13.** Prompt file reuse helps:  
A) Consistency B) Chaos C) Deletes code D) Removes SSO  
**14.** Chat command knowledge:  
A) Productivity feature B) Unrelated C) Only Git D) Only Issues  
**15.** REST API manages:  
A) **Subscriptions/seats** B) Coffee C) Monitors D) Chairs  
**16.** Context gathering uses:  
A) Open files/selection/comments B) Nothing C) Only email D) Only Twitter  
**17.** LLM may fail because:  
A) Missing private context B) Too many tabs always C) GitHub logo color D) Monday  
**18.** Toxicity filter stage:  
A) Pre and/or post proxy B) Only after merge C) Never D) Only Issues  
**19.** Public code match may cause:  
A) Discard/warn/block B) Free Pro+ C) Auto star D) VPN  
**20.** Individual users opt out of training:  
A) Possible in settings B) Impossible always C) Deletes account D) Removes Git  
**21.** Telemetry retention (~):  
A) 2 years B) 1 second C) Never D) 100 years  
**22.** Chat history:  
A) Session context B) Replaces git blame C) Deletes repo D) SSO  
**23.** Surrounded (4 Ss):  
A) Provide code context B) Hide code C) Remove tests D) Ban comments  
**24.** Multi-task prompt problem:  
A) Mixed-quality output B) Faster builds C) Free Enterprise D) Auto merge  
**25.** Legacy modernization:  
A) Incremental validated steps B) Blind rewrite C) Delete VCS D) No tests  
**26.** Sample data generation:  
A) Valid use case B) Exam forbidden C) Illegal D) Only Java 1.0  
**27.** Edge cases in tests:  
A) Explicitly request in prompt B) Never test C) Auto illegal D) Only UI  
**28.** Assertions:  
A) Ask Copilot to include B) Never use C) Ban Jest D) Remove CI  
**29.** Performance optimization prompts:  
A) Valid productivity use B) Not on exam C) Banned D) Only hardware  
**30.** Editor setting duplication warning:  
A) Alerts user B) Same as block always C) Deletes file D) Removes org  
**31.** Block vs warn:  
A) Block prevents suggestion B) Identical C) Opposite of Copilot D) Random  
**32.** Output ownership:  
A) User responsible to validate B) Microsoft owns all code C) No one D) Bot merges  
**33.** Troubleshoot exclusions:  
A) Check role, propagation, path pattern B) Ignore C) Only reboot D) Delete org  
**34.** Org enables Code Review for all repos:  
A) Policy management B) Individual only C) Impossible D) Only Free  
**35.** Feature availability across IDEs:  
A) Admin can manage B) Only one IDE ever C) Random D) None  
**36.** Negative agent constraint:  
A) “Do not write files” B) “Hack prod” C) “Share secrets” D) “Skip review”  
**37.** Copilot for learning codebase:  
A) Explain selected code B) Replace onboarding C) Remove docs D) Delete wiki  
**38.** Reduce context switching:  
A) In-IDE answers B) More apps C) Disable IDE D) Remove Chat  
**39.** Multiple-response strategy:  
A) Select every fully correct option B) Pick one only always C) Skip D) Random  
**40.** Preview features on exam:  
A) If commonly used B) Never C) Only beta exams D) Illegal  
**41.** Renewal path:  
A) Free Learn assessment B) Full price always C) Essay only D) None  
**42.** JetBrains Copilot:  
A) Supported B) Not supported  
**43.** Visual Studio Copilot:  
A) Supported B) Not supported  
**44.** github.com Copilot Chat:  
A) Exists B) Does not exist ever  
**45.** Exam language delay for localized versions (~):  
A) 8 weeks after English B) Same hour C) 5 years D) Never  

#### Practice Exam 2 — Answer Key

| Q | Ans |
|---|-----|
| 1 | A |
| 2 | A |
| 3 | B |
| 4 | A |
| 5 | B |
| 6 | A |
| 7 | B |
| 8 | B |
| 9 | B |
| 10 | A |
| 11 | A |
| 12 | A |
| 13 | A |
| 14 | A |
| 15 | A |
| 16 | A |
| 17 | A |
| 18 | A |
| 19 | A |
| 20 | A |
| 21 | A |
| 22 | A |
| 23 | A |
| 24 | A |
| 25 | A |
| 26 | A |
| 27 | A |
| 28 | A |
| 29 | A |
| 30 | A |
| 31 | A |
| 32 | A |
| 33 | A |
| 34 | A |
| 35 | A |
| 36 | A |
| 37 | A |
| 38 | A |
| 39 | A |
| 40 | A |
| 41 | A |
| 42 | A |
| 43 | A |
| 44 | A |
| 45 | A |

**Rationale summary:** Q8/9/10/11 test Enterprise-only features; Q7/8/30–33 test exclusions vs safeguards; Q16–21 architecture; Q22–28 prompting/productivity; Q34–35 org admin.

#### Practice Exam 2 — Diagnostic Rubric

| Missed cluster | Topic gap |
|----------------|-----------|
| Q1–3 | Responsible AI |
| Q4–15, 34–35, 42–44 | Features & admin |
| Q16–21 | Data architecture |
| Q22–28 | Prompting & productivity |
| Q29–33 | Safeguards |
| Q39–41 | Exam mechanics |

**Target score before real exam:** ≥85% (34/40) on Exam 1 and ≥38/45 on Exam 2.

---

### Practice Exam 3 (50 Questions) — Mixed Difficulty

*Abbreviated stems — higher difficulty.*

1. Company on **Pro** needs content exclusion → upgrade to **Business** (T/F) **T**  
2. Exclusion stops Agent Mode reading `/keys` → **F**  
3. IP indemnity on Business without block public code → incomplete **T**  
4. Proxy is optional decoration → **F**  
5. Zero retention IDE Business → **T**  
6. CLI 28-day monitoring → **T**  
7. Few-shot for standard `for` loop → usually overkill **T**  
8. Copilot auto-approves PRs → **F**  
9. Maintain edits exclusions → **F**  
10. Enterprise policy can override org exclusion → **T**  
11. MCP from Anthropic-origin standard → **T**  
12. Sub-Agents reduce context load → **T**  
13. Instructions file = prompt reuse → **T**  
14. Hallucinated package name — ship if compiles → **F**  
15. Duplication warning = legal advice → **F**  
16. Post-process security scan exists → **T**  
17. Agent “plan only” = negative constraint → **T**  
18. PR summary on Free tier typically → **F**  
19. SAML on Business → **T**  
20. Audit logs on Free org-wide → **F**  
21. Multiple-response: select IP indemnity requirements → **Business+ AND block public code**  
22. Multiple-response: validation steps → **Review, test, security check**  
23. Scenario: exclusion set but IDE still suggests — **wait propagation / restart session**  
24. Scenario: need web search in chat — **Enterprise**  
25. Scenario: vague “fix bug” fails — **add stack trace + file context**  
26. Scenario: integration tests without mocks fail quality — **add mock strategy**  
27. Scenario: GPL match suggestion — **review + duplication settings**  
28. Scenario: admin audit who disabled Copilot — **audit log**  
29. Scenario: seat management automation — **REST API**  
30. Scenario: secrets in Agent workflow — **not exclusion alone**  
31. Hard: telemetry vs prompt retention — **different policies**  
32. Hard: individual opt-out training — **settings available**  
33. Hard: Plan Mode before large refactor — **recommended**  
34. Hard: Edit Mode for scoped rename — **appropriate**  
35. Hard: Copilot Spaces — **shared team context**  
36. Hard: Spark — **app building**  
37. Hard: Code Review policy org-wide — **admin configures**  
38. Hard: Feature off in VS Code but on in VS — **admin feature availability**  
39. Hard: Chat refuses excluded file — **expected**  
40. Hard: Excluded file context in other files — **blocked**  
41. Hard: Section 1 flag workflow — **review before advance**  
42. Hard: Passing 700 on 1000 — **scaled score**  
43. Hard: ~65 questions — **approximate**  
44. Hard: 100 minutes — **time box**  
45. Hard: Jan 2026 skills — **Agent/MCP in scope**  
46. Hard: Renewal — **Learn assessment**  
47. Hard: Programming language prereq — **yes**  
48. Hard: GitHub fundamentals prereq — **yes**  
49. Hard: GA vs Preview — **mostly GA**  
50. Hard: Responsible AI threads all domains — **T**

#### Practice Exam 3 — Diagnostic Rubric

| Score | Action |
|-------|--------|
| 45–50 | Schedule exam within 1–2 weeks |
| 38–44 | Drill weak domains; retake Exams 1–2 |
| 30–37 | Repeat 4-week plan; hands-on labs |
| <30 | Restart Fundamentals paths Part 1 & 2 |

Map misses: **T/F 1–20** → plans & exclusions; **21–30** → scenarios; **31–50** → mixed advanced.

---

## 5. Final Review

### 5.1 Four-Week Study Plan

| Week | Focus | Daily (≈60–90 min) | Weekend |
|------|-------|-------------------|---------|
| **1** | Domains 1 + 4 + 5 | Read docs; 15 flashcards; 5 practice Qs | Install Copilot; complete Learn Module 1 |
| **2** | Domains 2–3 (features) | Plan tier table recitation; CLI lab; 20 flashcards | Practice Exam 1 |
| **3** | Domains 6 + 7 | Exclusion lab; test prompts; 20 flashcards | Practice Exam 2 |
| **4** | Weak areas + exams | Missed-card drill; scenario writing | Practice Exam 3 + 48h review |

**Daily micro-routine (45 min minimum):**
1. 10 min — flashcards (focus misses)
2. 20 min — one domain deep read (Microsoft docs)
3. 10 min — 5 practice questions
4. 5 min — write one “If X think Y” note

### 5.2 48-Hour Pre-Exam Plan

**T-48h**
- [ ] Retake missed flashcards (score ≥90%)
- [ ] Redraw proxy pipeline from memory
- [ ] Recite plan tier table without notes
- [ ] List 5 things content exclusion does **not** cover

**T-24h**
- [ ] 30-question mixed drill (Domains 2, 4, 7)
- [ ] Hands-on: 5 min Chat + 5 min inline only
- [ ] No all-nighter — sleep 7+ hours

**T-2h**
- [ ] Light review: master cheat sheet only
- [ ] Prepare ID, workspace, quiet room, stable internet
- [ ] Pearson VUE system test

### 5.3 Night Before Checklist

- [ ] ID and exam appointment confirmed  
- [ ] Proctor room clear; no notes/second monitor violations  
- [ ] Water ready; bathroom break taken  
- [ ] Copilot plan tiers memorized  
- [ ] Exclusion vs Agent Mode trap reviewed  
- [ ] Section 1 review strategy internalized  
- [ ] Sleep prioritized over cramming  

### 5.4 One-Page Master Cheat Sheet

```
GH-300 GITHUB COPILOT — MASTER SHEET
====================================
PASS: 700/1000 | ~65 Q | 100 min | 2 sections (NO back to Sec 1)

DOMAINS (Jan 2026)
  Responsible AI 15-20% | Features 25-30% x2 | Architecture 10-15%
  Prompting 10-15% | Productivity 10-15% | Privacy 10-15%

ALWAYS: Validate AI output before production.

PLANS
  Free/Pro/Pro+ = individual
  Business+ = content exclusion, IP indemnity, SAML, org policies, audit logs
  Enterprise = + fine-tuned models, KB, PR summaries, Bing search (verify docs)

CONTENT EXCLUSION (Business+)
  Blocks: inline in path, context from path, chat on path
  Does NOT apply: CLI, coding agent, Agent Mode in Chat
  Editors: repo admin / org / enterprise owner | Maintain = view only
  Propagation: ~30 min

DATA FLOW
  IDE → Proxy PRE (toxicity, relevance) → LLM → Proxy POST
       (security, public code match, quality) → IDE
  Business IDE: zero prompt retention | CLI/Agent: ~28 days monitoring

PROMPTS — 4 Ss: Single, Specific, Short, Surrounded
  Zero-shot = simple | Few-shot = unusual patterns
  Instructions files = team standards

PRODUCTIVITY
  Tests: name framework + edge cases + assertions
  Security: suggest + human review + scanners
  No auto-merge PRs

IP: Business+ + "Suggestions matching public code: BLOCKED"
Duplication: WARN vs BLOCK

AGENT: MCP tools | Sub-Agents | negative constraints ("no file writes")
EXAM: Scenario → lowest plan that meets ALL requirements
      Section 1 → flag, answer all, REVIEW, then submit
```

---

## 6. Test-Day Strategy

### 6.1 Time Management

| Phase | Time | Action |
|-------|------|--------|
| Section 1 start | 0–10 min | Skim all questions; answer easy ones |
| Section 1 mid | 10–50 min | Scenarios; flag uncertain |
| Section 1 end | 50–60 min | **Review every flagged question** |
| Section 1 submit | 60 min | Only when fully reviewed |
| Section 2 | Remaining ~40 min | Same flag-review pattern |

**Pacing:** ~1.5 min/question average. Mark and move — don’t stall >3 min.

### 6.2 Handling Uncertainty

1. Eliminate clearly wrong answers (wrong tier, wrong interface, violates validation)  
2. Look for **governance keywords** (block vs warn, admin vs member)  
3. Prefer **documented Microsoft/GitHub behavior** over “what you’d prefer”  
4. On multiple-response: only select if you can defend each choice  
5. Flag and return — but **Section 1 flags must be resolved before submit**

### 6.3 Review Workflow

**During exam**
- [ ] First pass: answer all  
- [ ] Second pass: flagged only  
- [ ] Third pass: read stem again for “NOT” / “EXCEPT”  
- [ ] Section 1: final full scan before advance  

**After practice exams (study phase)**
- Log misses in table: Question → Domain → Why wrong → Flashcard #

---

## 7. Personalization Questions

Answer these to tune your schedule (guide above already works standalone):

1. What is your target exam date?  
2. Do you use Copilot daily today (Free, Pro, Business, Enterprise)?  
3. Are you an **individual developer** or **org admin** responsible for Copilot policies?  
4. Which IDE is your primary (VS Code, Visual Studio, JetBrains)?  
5. Have you used **Agent Mode, CLI, or MCP** hands-on?  
6. How many hours per week can you study (realistic)?  
7. Did you already complete *GitHub Copilot Fundamentals Part 1 & 2* on Learn?  
8. What is your weakest area (plans, architecture, prompting, privacy)?  
9. Will you test **online proctored** or at a **test center**?  
10. Do you need accommodations (extra time, assistive tech)?

**Adjustment rules:**
- **Admin track:** Add +30% time on Domains 2–3 and 7  
- **Beginner track:** Extend Week 1–2; delay practice exams until Week 3  
- **Power user track:** Still drill plan tiers and exclusions — highest fail rate  
- **<5 hrs/week:** Use 6-week plan; double flashcard days  

---

## Quick Start (Today)

1. Bookmark [official GH-300 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/gh-300)  
2. Study **plan tier table** (Section 2) — 20 minutes  
3. Run **Flashcards 1–30** (Section 3.1)  
4. Take **Practice Exam 1** timed — review diagnostics  
5. Schedule exam only after **≥85%** on two practice exams  

You’ve got this. Pass focus: **features + governance + exclusions + architecture + validate everything.**
