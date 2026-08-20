# Lab 06 — Key Vault, OpenTelemetry & KQL

**Topics:** [10-key-vault-app-configuration.md](../10-key-vault-app-configuration.md), [11-opentelemetry-kql-troubleshooting.md](../11-opentelemetry-kql-troubleshooting.md)  
**Time:** ~45 minutes

---

## Goal

Fetch a secret with MI, emit a trace span, query failures in Log Analytics with KQL.

---

## 1. Key Vault secret

```bash
az keyvault create -g rg-ai200-lab -n ai200-lab-kv --enable-rbac-authorization true
az keyvault secret set --vault-name ai200-lab-kv -n DemoSecret --value "lab-only-value"
```

Assign **Key Vault Secrets User** to your user or app MI, then:

```python
from azure.identity import DefaultAzureCredential
from azure.keyvault.secrets import SecretClient

client = SecretClient("https://ai200-lab-kv.vault.azure.net/", DefaultAzureCredential())
print(client.get_secret("DemoSecret").value[:3] + "***")
```

---

## 2. OpenTelemetry (minimal)

Add OTLP export to Application Insights connection string / endpoint per [Microsoft docs](https://learn.microsoft.com/en-us/azure/azure-monitor/app/opentelemetry-enable?tabs=python).

Create spans: `rag.request` → `retrieve` → `llm.complete`.

---

## 3. KQL in Log Analytics

Open workspace → Logs:

```kusto
traces
| where timestamp > ago(1h)
| where message contains "correlation_id"
| project timestamp, message, severityLevel
| take 20
```

```kusto
dependencies
| where timestamp > ago(24h)
| summarize avg(duration), p95=percentile(duration, 95) by name
```

---

## 4. App Configuration (optional)

```bash
az appconfig create -g rg-ai200-lab -n ai200-lab-config --sku Free
az appconfig kv set -n ai200-lab-config --key rag:top_k --value 5 --label dev
```

Fetch in Python with `AzureAppConfigurationClient`.

---

## Verify understanding

- [ ] Key Vault vs App Configuration for feature flags
- [ ] Which tables hold traces vs dependency timing
- [ ] Why not log secret values in trace attributes

---

## Exam tie-in

"Triage increased 503 from model dependency" → **KQL on `dependencies`** + distributed trace waterfall.
