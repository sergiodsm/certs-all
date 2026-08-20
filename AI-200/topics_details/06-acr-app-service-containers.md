# Topic 06 — ACR & App Service Container Hosting

> **Domain B (20–25%)** — official skill B1  
> **Module:** [`../05-generative-rag.md`](../05-generative-rag.md)  
> **Lab:** [labs/05-container-apps-deploy.md](./labs/05-container-apps-deploy.md)

---

## In one sentence

Build images with **Docker**, store/version them in **Azure Container Registry (ACR)**, optionally build via **ACR Tasks**, and run on **Azure App Service** with environment variables and secrets injected at runtime — never baked into the image.

---

## Why it exists on the exam

AI backends ship as containers. AI-200 tests ACR lifecycle, automated builds, and App Service configuration patterns from the official B1 bullets.

---

## How it works in Azure

### Minimal Dockerfile (Python AI API)

```dockerfile
FROM python:3.12-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
ENV PORT=8000
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

### Push to ACR

```bash
az acr login --name myregistry
docker tag ai-api:latest myregistry.azurecr.io/ai-api:v1.2.0
docker push myregistry.azurecr.io/ai-api:v1.2.0
```

### ACR Tasks (cloud build)

```bash
az acr build --registry myregistry \
  --image ai-api:v1.2.0 \
  --file Dockerfile .
```

**Exam point:** CI builds in Azure without local Docker — reproducible, integrated with RBAC.

### App Service: deploy container

```bash
az webapp create --resource-group rg-ai --plan plan-linux \
  --name ai-api-prod --deployment-container-image-name myregistry.azurecr.io/ai-api:v1.2.0

az webapp config appsettings set --name ai-api-prod --resource-group rg-ai \
  --settings COSMOS_DATABASE=ai-db APP_CONFIG_ENDPOINT=https://myappconfig.azconfig.io
```

### Secrets on App Service

| Method | Exam preference |
|--------|-----------------|
| Key Vault references | `@Microsoft.KeyVault(SecretUri=...)` in app settings |
| Managed identity + Key Vault SDK | No secret in portal at all |
| Plain text in app settings | ⚠️ Avoid for production |

```bash
# Enable system MI
az webapp identity assign --name ai-api-prod --resource-group rg-ai

# Grant Key Vault Secrets User to MI
```

---

## Image versioning strategy

```text
  v1.1.0 ──► production slot
  v1.2.0-rc ──► staging slot ──► swap after validation
```

- **Immutable tags** (`v1.2.0`) — not `:latest` in production.
- Rollback = redeploy previous tag.

---

## When to use / avoid

| App Service containers | Container Apps / AKS |
|------------------------|----------------------|
| Simple web API, familiar PaaS | KEDA scale-to-zero, event-driven |
| Quick migration from App Service | Complex microservices on K8s |
| Built-in deployment slots | Fine-grained K8s networking |

---

## ⚠️ Exam traps

1. **Secrets in Dockerfile ENV** — visible in image layers.
2. **`:latest` only** — can't rollback reliably.
3. **No MI on App Service** — using connection strings everywhere.
4. **Forgetting ACR Tasks** when question asks "build without local Docker."

---

## Checkpoint questions

**Q1.** Build container in CI without local Docker daemon?  
<details><summary>Answer</summary>ACR Tasks (`az acr build`).</details>

**Q2.** Rotate DB password without rebuilding image?  
<details><summary>Answer</summary>Key Vault reference or runtime fetch via MI — config outside image.</details>

**Q3.** Safe rollout of new API version?  
<details><summary>Answer</summary>Staging slot / new tag → validate → swap traffic.</details>

---

## Skills checklist (official B1)

- [ ] ACR: build, store, version, manage images
- [ ] ACR Tasks
- [ ] App Service deploy + env vars + secrets

---

## Next topic

[07 — Container Apps, KEDA & AKS](./07-container-apps-keda-aks.md)
