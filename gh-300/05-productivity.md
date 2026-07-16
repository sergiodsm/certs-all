# Domain 5 — Improve Developer Productivity (10–15%)

## Learning goal

Use Copilot across the SDLC **without** confusing “faster drafting” with “done.”

---

## 5.1 Productivity map

| Activity | Copilot helps by… | Human still must… |
|---|---|---|
| Code generation | Drafting functions/modules from intent | Verify correctness & design fit |
| Refactoring | Proposing structural edits | Preserve invariants; run tests |
| Documentation | First-draft JSDoc/XML/Markdown | Fix accuracy & audience |
| Learning codebase | Explaining selected code in place | Confirm against runtime behavior |
| Sample data | Fixtures/demos | Avoid real PII |
| Legacy modernization | Incremental rewrites | Behavior parity checks |
| Unit tests | Drafting cases/assertions | Ensure meaningful edges |
| Integration tests | Scaffolding flows | Boundaries, doubles vs real deps |
| Security | Threat-minded review suggestions | Validate & prioritize fixes |
| Performance | Optimization ideas | Measure; check concurrency |

---

## 5.2 Code generation — professional pattern

1. Specify signature + constraints.  
2. Generate.  
3. Compile/typecheck.  
4. Generate tests.  
5. Ask for edge cases.  
6. Security skim.  
7. Open PR.

### Example prompt

```text
Implement function parseIsoDuration(input: string): Duration in TypeScript.
Rules: no external libs; throw DurationParseError on invalid input;
support PnDTnHnMnS subset only. Export types. Add 6 vitest cases including invalid.
```

---

## 5.3 Refactoring safely

**Unsafe:** “Rewrite the whole module somehow.”  
**Safe:** target structure + invariants + incremental Agent/Edit sessions.

```text
Refactor PaymentService to extract PricingCalculator.
Invariants:
- public method charge() signature unchanged
- existing tests must pass
- no DB schema changes
Do one file at a time; stop after PricingCalculator + updated imports.
```

Legacy modernization = same idea: **small increments, tests, review**.

---

## 5.4 Documentation & learning (reduce context switching)

Ask Chat to explain **selected** unfamiliar functions instead of leaving the IDE. That is the exam’s “reduce context switching” pattern.

Doc prompt:

```text
Generate XML docs for all public methods in this class.
Audience: new team members. Include parameter meanings and thrown exceptions.
Do not invent behavior not present in code — mark unknowns as TODO.
```

---

## 5.5 Sample data (ethical use)

Good: synthetic fixtures for tests/demos.  
Bad: real customer PII, production secrets, live card numbers.

```text
Generate 20 realistic but fake Customer JSON records for US locale.
No real emails of employees. Use example.com domains. Include 2 edge rows: empty phone, very long name.
```

---

## 5.6 Testing workflows

### Unit tests

```text
Given the selected function, write unit tests for:
happy path, null input, empty list, max boundary, and unauthorized user.
Use our existing test style in nearby *.test.ts files.
Assert exceptions by type and message fragment.
```

### Integration tests

Still require humans to decide:

- Real dependency vs test double  
- Environment setup  
- Meaningful assertions (not just “status 200”)

### Edge-case follow-up (exam favorite)

After weak tests: ask explicitly for null/empty/max/auth failure assertions — not “make tests shorter.”

---

## 5.7 Security & performance suggestions

**Security prompt pattern**

```text
Threat-model this handler. Check: injection, authn/authz gaps, secret handling,
SSR F risks, unsafe deserialization, dependency red flags.
Return findings as: severity, location, exploit sketch, fix.
Do not suggest hardcoding credentials.
```

**Performance pattern**

```text
Propose caching for getDashboardStats. Discuss invalidation, stampede risk,
memory bounds, and concurrency. Provide an implementation sketch and how to measure.
```

Next step after any perf suggestion: **validate correctness + measure** — never “ship immediately.”

---

## 5.8 PR lifecycle productivity

Copilot can:

- Summarize PR changes  
- Answer questions about a diff  
- Assist review with customizable standards  

Copilot does **not** (exam distractors):

- Auto-merge to `main` as proof of correctness  
- Replace CI or security sign-off  
- Guarantee the change is behavior-preserving

---

## Mini workflow lab (45 minutes)

Pick a small function in any repo and run this loop:

1. Explain selection in Chat  
2. Generate unit tests + edges  
3. Ask for security review  
4. Ask for a PR summary of your local diff  
5. Write what you rejected and why (Domain 1 crossover)

---

## Domain 5 quick self-test

1. Safest legacy modernization workflow?  
2. How do you improve shallow generated tests?  
3. What must still happen after a caching suggestion?  
4. What PR help is in-bounds vs out-of-bounds for Copilot?
