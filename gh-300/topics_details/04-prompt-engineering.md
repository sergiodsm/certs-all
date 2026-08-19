# Domain 4 — Prompt Engineering & Context Crafting (10–15%)

## Professor framing

Prompt engineering on GH-300 is **applied**. You will not be asked to recite a textbook definition in isolation — you will pick the prompt strategy that fits a developer scenario.

---

## 4.1 The 4S framework (exam-friendly)

| S | Meaning | Failure if ignored |
|---|---|---|
| **Single** | One primary task per prompt | Mixed quality, partial answers |
| **Specific** | Language, API, constraints, I/O | Vague “fix it” output |
| **Short** | Enough detail, no novel | Diluted attention / noise |
| **Surrounded** | Context: files, examples, errors, history | Off-topic or generic code |

**Most under-estimated on exam:** Specificity. Poor suggestions are usually blamed on insufficient specificity before exotic causes.

---

## 4.2 Prompt structure template

```text
ROLE / CONTEXT (optional): You are helping in a <stack> codebase.
GOAL: <one clear outcome>
CONSTRAINTS: <must / must-not>
INPUTS: <types, signatures, error logs>
OUTPUT: <format: code only / diff / steps / tests>
EXAMPLES (optional few-shot): <1–3 samples>
SUCCESS CRITERIA: <how we know it’s done>
```

### Weak vs strong

**Weak**

```text
Fix the payment thing.
```

**Strong**

```text
Write a C# method ValidatePayment(PaymentRequest request) that:
- rejects null request
- allows currencies: USD, EUR, GBP only
- returns ValidationResult with error codes
Include XML docs and two usage examples.
Do not call external services.
```

---

## 4.3 How context is determined

Context commonly includes:

- Current selection / open files  
- Chat history (prior turns)  
- Explicit attachments / `#file` style references (product UI varies)  
- Instructions / prompt files  
- Repository customization files when configured  

Context is **not** magic omniscience. If the model lacks a file, attach it or summarize the contract.

### Debugging bad Chat answers

| Symptom | Likely missing context | Fix |
|---|---|---|
| Wrong framework | No stack stated; wrong files open | State stack; attach canonical module |
| Ignores team style | No examples / instructions | Few-shot or instructions file |
| Invents API | No types/docs attached | Attach interface + “do not invent” |
| Off-topic | Bloated history | New thread; restate single goal |

---

## 4.4 Zero-shot vs few-shot

| Style | Definition | Best when |
|---|---|---|
| **Zero-shot** | Task instruction **without** worked examples | Straightforward, well-known patterns |
| **Few-shot** | One or more input→output examples | Non-obvious format, consistency, style matching |

### Few-shot example

```text
Convert DTOs to Zod schemas using this style:

Example:
Input: type User = { id: string; email: string }
Output:
export const UserSchema = z.object({
  id: z.string().uuid(),
  email: z.string().email(),
});

Now convert:
type Invoice = { id: string; totalCents: number; status: "open" | "paid" }
```

---

## 4.5 Prompt process flow & chat history

Typical Chat flow:

```text
Turn 1: goal + constraints
Turn 2: refine with error message / failing test
Turn 3: ask for tests / edge cases
Turn 4: ask for security review of the draft
```

History helps you **avoid restating everything** — but long noisy history can also drag quality down. Starting a clean thread is a professional move.

---

## 4.6 Best practices checklist

1. Name the language/runtime/framework versions when relevant.  
2. State invariants (“do not change public API”).  
3. Provide failing test or stack trace when debugging.  
4. Ask for edge cases explicitly.  
5. Forbid secrets and invented dependencies.  
6. Iterate — first answer is a draft.  
7. Encode durable rules in **instructions / prompt files**, not only one-off Chat.

---

## 4.7 Prompt files vs instructions files

| Artifact | Role |
|---|---|
| **Instructions** | Always-on (or scoped) project/team norms |
| **Prompt files** | Reusable prompt packs for recurring tasks (e.g., “write migration,” “threat model this handler”) |

Both improve **consistency** across people/sessions. Neither eliminates hallucinations.

Hands-on: **[labs/06-instructions-prompts.md](./labs/06-instructions-prompts.md)**  
Catalog: **[examples/prompts-catalog.md](./examples/prompts-catalog.md)**

---

## Domain 4 quick self-test

1. Rewrite “make this better” into a 4S prompt.  
2. When is few-shot better than zero-shot?  
3. List four context sources Chat may use.  
4. Why do prompt files help teams?
