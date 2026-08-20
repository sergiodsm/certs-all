# Lab 05 — ACR Build & Container Apps + KEDA

**Topics:** [06-acr-app-service-containers.md](../06-acr-app-service-containers.md), [07-container-apps-keda-aks.md](../07-container-apps-keda-aks.md)  
**Time:** ~60 minutes

---

## Goal

Build an image with ACR Tasks, deploy to Container Apps, configure KEDA scale rule on a Service Bus queue.

---

## 1. ACR build (no local Docker)

```bash
az acr create --resource-group rg-ai200-lab --name ai200labacr --sku Basic
az acr build --registry ai200labacr --image embed-worker:v1 --file Dockerfile .
```

---

## 2. Container Apps environment

```bash
az containerapp env create -n ai200-env -g rg-ai200-lab -l eastus

az containerapp create -n embed-worker -g rg-ai200-lab \
  --environment ai200-env \
  --image ai200labacr.azurecr.io/embed-worker:v1 \
  --ingress internal \
  --min-replicas 0 --max-replicas 5 \
  --registry-server ai200labacr.azurecr.io
```

---

## 3. KEDA scale rule (portal or CLI)

Configure scaler:

- **Type:** Azure Service Bus Queue
- **Queue:** `embed-jobs`
- **Message count threshold:** 5 messages → 1 replica (adjust per lab)

---

## 4. Revision canary

Deploy `v2` as new revision; split 10% traffic; check logs; shift to 100%.

```bash
az containerapp logs show -n embed-worker -g rg-ai200-lab --follow
```

---

## Verify understanding

- [ ] Why `min-replicas 0` saves cost for batch embed workers
- [ ] Readiness vs liveness for worker that pulls from queue
- [ ] Internal ingress meaning for worker-only apps

---

## Exam tie-in

"Scale embedding workers based on queue depth" → **Container Apps + KEDA**, not CPU autoscale alone.
