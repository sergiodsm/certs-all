# Topic 07 — Container Apps, KEDA & AKS

> **Domain B (20–25%)** — official skill B2  
> **Module:** [`../05-generative-rag.md`](../05-generative-rag.md)  
> **Lab:** [labs/05-container-apps-deploy.md](./labs/05-container-apps-deploy.md)

---

## In one sentence

**Azure Container Apps** runs containers with **revisions** and **KEDA** autoscaling; **AKS** runs Kubernetes workloads from **manifests** — both require logs/events/connectivity checks when AI pipelines fail in production.

---

## Why it exists on the exam

AI workloads burst (queue depth spikes). KEDA scaling on Service Bus queue length is a canonical AI-200 pattern. AKS troubleshooting appears explicitly in the skills outline.

---

## Container Apps

### Environment + app

```bash
az containerapp env create --name ai-env --resource-group rg-ai --location eastus

az containerapp create \
  --name embed-worker \
  --resource-group rg-ai \
  --environment ai-env \
  --image myregistry.azurecr.io/embed-worker:v1 \
  --target-port 8080 \
  --ingress internal \
  --min-replicas 0 \
  --max-replicas 10
```

### Revisions & traffic splitting

```text
  Revision embed-worker--v1  ── 90% traffic
  Revision embed-worker--v2  ── 10% traffic  (canary)
```

```bash
az containerapp revision set-mode --name embed-worker --resource-group rg-ai --mode multiple
az containerapp ingress traffic set --name embed-worker --resource-group rg-ai \
  --revision-weight embed-worker--v1=90 embed-worker--v2=10
```

### KEDA: scale on Service Bus queue

```yaml
# Conceptual scale rule (CLI/portal/Bicep configure KEDA scalers)
# scaler: azure-servicebus
# metadata: queueName=embed-jobs, messageCount=5
# → add replica per N messages
```

**Exam scenario:** Embedding workers idle at 0 replicas; queue fills → KEDA scales out → drains queue → scales to zero.

---

## AKS deployment manifest

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ai-api
spec:
  replicas: 3
  selector:
    matchLabels:
      app: ai-api
  template:
    metadata:
      labels:
        app: ai-api
    spec:
      containers:
        - name: ai-api
          image: myregistry.azurecr.io/ai-api:v1.2.0
          ports:
            - containerPort: 8000
          env:
            - name: APP_CONFIG_ENDPOINT
              value: "https://myappconfig.azconfig.io"
          readinessProbe:
            httpGet:
              path: /health/ready
              port: 8000
            initialDelaySeconds: 10
          livenessProbe:
            httpGet:
              path: /health/live
              port: 8000
---
apiVersion: v1
kind: Service
metadata:
  name: ai-api
spec:
  selector:
    app: ai-api
  ports:
    - port: 80
      targetPort: 8000
```

```bash
kubectl apply -f deployment.yaml
kubectl get pods
kubectl logs deployment/ai-api
kubectl describe pod <pod-name>  # events: ImagePullBackOff, OOMKilled
```

---

## Troubleshooting checklist

| Symptom | Check |
|---------|-------|
| 502 from ingress | Readiness probe failing; app not listening on `target-port` |
| CrashLoopBackOff | Logs: missing env, auth to Cosmos failed |
| Slow AI responses | HPA/KEDA max replicas; downstream model 429 |
| Intermittent timeouts | DNS, private endpoint, NSG egress |

```bash
# Container Apps
az containerapp logs show --name embed-worker --resource-group rg-ai --follow

# AKS connectivity
kubectl exec -it <pod> -- curl -v https://<cosmos>.documents.azure.com
```

---

## When to use / avoid

| Container Apps | AKS |
|----------------|-----|
| Serverless containers, KEDA, minimal ops | Full K8s control, custom CRDs |
| Internal workers + HTTP APIs | Large multi-team platform |
| Scale to zero | Long-running stateful sets at scale |

---

## ⚠️ Exam traps

1. **CPU-based autoscale only** for queue workers — use **KEDA** on queue depth.
2. **No readiness probe** — traffic hits starting containers.
3. **Internal ingress** misunderstood — worker not reachable from wrong VNet.
4. **kubectl apply** without manifest knowledge — exam may show YAML errors.

---

## Checkpoint questions

**Q1.** Embed queue depth drives load; cost when idle matters. Service?  
<details><summary>Answer</summary>Container Apps + KEDA (scale to zero on Service Bus).</details>

**Q2.** Canary new embedding worker revision. Container Apps feature?  
<details><summary>Answer</summary>Multiple revisions + traffic weighting.</details>

**Q3.** Pod ImagePullBackOff. First command?  
<details><summary>Answer</summary>`kubectl describe pod` — events show auth/tag/registry errors.</details>

---

## Skills checklist (official B2)

- [ ] Container Apps: env config, revisions
- [ ] KEDA event-driven scaling
- [ ] AKS deploy/manage via manifests
- [ ] Monitor/troubleshoot logs, events, connectivity

---

## Next topic

[08 — Service Bus & Event Grid](./08-service-bus-event-grid.md)
