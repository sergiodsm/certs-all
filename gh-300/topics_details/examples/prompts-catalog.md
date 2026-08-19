# Prompt Catalog — Exam & Workplace Patterns

Copy, adapt, and practice. Each pattern maps to Domains 4–5 (and often 1).

---

## 1. Zero-shot implementation

```text
Implement function slugify(input: string): string in TypeScript.
Rules: lowercase; non-alphanumerics to single hyphens; trim hyphens; Unicode letters allowed via normalization.
No dependencies. Include JSDoc. Do not write tests yet.
```

---

## 2. Few-shot style matching

```text
Convert REST errors to ProblemDetails using this style:

Example input: NotFoundError("Order 12")
Example output:
{
  "type": "https://api.example.com/problems/not-found",
  "title": "Not Found",
  "status": 404,
  "detail": "Order 12"
}

Now convert: ValidationError(["email invalid", "age < 18"])
```

---

## 3. Refactor with invariants

```text
Extract pricing logic from CheckoutService into PricingCalculator.
Invariants: charge() signature unchanged; existing tests pass; no schema changes.
Touch only src/checkout/**. Summarize risk before editing.
```

---

## 4. Edge-case test expansion

```text
Improve the selected test file.
Add cases: null input, empty array, max int boundary, unauthorized user, duplicate id.
Assert thrown error types. Keep existing happy-path tests.
```

---

## 5. Integration test scaffold

```text
Draft an integration test for POST /api/orders.
Use the test server helper already in repo.
Mock payment gateway; use real validation layer.
Assert 201 body shape and 400 validation errors.
Do not hit production services.
```

---

## 6. Security review

```text
Threat-model the selected handler.
Return severity | issue | location | exploit sketch | fix.
Cover injection, authz, secret leakage in logs, SSRF, mass assignment.
Do not suggest hardcoding credentials or disabling TLS.
```

---

## 7. Performance proposal

```text
Propose a cache for getDashboardStats(userId).
Discuss TTL, invalidation, stampede, memory bounds, personalization risks.
Provide implementation sketch and a measurement plan.
Do not claim speedup without metrics.
```

---

## 8. Documentation without invention

```text
Generate Markdown docs for the public API of this module.
Only document behavior present in code.
Mark unknowns as TODO(UNKNOWN). Include examples that compile.
```

---

## 9. Legacy modernization (incremental)

```text
Modernize selected CommonJS module to ESM TypeScript.
Step 1 only: add types without behavior changes.
Do not rename exports. List follow-up steps but do not implement them yet.
```

---

## 10. Synthetic sample data

```text
Generate 15 fake Customer records as JSON.
Locale: en-US. Emails @example.com. Include edges: missing phone, 80-char name, unicode street.
No real employee or customer data.
```

---

## 11. Agent Mode with negative constraints

```text
GOAL: Add zod validation to POST /api/users
ALLOW: edit src/api/users/** ; run npm test -- users
DENY: package.json dependency changes; migrations; git commit/push
STOP: after two failing test cycles; summarize blockers
```

---

## 12. Plan-only

```text
Plan a migration from moment to luxon in this repo.
Do not modify files.
List file groups, risk ranking, and a rollback strategy.
```

---

## 13. Explain-in-place (reduce context switching)

```text
Explain the selected function for a new teammate.
Cover inputs, outputs, side effects, and failure modes.
Point to related callers if visible in context.
```

---

## 14. PR summary helper

```text
Summarize this diff for a PR description:
- Why
- What changed
- Risk / rollback
- Test plan
Keep under 150 words. No marketing language.
```

---

## 15. Inclusive / fairness language pass

```text
Review the selected user-facing copy and code comments for biased or exclusionary language.
Suggest inclusive alternatives. Do not change program logic.
```

---

## Anti-patterns (don’t practice these)

```text
Fix it
Make it better and secure and fast and perfect
Here’s prod DB password for context: ...
Rewrite the entire monorepo
```
