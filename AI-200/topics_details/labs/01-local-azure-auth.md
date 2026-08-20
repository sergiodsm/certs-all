# Lab 01 — Local Azure Auth (DefaultAzureCredential)

**Topics:** [01-foundation-sdk-python.md](../01-foundation-sdk-python.md)  
**Time:** ~30 minutes  
**Prerequisites:** Azure subscription, `az` CLI, Python 3.11+

---

## Goal

Run Python locally against Azure using the same auth pattern you'll use in Container Apps/Functions: **no keys in code**.

---

## Steps

### 1. Login and verify identity

```bash
az login
az account show --query "{name:name, id:id, user:user.name}"
```

### 2. Create a resource group (optional sandbox)

```bash
az group create --name rg-ai200-lab --location eastus
```

### 3. Install packages

```bash
python -m venv .venv
# Windows: .venv\Scripts\activate
pip install azure-identity azure-cosmos
```

### 4. Test credential acquisition

```python
# lab01_credential.py
from azure.identity import DefaultAzureCredential

credential = DefaultAzureCredential()
token = credential.get_token("https://management.azure.com/.default")
print("Token acquired, expires:", token.expires_on)
```

Run: `python lab01_credential.py` — should succeed after `az login`.

### 5. (Optional) Assign RBAC on Cosmos DB

If you have a Cosmos account:

```bash
# Get your user's object id
USER_OID=$(az ad signed-in-user show --query id -o tsv)
COSMOS_ID=$(az cosmosdb show -g rg-ai200-lab -n mycosmos --query id -o tsv)
az role assignment create --assignee $USER_OID --role "Cosmos DB Built-in Data Reader" --scope $COSMOS_ID
```

```python
from azure.identity import DefaultAzureCredential
from azure.cosmos import CosmosClient

client = CosmosClient("https://<account>.documents.azure.com:443/", credential=DefaultAzureCredential())
print(list(client.list_databases()))
```

---

## Verify understanding

- [ ] Explain what `DefaultAzureCredential` tries locally vs in Azure
- [ ] Why not embed the Cosmos primary key in `.env` committed to git?
- [ ] Which role is least privilege for read-only queries?

---

## Cleanup

```bash
az group delete --name rg-ai200-lab --yes --no-wait
```
