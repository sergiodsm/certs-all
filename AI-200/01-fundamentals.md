# Azure AI Cloud Developer Associate: Azure SDK Integration & Python Backend Development

This certification is the **AZ-204 replacement** focus for building AI-enabled backend services. This topic is about the “glue code” you write: using Azure SDKs/REST from a Python backend, authenticating securely, validating inputs/outputs, and handling transient failures reliably.

## What you should understand
- How your app calls Azure AI endpoints (HTTP/SDK) and what request/response shapes you should expect.
- How authentication works in cloud-native apps (typically Entra ID + managed identity).
- How to build robust backend behavior: timeouts, retries, idempotency, and safe logging.

## Topics checklist
- [ ] Use Azure SDKs and/or REST to call Azure AI services from a Python backend
- [ ] Authentication patterns (managed identity vs keys; least privilege)
- [ ] Request/response schema handling (validation, serialization, error mapping)
- [ ] Defensive backend behavior (timeouts, retries with backoff, circuit breaker concepts)
- [ ] Safe logging (avoid writing prompts/PII/secrets to logs)
- [ ] Environment separation (dev/test/prod) and configuration management
- [ ] Understand failure modes you must handle (429/5xx/partial failures)
- [ ] Versioning strategy (API/model changes and how your backend stays compatible)

## Exam-style practice (10 questions + answers)
### Question 1
You’re deploying a Python API that calls an Azure AI endpoint. What’s the preferred way to authenticate without storing secrets in code?

**Answer (model):**
Use **Entra ID authentication** with **managed identity** (or another identity-based approach). Grant only the required permissions to the AI resource and acquire tokens at runtime.

### Question 2
In an app, what’s a practical reason to treat “endpoint” and “deployment” as separate concepts?

**Answer (model):**
An **endpoint** is the stable API surface your app calls; a **deployment** is the specific model/config behind it. This separation lets you update models/parameters behind the same endpoint while keeping the app contract stable.

### Question 3
Your backend gets intermittent timeouts when calling a model. What’s the best first improvement?

**Answer (model):**
Add robust backend controls: correct **timeouts**, **retry with exponential backoff** for transient errors, and ensure the app can degrade gracefully (e.g., fallback response or user-friendly error).

### Question 4
Why should you validate/guard the model response shape before using it?

**Answer (model):**
Model outputs can be malformed or partially missing. Validating the response prevents downstream crashes and allows you to trigger a controlled fallback (or a retry) instead of propagating bad data.

### Question 5
What’s a common security mistake when logging AI requests and how do you avoid it?

**Answer (model):**
Mistake: logging raw prompts/inputs/outputs that may contain secrets or PII. Avoid it by **redacting**, **minimizing**, and logging only what you need (and with strict access controls).

### Question 6
Your service receives duplicate requests from a client. How does this affect backend calls to AI endpoints?

**Answer (model):**
You must make calls **idempotent where possible**. Common patterns include request IDs/correlation IDs, deduplication, and storing/returning cached results to prevent repeated side effects or wasted tokens.

### Question 7
You’re building a multi-step AI workflow (retrieve data, then call a model, then write results). What’s the most important backend reliability principle?

**Answer (model):**
Use **clear error boundaries** between steps and handle failures explicitly: timeouts/retries per step, consistent error responses to the caller, and instrumentation so you can debug which step failed.

### Question 8
Your code currently hard-codes the AI service URL and model parameters. What’s better for cloud development lifecycle?

**Answer (model):**
Externalize configuration (environment variables/config service), and keep deployment/model parameters environment-specific. This keeps the app portable across dev/test/prod and reduces risky code changes.

### Question 9
How would you handle HTTP 429 (rate limiting) from an AI endpoint?

**Answer (model):**
Respect backoff guidance: retry with **exponential backoff + jitter**, reduce concurrency, and consider caching. Treat repeated 429 as a signal to scale up/down or reduce workload.

### Question 10
In a Python backend, what’s a good practice for turning provider errors into consistent API responses?

**Answer (model):**
Create a centralized error mapper: map transient errors to retryable responses, map validation issues to 4xx, and include correlation IDs while avoiding sensitive details.

