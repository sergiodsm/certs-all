# Azure AI Cloud Developer Associate: Containerized Solutions on Azure (Deploy & Scale)

This topic is where AZ-204 expertise strongly applies: you must deploy AI-enabled backends as containerized apps, manage environments, scale, and operate safely. The goal is to make your AI service reliable under load and easy to troubleshoot.

## What you should understand
- How to package your Python backend as a container.
- How to configure settings/secrets via environment and identity (not baked-in code).
- How to scale and operate using health checks and observability.

## Topics checklist
- [ ] Dockerize your Python AI backend (dependencies, build, runtime)
- [ ] Store secrets/config outside the image (managed identity, env/config services)
- [ ] Use health checks (readiness/liveness) so traffic only hits healthy instances
- [ ] Configure networking safely (inbound rules, private access patterns when needed)
- [ ] Scale out/in based on workload (autoscaling concepts)
- [ ] Version deployments (immutable images; rollout/rollback strategy)
- [ ] Ensure your container supports graceful shutdown (finish in-flight requests)
- [ ] Instrument logs/metrics/traces for operations
- [ ] Handle startup dependencies (AI endpoint reachability, token acquisition)
- [ ] Cost awareness (scale-to-demand, avoid busy-waiting and excessive concurrency)

## Exam-style practice (10 questions + answers)
### Question 1
Why should you avoid hard-coding secrets into a container image?

**Answer (model):**
Because images are widely distributed and may be stored longer than needed. Put secrets/config outside the image (managed identity/env/config) to reduce exposure.

### Question 2
What’s the purpose of a readiness probe in a containerized app?

**Answer (model):**
Readiness indicates when the app is able to serve traffic. It prevents routing requests to instances that aren’t fully initialized.

### Question 3
Your app needs a model endpoint available at startup. What’s a safe approach?

**Answer (model):**
Fail fast with clear errors (or degrade gracefully) and rely on readiness probes + retries/backoff in startup logic so the system self-recovers rather than serving broken behavior.

### Question 4
How can you safely roll out an updated model integration without breaking clients?

**Answer (model):**
Use an immutable deployment strategy and keep the external API contract stable. Version internal model/deployment behavior behind the same endpoint, and run validation before full rollout.

### Question 5
Why does graceful shutdown matter for AI backends?

**Answer (model):**
To avoid dropping in-flight requests (which can cause user-facing failures and inconsistent outputs). Graceful shutdown lets the app complete work or fail cleanly.

### Question 6
Your AI endpoint rate limits you during traffic spikes. What container-level approaches help?

**Answer (model):**
Reduce request fan-out by limiting concurrency, implement backpressure at the API layer, and scale based on queue/workload rather than raw inbound traffic.

### Question 7
How do you enable managed identity-style auth for a containerized workload?

**Answer (model):**
Bind the app/container identity to the platform-managed identity and request tokens at runtime using the environment-provided credentials (rather than storing static keys in the image).

### Question 8
What’s a practical strategy for debugging production issues in containers?

**Answer (model):**
Use structured logs plus distributed tracing/telemetry. Correlation IDs and request IDs help you connect failures to specific model calls and downstream dependencies.

### Question 9
Why is configuration via environment variables preferred for dev/test/prod?

**Answer (model):**
Because you can deploy the same image to different environments and only change runtime configuration, reducing risky code changes.

### Question 10
How do you keep costs under control when running containerized AI services?

**Answer (model):**
Right-size and autoscale, avoid unnecessary parallelism, use caching where appropriate, and ensure failed/retried requests don’t create runaway compute usage.

