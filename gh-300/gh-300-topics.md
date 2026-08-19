# Exam GH-300: GitHub Copilot — Topics Overview

Official certification topics from Microsoft Learn.  
Source of truth: [Study guide for Exam GH-300](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/gh-300)  
Credential page: [GitHub Copilot certification](https://learn.microsoft.com/en-us/credentials/certifications/github-copilot/)

**Complementary study guide (setup labs, examples, exam traps):** [`./gh-300/README.md`](./gh-300/README.md)

**Skills measured as of:** August 7, 2026  
Re-check the study guide before exam day — Microsoft updates skill outlines.

Practice questions below are **unofficial study aids** styled like GH-300 scenarios. They are not Microsoft exam dumps.

---

## Table of contents

1. [Exam snapshot](#exam-snapshot)
2. [Audience profile](#audience-profile)
3. [Skills at a glance](#skills-at-a-glance)
4. [Domain 1 — Use GitHub Copilot responsibly (15–20%)](#domain-1--use-github-copilot-responsibly-1520)
5. [Domain 2 — Use GitHub Copilot features (25–30%)](#domain-2--use-github-copilot-features-2530)
6. [Domain 3 — Understand GitHub Copilot data and architecture (10–15%)](#domain-3--understand-github-copilot-data-and-architecture-1015)
7. [Domain 4 — Apply prompt engineering and context crafting (10–15%)](#domain-4--apply-prompt-engineering-and-context-crafting-1015)
8. [Domain 5 — Improve developer productivity with GitHub Copilot (10–15%)](#domain-5--improve-developer-productivity-with-github-copilot-1015)
9. [Domain 6 — Configure privacy, content exclusions, and safeguards (10–15%)](#domain-6--configure-privacy-content-exclusions-and-safeguards-1015)
10. [Official study resources](#official-study-resources)
11. [Topic checklist](#topic-checklist)
12. [Question validation notes](#question-validation-notes)

---

## Exam snapshot

| Item | Detail |
|---|---|
| Exam code | **GH-300** |
| Name | GitHub Copilot |
| Level | Intermediate |
| Focus | Using GitHub Copilot for productivity, quality, and security |
| Duration | 100 minutes |
| Passing score | 700 / 1000 |
| Delivery | Proctored (Pearson VUE; interactive components possible) |
| Languages | English, Spanish, Portuguese (Brazil), Korean, Japanese |
| Related products | GitHub |
| Typical roles | Developer, DevOps Engineer, App Maker, Technology Manager |

---

## Audience profile

Candidates should be able to use **GitHub Copilot** to improve software development **productivity**, **quality**, and **security**, including:

- Responsible AI use
- Prompt engineering
- Copilot features across plans
- Privacy safeguards

Expected background:

- Familiarity with **GitHub fundamentals**
- Experience with **one or more programming languages**

---

## Skills at a glance

| # | Skill area | Weight |
|---|---|---|
| 1 | Use GitHub Copilot responsibly | 15–20% |
| 2 | Use GitHub Copilot features | 25–30% |
| 3 | Understand GitHub Copilot data and architecture | 10–15% |
| 4 | Apply prompt engineering and context crafting | 10–15% |
| 5 | Improve developer productivity with GitHub Copilot | 10–15% |
| 6 | Configure privacy, content exclusions, and safeguards | 10–15% |

> Note: Microsoft’s certification page may list a separate “GitHub Copilot features” line; the detailed study guide groups IDE, CLI, capabilities, and org policy under **Use GitHub Copilot features**.

---

## Domain 1 — Use GitHub Copilot responsibly (15–20%)

### Understand responsible AI principles

- Describe **risks and limitations** of Generative AI tools
- Describe **ethical and responsible AI** usage
- Identify **potential harms** and **mitigation strategies** for AI usage

### Validate and operate AI tools

- Explain the need to **validate AI output**
- Identify how to **operate GitHub Copilot responsibly**

**Study focus:** human oversight, hallucinations, bias/security risks, “AI suggests — humans decide.”

### Practice questions (Domain 1)

**Q1.** A developer accepts a Copilot suggestion that compiles but uses a weak hashing algorithm for passwords. What responsible-AI concern does this primarily illustrate?

- A. Model training data leakage  
- B. Generative AI can produce insecure or outdated recommendations  
- C. Copilot cannot run inside an IDE  
- D. Content exclusions always block security libraries  

**Q2.** What is the best first response when Copilot Chat invents a library API that does not exist?

- A. Merge immediately to save time  
- B. Disable Copilot organization-wide  
- C. Validate the suggestion against docs/tests before trusting it  
- D. Assume hallucinations only happen in Preview features  

**Q3.** Which mitigation best reduces harm from biased or unfair generated code comments/policies?

- A. Never use Chat  
- B. Human review with diverse team standards and inclusive language checks  
- C. Only use inline completions  
- D. Turn off public-code filtering  

**Q4.** Why must developers validate AI-generated code even when it looks correct?

- A. Copilot never uses context from open files  
- B. Suggestions can be plausible yet wrong, insecure, or non-compliant  
- C. Validation is only required for Enterprise plans  
- D. Copilot output is legally guaranteed bug-free  

**Q5.** Which practice best represents operating GitHub Copilot responsibly day to day?

- A. Blindly accept all inline suggestions  
- B. Treat Copilot as an assistant and keep developers accountable for merged code  
- C. Paste production secrets into prompts for better context  
- D. Disable all tests because Copilot writes them  

**Q6.** A teammate wants Copilot to decide production incident root cause without engineer review. What risk is highest?

- A. Over-reliance / insufficient human oversight  
- B. IDE theme incompatibility  
- C. Missing REST API subscription endpoints  
- D. Inability to open markdown files  

**Q7.** Which statement about generative AI limitations is accurate for Copilot usage?

- A. Models always know your private roadmap  
- B. Outputs can omit edge cases and miss business constraints  
- C. Copilot replaces compliance review  
- D. Copilot cannot generate comments  

**Q8.** Identifying potential harms of AI coding assistants commonly includes which examples?

- A. Only UI color mismatch  
- B. Security flaws, license issues, privacy leakage via prompts, incorrect logic  
- C. Faster keyboard shortcuts only  
- D. Git commit signing failures only  

**Q9.** Ethical use of Copilot in a company most clearly requires that:

- A. Developers credit Copilot as author in every commit  
- B. Generated code follows company policy, licensing, and security review  
- C. Only managers may accept suggestions  
- D. Chat history is published publicly  

**Q10.** After Copilot generates unit tests that all pass, what is still a responsible next step?

- A. Delete the tests to reduce repo size  
- B. Review whether assertions actually cover meaningful edge cases and requirements  
- C. Disable coverage tools  
- D. Skip code review because tests passed  

<details>
<summary>Domain 1 answer key + explanations</summary>

1. **B** — Compiling code is not the same as being secure. Generative AI often suggests weak or outdated patterns (like insecure hashing); that is a core risk/limitation.
2. **C** — Invented APIs are hallucinations. Responsible use starts with validating against docs, types, and tests before trusting the suggestion.
3. **B** — Bias/unfair language is mitigated by human review against team standards, not by disabling features wholesale.
4. **B** — Plausible output can still be wrong, insecure, or non-compliant. Validation is required on every plan.
5. **B** — Copilot is an assistant; developers stay accountable for what is reviewed and merged.
6. **A** — Letting AI alone drive incident root cause is over-reliance and insufficient human oversight.
7. **B** — Models routinely miss edge cases and unspoken business rules even when syntax looks fine.
8. **B** — Typical harms include security bugs, license risk, privacy leakage via prompts, and incorrect logic.
9. **B** — Ethical workplace use means accepted code must still meet policy, licensing, and security review.
10. **B** — Passing tests can be shallow. Review assertions for real requirements and edge coverage before relying on them.

</details>

---

## Domain 2 — Use GitHub Copilot features (25–30%)

Largest domain — know product surface area and plan/policy differences.

### Use GitHub Copilot in the IDE

- Enable Copilot in the IDE
- Trigger Copilot through:
  - Inline suggestions
  - Chat
  - CLI
  - Agent mode
- Configure **content exclusions** for specific files or repositories (app knowledge)

### Use GitHub Copilot CLI

- Define GitHub Copilot CLI and how it benefits developers
- Identify steps for **installing** GitHub Copilot CLI
- Describe key CLI **features and commands**
- Use Copilot CLI **interactively** and in **sessions**
- Generate **scripts** and manage **files** with Copilot CLI

### Use GitHub Copilot features and capabilities

- Use **Agent Mode**, **Copilot Edits**, and **MCP** for enhanced development and workflows
- Manage **Agent Sessions** and delegate tasks to **Sub-Agents** for optimized context usage
- Use Copilot for **code review** and coding assistance
- Utilize **Spaces**, **Spark**, **Pull Request summaries**, and customizable review standards via **instructions files**
- Understand limits, options, feedback, and commands of **GitHub Copilot Chat**
- Include **prompt file** reuse for consistent responses

### Manage organization-wide settings and policies

- Configure **organization-wide policy** management
- Enable Copilot **Code Review** policies
- Manage feature availability across **IDEs** and **github.com**
- Utilize **audit log** events
- Manage **subscriptions** using the **REST API**

**Study focus:** what exists where (Individual / Business / Enterprise), Agent vs Edits, Chat commands, org admin controls.

### Practice questions (Domain 2)

**Q1.** A developer wants multi-step changes that may include running terminal commands autonomously. Which capability is the best fit?

- A. Inline ghost-text only  
- B. Agent Mode  
- C. Public-code filter only  
- D. Content exclusion patterns only  

**Q2.** What is a primary benefit of GitHub Copilot CLI for developers?

- A. Replaces Git remotes  
- B. Brings Copilot assistance into the terminal for scripting and file tasks  
- C. Hosts production databases  
- D. Disables IDE extensions automatically  

**Q3.** Which action typically comes first when enabling Copilot in an IDE?

- A. Delete `.gitignore`  
- B. Install/sign in to the Copilot extension/plugin and authenticate  
- C. Disable TLS  
- D. Fork every repository  

**Q4.** You need multi-file code changes you can review and selectively accept, without handing full autonomous terminal control to an agent. Which approach fits best?

- A. Copilot Edits / Edit Mode–style workflows for reviewing proposed changes  
- B. Only inline single-line ghost text with no Chat  
- C. Organization audit logs  
- D. Content exclusion patterns  

**Q5.** What does MCP enable in Copilot-enhanced workflows?

- A. Mandatory commit hooks only  
- B. Connecting Copilot agents to external tools/context sources through a protocolized integration  
- C. Free Enterprise seats for all users  
- D. Automatic deletion of audit logs  

**Q6.** An org admin must restrict which Copilot features are available in IDEs and on github.com. Where is this primarily handled?

- A. Random README files  
- B. Organization-wide Copilot policy / feature management settings  
- C. Personal VS Code color themes  
- D. npm scripts  

**Q7.** Why use Sub-Agents within Agent Sessions?

- A. To remove the need for authentication  
- B. To delegate specialized work and optimize context usage across tasks  
- C. To replace CI pipelines entirely  
- D. To encrypt disks  

**Q8.** Instructions files are most useful for:

- A. Customizing recurring review/coding standards so Copilot follows team norms  
- B. Storing production passwords  
- C. Replacing branch protection  
- D. Billing invoices only  

**Q9.** Which statement about Copilot Chat commands and feedback options is most accurate?

- A. Chat has no commands and cannot accept feedback  
- B. Chat supports commands/options to steer responses, and users/orgs can provide feedback according to product settings and policies  
- C. Submitting feedback always publishes your private repository publicly  
- D. Chat commands only work if content exclusions are disabled  

**Q10.** An administrator needs to review who enabled Copilot features and related activity for compliance. What should they use?

- A. Only local browser history  
- B. Organization audit log events related to Copilot  
- C. PR emoji reactions only  
- D. Docker Hub stars  

<details>
<summary>Domain 2 answer key + explanations</summary>

1. **B** — Agent Mode is built for multi-step autonomous work, including terminal actions when allowed.
2. **B** — Copilot CLI brings assistant workflows into the terminal (scripts, files, interactive sessions), not git remotes or hosting.
3. **B** — Enabling Copilot starts with installing the IDE extension/plugin and authenticating to a licensed account.
4. **A** — Edit Mode / Copilot Edits focuses on proposed multi-file changes you review and accept selectively, without full agent autonomy.
5. **B** — MCP connects agents to external tools and data sources through a standard integration protocol.
6. **B** — Org (and enterprise) Copilot policies control which features are available in IDEs and on github.com.
7. **B** — Sub-Agents handle delegated work in isolated context so the main agent session stays focused and efficient.
8. **A** — Instructions files encode recurring coding/review standards so Copilot follows team norms consistently.
9. **B** — Chat supports commands/options to steer responses; feedback exists under product/org policy settings (it does not auto-publish private code).
10. **B** — Organization/enterprise audit logs record Copilot plan, policy, license, and related admin/agent activity for compliance.

</details>

---

## Domain 3 — Understand GitHub Copilot data and architecture (10–15%)

### Describe data handling and flow

- Explain **data usage, flow, and sharing**
- Describe **input processing** and **prompt building**
- Explain **proxy filtering** and **post-processing**

### Understand lifecycle and limitations

- Visualize the **code suggestion lifecycle**
- Describe **limitations of LLMs** and Copilot

**Study focus:** what context is sent, how suggestions are produced/filtered, what Copilot cannot reliably do.

### Practice questions (Domain 3)

**Q1.** In a typical suggestion lifecycle, what happens after the IDE gathers context and builds a prompt?

- A. The prompt is ignored and a random snippet is inserted  
- B. The request is processed by Copilot’s service/model pipeline, then suggestions are returned for user acceptance  
- C. Git automatically merges to main  
- D. The disk is reformatted  

**Q2.** “Prompt building” in Copilot architecture most nearly means:

- A. Compiling C++ only  
- B. Assembling model input from user intent plus relevant available context  
- C. Creating invoices  
- D. Signing commits  

**Q3.** Proxy filtering / policy enforcement in the data path is best described as:

- A. Cosmetic UI sorting of chat threads  
- B. Intermediate checks that can filter or constrain requests/responses according to product/policy safeguards  
- C. Replacing your firewall entirely  
- D. Deleting excluded files from disk  

**Q4.** Why is understanding data flow important for enterprises adopting Copilot?

- A. To know what context may leave the workstation and how policies affect sharing/retention behavior  
- B. Because Copilot stores all code in public Gists by default  
- C. Because Copilot requires FTP  
- D. Because models run only on the developer laptop with zero network  

**Q5.** A key LLM limitation relevant to Copilot is that models may:

- A. Never generate syntax errors in any language  
- B. Confidently suggest incorrect APIs or outdated patterns  
- C. Automatically pass all compliance audits  
- D. Know secrets without being given them  

**Q6.** After a model produces candidate completions, post-processing commonly includes:

- A. Policy/safety/filter steps (for example public-code matching checks) before results are shown  
- B. Automatic force-push of the suggestion to `main`  
- C. Permanent deletion of the prompt from the developer machine only  
- D. Replacing the user’s Git remote URLs  

**Q7.** Which input is commonly part of context for inline completions?

- A. Only the company lunch menu  
- B. Nearby code, comments, and relevant file/editor context when available  
- C. Unrelated private emails always  
- D. All of GitHub.com at once without limits  

**Q8.** Visualizing the suggestion lifecycle helps a developer understand that:

- A. Acceptance is automatic and irreversible  
- B. Suggestions are proposed outputs the developer can accept, reject, or edit  
- C. Copilot bypasses source control  
- D. Lifecycle only applies to CLI  

**Q9.** For organizational code, a common architecture/policy expectation candidates should know is that product offerings distinguish how business telemetry/training uses customer code — so you should:

- A. Assume every plan trains public models on your private repos  
- B. Verify current Microsoft/GitHub documentation for your plan’s data-handling promises  
- C. Ignore all privacy settings  
- D. Publish `.env` files to improve completions  

**Q10.** Which statement best reflects Copilot limitations vs human engineers?

- A. Copilot fully understands undocumented tribal business rules without context  
- B. Copilot lacks full product judgment; engineers must supply intent and verify outcomes  
- C. Copilot can replace security incident commanders  
- D. Copilot guarantees identical output every time for the same prompt  

<details>
<summary>Domain 3 answer key + explanations</summary>

1. **B** — After context/prompt assembly, the request goes through Copilot’s service/model pipeline and returns suggestions for the developer to accept or reject.
2. **B** — Prompt building means combining user intent with available editor/repo context into model input.
3. **B** — Proxy/policy layers can filter or constrain requests and responses (safeguards, plan/policy controls)—not delete files or replace firewalls.
4. **A** — Enterprises need to know what context may leave the workstation and how retention/sharing/policy settings apply.
5. **B** — LLMs often invent or outdated APIs with high confidence; that is a primary practical limitation.
6. **A** — Post-processing can apply safety/policy filters (for example public-code matching) before showing candidates.
7. **B** — Inline completions commonly use nearby code, comments, and other available editor/file context.
8. **B** — Suggestions are proposals; the developer accepts, rejects, or edits them—they are not auto-merged.
9. **B** — Data-handling rules differ by product/plan and change over time; always verify current Microsoft/GitHub documentation for your plan.
10. **B** — Copilot lacks full product/judgment context; engineers must supply intent and verify outcomes.

</details>

---

## Domain 4 — Apply prompt engineering and context crafting (10–15%)

### Craft effective prompts

- Describe **prompt structure** and **context**
- Understand how **context is determined**
- Use **zero-shot** and **few-shot** prompting
- Apply **best practices** for prompt crafting

### Engineer prompts for performance

- Explain **prompt engineering principles**
- Describe **prompt process flow** and **chat history** usage

**Study focus:** clear intent, constraints, examples, relevant open files/context, iterating when answers are weak.

### Practice questions (Domain 4)

**Q1.** Which prompt is better structured for generating a payment validator?

- A. “Fix it”  
- B. “Write a C# method `ValidatePayment(PaymentRequest request)` that rejects nulls and unsupported currencies; include XML docs and two usage examples”  
- C. “Code”  
- D. “???”  

**Q2.** Zero-shot prompting means:

- A. Providing no task description  
- B. Asking the model to perform a task without giving examples  
- C. Using exactly zero tokens  
- D. Disabling Copilot  

**Q3.** Few-shot prompting improves results by:

- A. Removing all context  
- B. Providing one or more examples of desired input/output patterns  
- C. Always generating fewer lines of code  
- D. Preventing Chat history  

**Q4.** Context for Copilot Chat is often influenced by:

- A. Only your desktop wallpaper  
- B. Conversation history, open/selected files, and explicit references you attach or mention  
- C. Unrelated DNS caches exclusively  
- D. Printer drivers  

**Q5.** A best practice when a first answer is wrong is to:

- A. Accept it anyway  
- B. Iterate: add constraints, examples, error messages, and relevant file context  
- C. Uninstall Git  
- D. Switch keyboard layout  

**Q6.** Which principle improves prompt performance most consistently?

- A. Ambiguous goals with hidden requirements  
- B. Clear goal, constraints, language/framework, and success criteria  
- C. Asking for “magic”  
- D. Including secrets for “realism”  

**Q7.** Prompt process flow in Chat typically uses prior turns so that:

- A. Chat history can refine follow-ups without restating everything each time  
- B. History is never used  
- C. History automatically pushes to production  
- D. History bypasses content exclusions always  

**Q8.** You want Copilot to match an existing coding style. What should you do?

- A. Avoid opening any files  
- B. Provide few-shot examples or point Copilot at representative code/instructions files  
- C. Only use zero-shot forever  
- D. Disable syntax highlighting  

**Q9.** Which prompt issue most often leads to low-quality suggestions?

- A. Over-specified acceptance criteria  
- B. Missing language, unclear intent, and no constraints  
- C. Including unit test names  
- D. Asking for documentation  

**Q10.** Reusable prompt files are valuable because they:

- A. Guarantee zero hallucinations  
- B. Standardize recurring instructions so responses stay consistent across sessions/team members  
- C. Replace CI  
- D. Disable inline suggestions  

<details>
<summary>Domain 4 answer key + explanations</summary>

1. **B** — Strong prompts state language, signature, constraints, and deliverables; vague prompts like “Fix it” under-specify the task.
2. **B** — Zero-shot means asking for a task with no worked examples (still with a clear instruction).
3. **B** — Few-shot adds one or more examples so the model mirrors the desired pattern.
4. **B** — Chat context typically includes history plus open/selected files and anything you explicitly attach or reference.
5. **B** — When wrong, iterate: tighten constraints, add examples/errors, and attach relevant files.
6. **B** — Clear goals, constraints, stack, and success criteria reliably improve prompt performance.
7. **A** — Prior chat turns let follow-ups refine the task without restating every detail each time.
8. **B** — Style matching improves with few-shot examples or instructions/representative code as context.
9. **B** — Missing language, unclear intent, and missing constraints are the most common causes of weak output.
10. **B** — Prompt files reuse standard instructions so responses stay consistent across sessions/people (they do not eliminate hallucinations).

</details>

---

## Domain 5 — Improve developer productivity with GitHub Copilot (10–15%)

### Enhance productivity and code quality

- Use Copilot for:
  - Code generation
  - Refactoring
  - Documentation
- Accelerate learning and reduce **context switching**
- Generate **sample data**
- Modernize **legacy code**

### Support testing and security

- Generate **unit** and **integration** tests
- Identify **edge cases** and write **assertions**
- Suggest **security improvements**
- Suggest **performance optimizations**

**Study focus:** real developer workflows — write, explain, test, harden — with validation of AI output.

### Practice questions (Domain 5)

**Q1.** A developer needs JSDoc/XML docs for a public API quickly. Copilot is most helpful for:

- A. Generating first-draft documentation from signatures and comments for human edit  
- B. Deleting the API  
- C. Changing DNS records  
- D. Issuing TLS certs on the public internet  

**Q2.** Which Copilot use case best reduces context switching while learning a new codebase?

- A. Asking Chat to explain a selected unfamiliar function in place  
- B. Browsing random unrelated repos without prompts  
- C. Turning off the editor  
- D. Only reading binary files  

**Q3.** You ask Copilot to modernize a legacy module. What is the safest workflow?

- A. Replace everything unreviewed  
- B. Generate proposed refactors in small increments, run tests, and review behavior  
- C. Skip compilation  
- D. Force-push untested rewrites  

**Q4.** Generating sample data with Copilot is most useful when:

- A. You need realistic fixtures for local demos/tests without handcrafting every record  
- B. You need production PII from customers  
- C. You want to email passwords  
- D. You disable source control  

**Q5.** For unit tests, Copilot can help most by:

- A. Inventing a new language runtime  
- B. Drafting tests and assertions from method behavior descriptions you provide  
- C. Guaranteeing 100% mutation coverage automatically  
- D. Removing edge cases  

**Q6.** Which follow-up best improves generated tests?

- A. “Make tests shorter only”  
- B. “Add edge cases: null input, empty collection, max boundary; assert thrown exceptions”  
- C. “Delete assertions”  
- D. “Ignore failures”  

**Q7.** A security-focused prompt to Copilot should ask for:

- A. Hard-coded credentials for convenience  
- B. Threat-minded review: injection risks, authz checks, secrets handling, dependency concerns  
- C. Disabling HTTPS  
- D. Logging full card numbers  

**Q8.** Copilot suggests a caching layer for a hot path. What should you do next?

- A. Ship immediately  
- B. Validate correctness, concurrency, invalidation rules, and measure performance  
- C. Assume microbenchmarks are unnecessary  
- D. Cache security tokens forever in cookies  

**Q9.** Integration tests generated by Copilot still require:

- A. No environment setup ever  
- B. Human verification of boundaries, test doubles vs real dependencies, and meaningful assertions  
- C. Disabling CI  
- D. Production writes on every run  

**Q10.** Refactoring with Copilot is most productive when prompts specify:

- A. “Improve somehow”  
- B. Target structure, naming standards, and invariants that must not change  
- C. Random formatting only  
- D. Removing all types  

<details>
<summary>Domain 5 answer key + explanations</summary>

1. **A** — Copilot is strong at drafting docs from signatures/comments; humans still edit for accuracy.
2. **A** — Explaining selected code in Chat reduces context switching versus leaving the IDE to hunt docs.
3. **B** — Legacy modernization should be incremental with tests and behavior review—not unreviewed rewrites.
4. **A** — Sample/fixture data generation speeds demos and tests; it must not use real customer PII.
5. **B** — Copilot drafts unit tests from described behavior; it does not guarantee complete coverage by itself.
6. **B** — Asking for concrete edge cases and assertions materially improves generated tests.
7. **B** — Security prompts should request threat-minded review (injection, authz, secrets, dependencies)—never hard-coded credentials.
8. **B** — Performance ideas still need correctness, concurrency/invalidation checks, and measurement before shipping.
9. **B** — Integration tests need human checks of scope, doubles vs real deps, and meaningful assertions.
10. **B** — Productive refactor prompts specify target structure, naming, and invariants that must not change.

</details>

---

## Domain 6 — Configure privacy, content exclusions, and safeguards (10–15%)

### Manage privacy settings and exclusions

- Configure **content exclusions** and **editor settings**
- Describe **ownership** and **limitations of outputs**

### Apply safeguards and troubleshoot

- Enable **suggestions matching public code** filtering (duplication detection / public-code matching filters)
- Resolve issues with **suggestions** and **content exclusions**

**Study focus:** what exclusions do and do not guarantee; output IP/ownership caveats; safeguard toggles and troubleshooting; Agent/Edit/CLI exclusion limits.

### Practice questions (Domain 6)

**Q1.** What does configuring content exclusions do for supported Copilot surfaces?

- A. Delete excluded files from Git history  
- B. Stop inline suggestions in excluded files and stop those files from informing other suggestions, Chat (where supported), and Copilot code review  
- C. Block all outbound HTTPS from the IDE  
- D. Force excluded files to be used as training data  

**Q2.** A developer expects exclusions to guarantee no sensitive data ever appears in prompts. What is the accurate understanding?

- A. Exclusions apply to configured paths on supported surfaces; developers must still avoid pasting secrets into Chat and know IDE may expose limited semantic info indirectly  
- B. Exclusions encrypt the entire laptop disk  
- C. Exclusions disable GitHub authentication  
- D. Exclusions remove all license obligations for accepted code  

**Q3.** Setting suggestions matching public code to **Block** is intended to:

- A. Speed up `git fetch`  
- B. Suppress completions that closely match public GitHub code (subject to product/surface support)  
- C. Publish your private repositories  
- D. Eliminate any need for license or security review of accepted code  

**Q4.** Regarding ownership of Copilot suggestions, which statement is accurate?

- A. GitHub claims ownership of every suggestion you accept  
- B. GitHub does not claim ownership of suggestions; you remain responsible for code you choose to accept and use  
- C. Only Copilot Enterprise customers own suggestions  
- D. Suggestions can never be used in commercial software  

**Q5.** Inline suggestions in other files suddenly seem unaware of an internal SDK file that used to help completions. What should you check first?

- A. Whether that SDK path is covered by a content exclusion rule  
- B. Whether the repository has too many stars  
- C. Whether Chat slash commands are disabled globally forever  
- D. Whether the user renamed their GitHub username  

**Q6.** Which statement about content exclusions is documented correctly?

- A. Exclusions always apply equally to inline suggestions, Chat, Edit/Agent modes, Copilot CLI, and cloud agents  
- B. Exclusions can apply to inline suggestions and Chat on supported plans/surfaces, but Edit/Agent modes (and some agents/CLI) may not fully honor them  
- C. Exclusions are available only on Copilot Free with no org seat  
- D. Exclusions permanently purge matching blobs from GitHub.com  

**Q7.** After an admin sets public-code matching to Block, a user notices fewer completions. What is the most likely explanation?

- A. Copilot licenses were all revoked  
- B. Matching/near-matching public-code suggestions are being filtered out by policy  
- C. The repository was force-deleted  
- D. Content exclusions always disable inline suggestions in every file  

**Q8.** Troubleshooting poorer suggestions after adding exclusions should include:

- A. Confirming needed reference files are not excluded (on supported surfaces) and prompts still supply essential non-secret context  
- B. Excluding the entire monorepo and expecting better answers  
- C. Pasting production secrets into Chat to compensate  
- D. Disabling unit tests  

**Q9.** Content exclusions configured at organization or repository scope are valuable because they:

- A. Help enforce consistent privacy controls beyond individual developer habits  
- B. Replace identity and access management (IAM)  
- C. Automatically patch CVEs in dependencies  
- D. Remove the need for human code review  

**Q10.** A user reports Copilot “isn’t using” an opened secrets file. The path is excluded by org policy. What is the correct response?

- A. Rename the file solely to bypass policy without security approval  
- B. Keep the exclusion as intended and provide non-secret docs/interfaces as allowed context instead  
- C. Commit the secrets file to a public repository for easier context  
- D. Disable branch protection rules  

<details>
<summary>Domain 6 answer key + explanations</summary>

1. **B** — On supported surfaces, exclusions disable suggestions *in* those files and stop that content from informing other suggestions, Chat, and Copilot code review.
2. **A** — Exclusions are path/policy controls, not a secret vault. Do not paste secrets into Chat; IDE semantics may still leak limited info indirectly.
3. **B** — **Block** suppresses completions that closely match public GitHub code (where the filter is supported); it does not replace license review.
4. **B** — GitHub’s terms: it does not claim ownership of suggestions; you remain responsible for what you accept and ship.
5. **A** — If other files stop “seeing” an SDK file, check whether that path is excluded first.
6. **B** — Documented caveat: exclusions are not fully honored in Edit/Agent modes (and some CLI/agent surfaces), even when inline/Chat exclusions work.
7. **B** — Fewer suggestions after enabling Block usually means matching public-code candidates are being filtered.
8. **A** — If quality drops after exclusions, ensure needed non-secret reference files are still available as context and prompts compensate explicitly.
9. **A** — Org/repo exclusions scale privacy controls beyond each developer’s personal habits.
10. **B** — Keep the exclusion; supply allowed non-secret interfaces/docs instead of trying to bypass policy with secrets files.

</details>

---

## Official study resources

| Resource | Link / note |
|---|---|
| Exam study guide | [GH-300 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/gh-300) |
| Certification page | [GitHub Copilot](https://learn.microsoft.com/en-us/credentials/certifications/github-copilot/) |
| Learning paths | GitHub Copilot Fundamentals Part 1 of 2; Part 2 of 2 (Microsoft Learn) |
| Practice assessment | Available from the certification page on Microsoft Learn |
| Exam sandbox | Practice the exam UI before test day |
| Docs themes called out by Microsoft | Responsible AI; plans/features; how Copilot works & data; prompt crafting; developer use cases; testing; privacy & exclusions |

---

## Topic checklist

Use this as a coverage tracker while studying.

### Responsible use
- [ ] Risks and limitations of generative AI
- [ ] Ethical / responsible usage
- [ ] Potential harms and mitigations
- [ ] Why AI output must be validated
- [ ] Operating Copilot responsibly day to day

### Features (IDE / CLI / capabilities / org)
- [ ] Enable Copilot in IDE
- [ ] Inline suggestions, Chat, CLI, Agent mode triggers
- [ ] Content exclusions (files/repos)
- [ ] Install and use Copilot CLI (interactive + sessions)
- [ ] Scripts/file management via CLI
- [ ] Agent Mode, Copilot Edits, MCP
- [ ] Agent Sessions and Sub-Agents
- [ ] Copilot code review / coding assistance
- [ ] Spaces, Spark, PR summaries, instructions files
- [ ] Copilot Chat limits, options, feedback, commands, prompt files
- [ ] Org policies, Code Review policies, feature availability
- [ ] Audit logs
- [ ] Subscription management via REST API

### Data and architecture
- [ ] Data usage, flow, sharing
- [ ] Input processing / prompt building
- [ ] Proxy filtering / post-processing
- [ ] Suggestion lifecycle
- [ ] LLM and Copilot limitations

### Prompt engineering
- [ ] Prompt structure and context
- [ ] How context is determined
- [ ] Zero-shot vs few-shot
- [ ] Prompt best practices
- [ ] Prompt engineering principles
- [ ] Process flow and chat history

### Productivity
- [ ] Generation, refactoring, documentation
- [ ] Learning / less context switching
- [ ] Sample data and legacy modernization
- [ ] Unit/integration tests, edge cases, assertions
- [ ] Security and performance suggestions

### Privacy and safeguards
- [ ] Content exclusions and editor settings
- [ ] Ownership / limitations of outputs
- [ ] Public-code matching / duplication filtering
- [ ] Troubleshooting suggestions and exclusions

---

## Question validation notes

All **60** practice items were reviewed against:

- [GH-300 skills measured (Microsoft Learn)](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/gh-300)
- [Content exclusion for GitHub Copilot](https://docs.github.com/en/copilot/concepts/context/content-exclusion)
- [Excluding content from GitHub Copilot](https://docs.github.com/en/copilot/how-tos/configure-content-exclusion/exclude-content-from-copilot)
- [Managing suggestions matching public code](https://docs.github.com/en/copilot/how-tos/manage-your-account/manage-policies)
- [Copilot customization cheat sheet](https://docs.github.com/en/copilot/reference/customization-cheat-sheet) (instructions, prompt files, subagents)
- [Copilot policies / audit logs](https://docs.github.com/en/copilot/how-tos/administer-copilot/manage-for-enterprise/review-audit-logs)
- GitHub Copilot Product Specific Terms (ownership of suggestions)

### Validation summary

| Domain | Result | Notes |
|---|---|---|
| 1 Responsible use | Answers verified | Keys emphasize human validation, harms, and accountability — aligned to Domain 1 objectives |
| 2 Features | Answers verified | Agent Mode vs Edit Mode, MCP, org policies, audit logs, CLI, instructions/prompt files, Sub-Agents match current GH-300/docs language |
| 3 Data & architecture | Answers verified | Lifecycle, prompt building, filtering/post-processing, LLM limits wording tightened |
| 4 Prompt engineering | Answers verified | Zero-shot/few-shot, context, iteration, prompt files — standard and exam-aligned |
| 5 Productivity | Answers verified | Docs/refactor/tests/security/perf workflows with mandatory human review |
| 6 Privacy & safeguards | Answers corrected | Ownership wording aligned to “GitHub does not claim ownership”; exclusions effects expanded; **Edit/Agent/CLI exclusion limits** added (common exam trap) |

### Corrections applied during validation

1. **Domain 2 Q4** — Clarified Edit Mode vs full autonomous Agent/terminal control.  
2. **Domain 2 Q9** — Removed overclaim that feedback inherently trains/improves public models; tied feedback to product settings/policies.  
3. **Domain 3 Q6** — Tied post-processing to real filters (e.g., public-code matching).  
4. **Domain 6 Q1** — Matched official exclusion effects (no suggestions in excluded files + no informing other suggestions/Chat/code review where supported).  
5. **Domain 6 Q2** — Added documented limitation that IDE may still expose limited semantic info indirectly.  
6. **Domain 6 Q3/Q7** — Used accurate **Block** behavior for suggestions matching public code.  
7. **Domain 6 Q4** — Replaced soft “policy review” wording with Product Terms fact: GitHub does not claim ownership; user remains responsible.  
8. **Domain 6 Q6** — Replaced vague editor-settings item with documented fact that exclusions are **not fully honored** in Edit/Agent modes (and some CLI/agent surfaces).

### Still true for exam prep

- These remain **unofficial** practice items, not Microsoft exam content.  
- UI names (Edits vs Edit Mode, Spark, Spaces) can evolve — prefer concepts over memorizing only one label.  
- Always re-check GitHub Docs for GA/preview differences before sitting the exam.

---

## Important notes

- Bullets under each skill **illustrate** how Microsoft assesses that skill; related topics may appear on the exam.
- Most questions cover **GA** features; **Preview** features may appear if commonly used.
- English exam content updates can land ahead of localized versions.
- Always confirm current domains on the official study guide before scheduling.
- Practice questions in this file are for learning only and are **not** official Microsoft exam content.
