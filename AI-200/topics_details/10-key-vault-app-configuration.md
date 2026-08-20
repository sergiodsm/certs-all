# Topic 10 — Key Vault & App Configuration

> **Domain D (20–25%)** — official skill D1  
> **Module:** [`../06-evaluation-responsible-deployment.md`](../06-evaluation-responsible-deployment.md)  
> **Lab:** [labs/06-keyvault-telemetry-kql.md](./labs/06-keyvault-telemetry-kql.md)

---

## In one sentence

**Azure Key Vault** stores and **rotates secrets**; **Azure App Configuration** centralizes non-secret settings and feature flags — both accessed at runtime via **managed identity**, not baked into container images.

---

## Why it exists on the exam

Security is 20–25% of AI-200. Secret handling and centralized config appear in almost every deployment scenario.

---

## Key Vault

### Store & retrieve secret (Python)

```python
from azure.identity import DefaultAzureCredential
from azure.keyvault.secrets import SecretClient

credential = DefaultAzureCredential()
client = SecretClient(vault_url="https://myvault.vault.azure.net/", credential=credential)

db_password = client.get_secret("postgres-admin-password").value
```

### Rotation (exam concept)

```text
  Admin sets rotation policy on secret
        │
        ▼
  Key Vault generates new version
        │
        ▼
  Event Grid notification → Function updates dependent service / restarts app
        │
        ▼
  Apps fetch "latest" version via URI or SDK
```

**Exam point:** Rotation without rebuilding images — apps read current version at startup or on refresh.

### RBAC on vault

Grant app MI role **Key Vault Secrets User** — not Owner on subscription.

---

## App Configuration

```python
from azure.appconfiguration import AzureAppConfigurationClient
from azure.identity import DefaultAzureCredential

client = AzureAppConfigurationClient(
    base_url="https://myappconfig.azconfig.io",
    credential=DefaultAzureCredential(),
)

for setting in client.list_configuration_settings(label_filter="production"):
    if setting.key == "rag:max_chunks":
        max_chunks = int(setting.value)
```

### Labels & environments

| Key | Label | Value |
|-----|-------|-------|
| `model:deployment` | `dev` | `gpt-4o-mini-dev` |
| `model:deployment` | `prod` | `gpt-4o-prod` |

### Feature flags

```python
# SDK feature flag evaluation
if client.get_configuration_setting(key=".appconfig.featureflag/beta-rag").enabled:
    use_hybrid_search = True
```

Refresh without redeploy: poll App Configuration or use **sentinel key** refresh pattern.

---

## Key Vault vs App Configuration

| Store | Content |
|-------|---------|
| **Key Vault** | Passwords, API keys, certs, connection strings |
| **App Configuration** | Feature flags, model names, chunk sizes, endpoints (non-secret) |

**Pattern:** App Configuration value references Key Vault secret for sensitive parts.

---

## App Service / Container Apps integration

```bash
# Key Vault reference in App Service setting
az webapp config appsettings set --name ai-api --resource-group rg-ai \
  --settings POSTGRES_PASSWORD="@Microsoft.KeyVault(SecretUri=https://myvault.vault.azure.net/secrets/postgres-password/)"
```

---

## ⚠️ Exam traps

1. **Secrets in App Configuration as plain text** when they should be in Key Vault.
2. **No rotation plan** — manual redeploy only.
3. **Over-privileged MI** on Key Vault (Contributor vs Secrets User).
4. **Hard-coded model deployment name** in code vs App Configuration per env.

---

## Checkpoint questions

**Q1.** Rotate Postgres password without new container image?  
<details><summary>Answer</summary>Key Vault new secret version + app reload/MI fetch/reference update.</details>

**Q2.** Toggle hybrid search in prod without redeploy?  
<details><summary>Answer</summary>App Configuration feature flag.</details>

**Q3.** Where store OpenAI API key?  
<details><summary>Answer</summary>Key Vault — not repo, not Dockerfile.</details>

---

## Skills checklist (official D1)

- [ ] Key Vault: store, retrieve, rotate secrets
- [ ] App Configuration: settings and retrieval

---

## Next topic

[11 — OpenTelemetry & KQL troubleshooting](./11-opentelemetry-kql-troubleshooting.md)
