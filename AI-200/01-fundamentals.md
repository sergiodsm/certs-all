# Azure AI Cloud Developer Associate: Fundamentals

## Topics checklist
- [ ] What Azure AI Studio / Azure AI Foundry is and where you create/manage AI projects
- [ ] Core solution components (models, deployments, endpoints, orchestration, evaluation)
- [ ] Authentication & authorization concepts (Entra ID, managed identity vs keys)
- [ ] Calling AI endpoints from your app (REST/SDK) and handling request/response payloads
- [ ] Security basics (least privilege, secrets management patterns)
- [ ] Resource organization (resource groups/regions) and environment separation (dev/test/prod)

## Exam-style practice (with answers)
### Question 1
You’re building a backend service that calls an Azure AI model endpoint. You want to avoid embedding secrets in code. What’s the preferred approach for a cloud-developer setup?

**Answer (model):**
Use **Entra ID authentication** with **managed identity** (or another identity-based method) and grant the minimum required permissions to the AI resources. In your app, prefer acquiring tokens at runtime rather than hard-coding keys. Only use keys/secrets if the service requires it, and store them in a secure secret store.

### Question 2
In Azure AI solutions, what’s the practical difference between a **model deployment** and an **endpoint** (from the perspective of an app developer)?

**Answer (model):**
A **deployment** is the “running” instance/configuration of a specific model (and settings like deployment parameters). An **endpoint** is the address/contract clients call (the API surface) that routes requests to the appropriate deployment(s).

