# Microsoft Certified: Azure AI Cloud Developer Associate (AI-200)

Instructor summary for **Exam AI-200: Developing AI Cloud Solutions on Azure**.  
Use this file as the single study brief for Cursor sessions (`@AI-200/README_CURSOR.md`).

| Item | Detail |
|------|--------|
| Credential | [Microsoft Certified: Azure AI Cloud Developer Associate](https://learn.microsoft.com/en-us/credentials/certifications/azure-ai-cloud-developer-associate/?practice-assessment-type=certification) |
| Exam | AI-200 — Developing AI Cloud Solutions on Azure |
| Level | Intermediate · Role: Developer · Subjects: Application development, Artificial intelligence |
| Duration | 120 minutes (proctored; may include interactive items) |
| Passing score | **700 / 1000** |
| Language | English |
| Skills measured | As of **April 15, 2026** — [official study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200) |
| Practice assessment | Not currently available; use the [exam sandbox](https://aka.ms/examdemo) |
| Study guide short link | [aka.ms/AI200-StudyGuide](https://aka.ms/AI200-StudyGuide) |

> **Instructor note:** These practice questions are **study aids**, not leaked exam content. Each answer is tied to an official Microsoft Learn skill bullet and documentation page. Prefer **GA** features; Preview is labeled when relevant.

---

## 1. Certification overview (why this exam exists)

This certification validates that you can **design, build, and implement AI solutions on Azure**, with emphasis on:

- **Back-end services** (not notebooks or UI-only work)
- **Scalable architectures** (containers, messaging, serverless)
- The **full development lifecycle**: requirements → design → development → deployment → security → monitoring

You are expected to ship AI-enabled backends that store embeddings, retrieve for RAG, process work asynchronously, run in containers, and operate securely with observable telemetry.

---

## 2. Summary of skills required

### Audience proficiency (official)

You should be proficient in:

| Skill area | What “proficient” means on this exam |
|------------|--------------------------------------|
| **Azure SDKs / third-party SDKs on Azure** | Call services from **Python** with official clients; auth, retries, errors |
| **Azure data management services** | Cosmos DB for NoSQL, Azure Database for PostgreSQL, Azure Managed Redis |
| **Vector databases** | Store embeddings; run similarity search; support RAG with filters |
| **Messaging and eventing** | Service Bus queues/topics/DLQ; Event Grid filters, custom events, retries |
| **Containerized apps on Azure** | ACR, ACR Tasks, App Service containers, Container Apps, KEDA, AKS manifests |
| **Azure Functions** | Triggers, bindings, deploy serverless APIs for AI pipelines |
| **Security** | Key Vault (store/retrieve/rotate); App Configuration |
| **Monitoring & troubleshooting** | OpenTelemetry tracing; **KQL** for logs/metrics |

### Skills at a glance (exam weights)

| Weight | Domain (topic for practice sets below) |
|--------|----------------------------------------|
| **25–30%** | Develop AI solutions by using Azure data management services |
| **20–25%** | Develop containerized solutions on Azure |
| **20–25%** | Connect to and consume Azure services |
| **20–25%** | Secure, monitor, troubleshoot Azure solutions |

### Cross-cutting expectations (every domain)

- Authenticate with **Microsoft Entra ID / managed identity** (least privilege; avoid keys in code/images)
- Handle **timeouts, retries, idempotency**, and safe logging (no secrets/PII in logs)
- Prefer **Python + Azure SDK** patterns for backend reliability

---

## 3. Summary of topics required

Mapped 1:1 from the [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200).

### Topic A — Develop AI solutions by using Azure data management services (25–30%)

#### A1. Azure Cosmos DB for NoSQL

- Connect with the SDK and run queries
- Optimize **RUs** via indexing policies and consistency levels
- Store/retrieve embeddings; run **vector similarity search**
- Implement a **change feed processor** for inserts/updates (and deletes when using the appropriate mode)

#### A2. Azure Database for PostgreSQL

- Connect and query with SDKs
- Schema design, data types, indexing
- Reduce **pgvector** compute overhead; size compute/memory/storage for vectors
- Vector similarity search + **RAG** with **metadata filters**
- Connection optimization (pooling, throughput, latency)

#### A3. Azure Managed Redis

- Caching, expiration, invalidation
- **Vector indexing** for similarity search (not “cache only”)

### Topic B — Develop containerized solutions on Azure (20–25%)

#### B1. Container application hosting

- Build, store, version, manage images with **Azure Container Registry (ACR)**
- Build/run with **ACR Tasks**
- Deploy containers to **Azure App Service** (env vars and secrets)

#### B2. Container-orchestrated solutions

- **Azure Container Apps**: environment config, **revision** management
- Event-driven scaling with **KEDA**
- **AKS** deploy/manage via **manifest files**
- Troubleshoot via logs, events, end-to-end connectivity

### Topic C — Connect to and consume Azure services (20–25%)

#### C1. Event- and message-based AI solutions

- **Service Bus**: queues, topics/subscriptions, **dead-letter** handling
- **Event Grid**: filters, custom events, retries

#### C2. Azure Functions

- Serverless APIs with **triggers** and **bindings**
- Configure and deploy function apps

### Topic D — Secure, monitor, and troubleshoot Azure solutions (20–25%)

#### D1. Secure solutions

- **Key Vault**: secrets store, retrieve, **rotation**
- **App Configuration**: store/retrieve app settings (non-secrets; Key Vault references pattern)

#### D2. Monitor and troubleshoot

- Distributed tracing with **OpenTelemetry** SDKs
- **KQL** queries for logs and metrics

---

## 4. How to study with this file

1. Read sections **2–3** once (skills + topics map).
2. Drill **one topic** at a time (10 MCQs). Cover answers until you attempt.
3. For each miss: read the **Official source** link, then re-answer from memory.
4. Target **≥ 8/10** per topic before scheduling.
5. Optional deeper material in this folder: [`AI-200-topics.md`](./AI-200-topics.md), [`AI-200-INSTRUCTOR.md`](./AI-200-INSTRUCTOR.md), [`topics_details/`](./topics_details/).

---

## 5. Exam-style practice questions (10 per topic)

Format: single best answer unless noted.  
**Answers + validation sources** are in [Section 6](#6-answer-key-with-official-source-validation).

---

### Topic A — Azure data management for AI (10 questions)

**A1.** You need to keep a RAG index in sync when documents in Cosmos DB for NoSQL are inserted or updated. Which approach matches the skills measured for this exam?

- A) Nightly full table export to Blob, then rebuild the index
- B) Implement a **change feed processor** that detects new/updated items and re-embeds/reindexes them
- C) Poll the container with `SELECT *` every second using Session consistency
- D) Enable automatic geo-replication and rely on the secondary region as the index

**A2.** Vector queries on Cosmos DB for NoSQL are consuming excessive RUs. Which levers does the study guide explicitly call out for query/RU optimization?

- A) Only increasing provisioned RUs indefinitely
- B) **Indexing policies** and **consistency levels**
- C) Disabling partitioning and scanning all items
- D) Switching exclusively to Strong consistency for all reads

**A3.** You store embeddings in Cosmos DB and must run semantic retrieval. What capability must you use?

- A) Only SQL `ORDER BY _ts DESC`
- B) **Vector similarity search** over stored embeddings
- C) Change feed alone without storing vectors
- D) Mirror every document to Azure Queue Storage

**A4.** For Azure Database for PostgreSQL RAG, the study guide expects you to implement retrieval with which pattern?

- A) Full-table scan of `BYTEA` blobs with no filters
- B) Vector similarity search plus **metadata filters** for RAG
- C) Storing embeddings only in client memory
- D) Using PostgreSQL solely as a password store

**A5.** Your pgvector queries are slow and CPU-heavy. Which study-guide actions apply?

- A) Ignore indexes and add more client retries
- B) Implement indexing strategies, reduce pgvector compute overhead, and configure compute/memory/storage for vector workloads
- C) Disable the `vector` extension and use `TEXT` columns
- D) Move all vectors into environment variables

**A6.** You need low-latency similarity search for a hot, frequently accessed embedding set, and the exam skills mention Redis specifically. What should you implement on Azure Managed Redis?

- A) Only string `GET`/`SET` without indexes
- B) **Vector indexing** to enable similarity search (in addition to cache patterns)
- C) Pub/Sub only
- D) AOF persistence as a substitute for vector search

**A7.** Which Redis data operations are explicitly listed for AI solutions in the skills outline?

- A) Only LUA scripting for blockchain
- B) Caching, **expiration**, and **invalidation**
- C) Replacing Cosmos DB as the sole durable system of record for all documents
- D) Hosting Docker images inside Redis

**A8.** Multi-tenant RAG on PostgreSQL must never leak another tenant’s chunks. What is the correct retrieval design?

- A) Filter only in the LLM prompt after retrieving all tenants
- B) Apply a **tenant/metadata filter** in the vector query every time
- C) Use Session consistency on Redis instead of filters
- D) Store all tenants in one embedding with no IDs

**A9.** Cosmos DB consistency levels affect latency, availability, and RU cost. Which statement is consistent with official Cosmos DB consistency documentation used for exam reasoning?

- A) All five consistency levels have identical latency and RU cost
- B) Stronger consistency generally increases latency/cost tradeoffs vs weaker levels; choose based on correctness needs
- C) Eventual consistency always guarantees linearizability
- D) Consistency levels only apply to change feed, not queries

**A10.** You connect to Cosmos DB for NoSQL from Python. What does the skills outline expect?

- A) Only REST calls written by hand with no SDK
- B) Connect using the **SDK** and run queries
- C) Only the portal Data Explorer for production workloads
- D) JDBC drivers exclusively

---

### Topic B — Containerized solutions on Azure (10 questions)

**B1.** Your CI pipeline has no local Docker daemon. How do you build and push an image into ACR in Azure?

- A) Email the Dockerfile to support
- B) Use **ACR Tasks** (for example `az acr build`) to build in the cloud and store the image in ACR
- C) Run containers only on the developer laptop forever
- D) Store source code in Key Vault instead of images

**B2.** Skills measured include versioning and managing container images. Which service is the primary registry?

- A) Azure Batch
- B) **Azure Container Registry (ACR)**
- C) Azure Front Door
- D) Azure DNS

**B3.** You deploy a containerized AI API to Azure App Service. What must you configure according to the skills outline?

- A) Only NSG rules on the container host VM you manage
- B) App Service supplying **environment variables and secrets** to the container
- C) Manual SSH into every instance to edit `.env` files daily
- D) Baking production connection strings into the image layers

**B4.** You need blue/green or canary for a Container Apps AI service. Which feature is central?

- A) ACR geo-replication alone
- B) **Revision** management and traffic splitting across revisions
- C) Event Grid custom topics only
- D) Changing the subscription ID

**B5.** An embedding worker should scale out when a Service Bus queue depth grows. Which Container Apps capability matches the study guide?

- A) Manual VM scale sets only
- B) **KEDA** event-driven autoscaling in Container Apps
- C) Fixed replica count of 1 forever
- D) Scaling only via Cosmos DB RUs

**B6.** You must deploy an app to AKS using Kubernetes YAML. What does the exam expect?

- A) Only portal click-ops with no manifests
- B) Deploy and manage applications using **manifest files**
- C) Replace AKS with Logic Apps exclusively
- D) Store manifests as secrets in Redis

**B7.** Production Container Apps revisions fail readiness. First troubleshooting sources called out by the skills outline?

- A) Ignore logs and increase RUs
- B) Inspect **logs, events, and end-to-end connectivity**
- C) Delete the subscription
- D) Disable ingress permanently

**B8.** Why avoid putting API keys in the container image for App Service / Container Apps?

- A) Images are immutable artifacts that are copied and retained; secrets in layers widen blast radius — inject secrets/env at runtime or use managed identity
- B) Docker forbids environment variables
- C) ACR cannot store images that use env vars
- D) App Service cannot read environment variables

**B9.** ACR Tasks support which build scenarios relevant to AI backends?

- A) Only building Windows XP ISOs
- B) Cloud-based image builds (on-demand, source triggers, base-image update triggers)
- C) Compiling only .NET Framework 2.0
- D) Replacing Azure Functions entirely

**B10.** You change a Container Apps container image tag. What typically happens?

- A) Nothing — images are ignored
- B) A **revision-scope** change creates a new revision (image/config under the template)
- C) Only App Configuration is updated
- D) Key Vault deletes all secrets

---

### Topic C — Connect to and consume Azure services (10 questions)

**C1.** Thousands of documents must be embedded asynchronously with retries and failure isolation. Which service fits best?

- A) Azure Service Bus for queuing/processing back-end operations
- B) Azure DNS
- C) Azure Static Web Apps only
- D) Azure Advisor recommendations alone

**C2.** A Service Bus message fails repeatedly until `MaxDeliveryCount` is exceeded. Where does it go?

- A) Azure CDN
- B) The entity’s **dead-letter queue (DLQ)**
- C) Cosmos DB change feed automatically
- D) App Configuration

**C3.** Multiple downstream AI workers need different subsets of the same events. Which Service Bus pattern fits?

- A) A single queue with competing consumers only, no filtering
- B) **Topics and subscriptions** (publish once; filter per subscription)
- C) Store messages in public Blob containers
- D) Use only HTTP 200 polling of a website

**C4.** Blob-created events should start a lightweight workflow with filters and retries. Which service matches the skills outline?

- A) Azure Event Grid (filters, custom events, retries)
- B) Azure Bastion
- C) Azure Disk Encryption set
- D) Azure Front Door WAF policies only

**C5.** Difference emphasized for exam scenarios: Service Bus vs Event Grid?

- A) They are identical products
- B) Service Bus is for **durable messaging/work queues**; Event Grid is for **reactive event delivery/notification** with filters/retries
- C) Event Grid replaces PostgreSQL
- D) Service Bus cannot dead-letter

**C6.** You build a serverless HTTP API that also reacts to queue messages. Which Azure Functions concepts are required skills?

- A) Only timer triggers with no bindings
- B) **Triggers and bindings**, plus configuring/deploying function apps
- C) Only running Functions inside Redis
- D) Disabling all authentication forever

**C7.** An AI pipeline Function should run when a Service Bus message arrives. Best binding choice?

- A) Cosmos DB input binding only with no trigger
- B) **Service Bus trigger** (and optional output bindings for side effects)
- C) Manual `while True` sleep loops in a VM
- D) FTP trigger exclusively

**C8.** Consumers may receive the same message more than once. Safest AI worker pattern?

- A) Blindly insert duplicates every time
- B) **Idempotent processing** (dedup keys / upserts / processing ledger)
- C) Disable Service Bus peek-lock
- D) Log the API key on every retry

**C9.** Event Grid subscription should only handle one event type from a custom topic. What do you configure?

- A) **Filters** on the Event Grid subscription
- B) AKS network policies only
- C) ACR Tasks timer triggers
- D) Strong consistency on Cosmos DB

**C10.** Why use messaging when calling rate-limited embedding APIs?

- A) Messaging deletes rate limits permanently
- B) Queues **smooth load**, enable controlled concurrency, and support retries/DLQ instead of unbounded synchronous fan-out
- C) Event Grid guarantees free unlimited model tokens
- D) Functions cannot call external APIs

---

### Topic D — Secure, monitor, troubleshoot (10 questions)

**D1.** Where should you store database passwords and API keys for rotation and retrieval?

- A) Hard-coded in Git
- B) **Azure Key Vault** (with rotation and retrieval as required skills)
- C) Public README files
- D) Container image `ENV` baked at build time as the only store

**D2.** Feature flags and non-secret settings that change without redeploying code belong in:

- A) Azure App Configuration
- B) Azure Disk SKU names
- C) ACR anonymous pull exclusively
- D) Event Grid schema only

**D3.** Recommended pattern: App Configuration + Key Vault together?

- A) Put secrets in App Configuration plaintext and ignore Key Vault
- B) Store **Key Vault references** in App Configuration; app resolves secrets at runtime with managed identity
- C) Disable both services
- D) Copy secrets into Cosmos DB documents

**D4.** You must trace an AI request across API → Function → Cosmos DB → model call. Which skill is measured?

- A) Only screenshots of the portal
- B) Distributed tracing with **OpenTelemetry** SDKs
- C) Disabling all telemetry for privacy by logging raw prompts instead
- D) Using FTP logs exclusively

**D5.** You investigate elevated exception rates in Log Analytics. Which skill is measured?

- A) Writing **KQL** queries against logs/metrics
- B) Only deleting the Log Analytics workspace
- C) Restarting Windows Explorer
- D) Changing the Azure AD tenant name

**D6.** Least privilege for an App Service managed identity that only reads one Key Vault secret?

- A) Owner on the subscription
- B) Narrow RBAC such as **Key Vault Secrets User** (or equivalent get permission) on that vault/secret scope
- C) Contributor on every resource group
- D) Global Administrator

**D7.** Secret near expiry should trigger rotation automation. Which Key Vault-related pattern is documented by Microsoft?

- A) Never rotate secrets
- B) Use Key Vault events (for example near-expiry) with handlers (Functions/Event Grid) to rotate and update dependents
- C) Email passwords in clear text weekly
- D) Store only the previous secret version forever in App Settings without Key Vault

**D8.** What should you generally avoid putting in production traces/logs for AI backends?

- A) Correlation IDs and latency per dependency
- B) Raw prompts, secrets, and unnecessary PII
- C) HTTP status codes
- D) Deployment/version stamps

**D9.** OpenTelemetry in Azure Monitor Application Insights is used to:

- A) Replace Key Vault
- B) Emit traces/metrics/logs for distributed systems so you can diagnose end-to-end latency and failures
- C) Build container images
- D) Provision PostgreSQL extensions

**D10.** A canary revision shows higher p95 latency. Best next step using measured skills?

- A) Immediately delete all monitoring
- B) Use traces (OpenTelemetry) + **KQL** to compare dependency durations and error rates between revisions, then fix or roll back
- C) Disable KEDA permanently
- D) Switch all consistency levels to Strong without measuring

---

## 6. Answer key with official source validation

Each answer cites the **skills measured** bullet and a Microsoft Learn page that substantiates the concept.

### Topic A answers

| Q | Answer | Why (short) | Official validation |
|---|--------|-------------|---------------------|
| **A1** | **B** | Skills require a change feed processor for new/updated items — ideal for incremental re-embed/reindex. | [AI-200 study guide — Cosmos change feed](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [Change feed](https://learn.microsoft.com/en-us/azure/cosmos-db/change-feed) |
| **A2** | **B** | Outline: optimize RUs using **indexing policies** and **consistency levels**. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [Consistency levels](https://learn.microsoft.com/en-us/azure/cosmos-db/consistency-levels) |
| **A3** | **B** | Outline: store/retrieve embeddings; execute **vector similarity search**. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [Vector search in Cosmos DB](https://learn.microsoft.com/en-us/azure/cosmos-db/vector-search) |
| **A4** | **B** | Outline: RAG patterns using metadata filters with vector search. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [pgvector on Azure Database for PostgreSQL](https://learn.microsoft.com/en-us/azure/postgresql/flexible-server/how-to-use-pgvector) |
| **A5** | **B** | Outline lists indexing, reducing pgvector overhead, and sizing resources. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [pgvector docs](https://learn.microsoft.com/en-us/azure/postgresql/flexible-server/how-to-use-pgvector) |
| **A6** | **B** | Outline: implement **vector indexing** for similarity search on Managed Redis. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [Vector similarity on Azure Managed Redis](https://learn.microsoft.com/en-us/azure/redis/overview-vector-similarity) |
| **A7** | **B** | Outline: caching, expiration, and invalidation. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [Azure Managed Redis overview](https://learn.microsoft.com/en-us/azure/redis/overview) |
| **A8** | **B** | RAG with metadata filters is an explicit skill; tenant filter is the production pattern. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [pgvector](https://learn.microsoft.com/en-us/azure/postgresql/flexible-server/how-to-use-pgvector) |
| **A9** | **B** | Consistency is a tradeoff axis affecting latency/availability/RUs — exam lever for RU optimization. | [Consistency levels](https://learn.microsoft.com/en-us/azure/cosmos-db/consistency-levels); [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200) |
| **A10** | **B** | Outline: connect using the SDK and run queries. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [Cosmos DB Python SDK](https://learn.microsoft.com/en-us/azure/cosmos-db/nosql/sdk-python) |

### Topic B answers

| Q | Answer | Why (short) | Official validation |
|---|--------|-------------|---------------------|
| **B1** | **B** | Skills: build/run images with **ACR Tasks**; ACR builds without local Docker. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [ACR Tasks overview](https://learn.microsoft.com/en-us/azure/container-registry/container-registry-tasks-overview) |
| **B2** | **B** | Skills: build, store, version, manage images with ACR. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [Azure Container Registry](https://learn.microsoft.com/en-us/azure/container-registry/) |
| **B3** | **B** | Skills: deploy to App Service including env vars and secrets. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [App Service](https://learn.microsoft.com/en-us/azure/app-service/) |
| **B4** | **B** | Skills: Container Apps environment config and **revision** management; docs cover traffic split. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [Container Apps revisions](https://learn.microsoft.com/en-us/azure/container-apps/revisions) |
| **B5** | **B** | Skills: event-driven scaling with **KEDA** in Container Apps. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [Container Apps overview (KEDA)](https://learn.microsoft.com/en-us/azure/container-apps/overview) |
| **B6** | **B** | Skills: deploy/manage AKS apps using **manifest files**. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [AKS documentation](https://learn.microsoft.com/en-us/azure/aks/) |
| **B7** | **B** | Skills: monitor/troubleshoot via logs, events, connectivity. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [Container Apps log monitoring](https://learn.microsoft.com/en-us/azure/container-apps/log-monitoring) |
| **B8** | **A** | Images are shared artifacts; inject secrets at runtime / use MI (App Service + Key Vault skills reinforce this). | [App Service](https://learn.microsoft.com/en-us/azure/app-service/); [Key Vault](https://learn.microsoft.com/en-us/azure/key-vault/); [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200) |
| **B9** | **B** | ACR Tasks: cloud builds, source/base-image/timer triggers. | [ACR Tasks overview](https://learn.microsoft.com/en-us/azure/container-registry/container-registry-tasks-overview) |
| **B10** | **B** | Image/template changes are revision-scope → new revision. | [Container Apps revisions](https://learn.microsoft.com/en-us/azure/container-apps/revisions) |

### Topic C answers

| Q | Answer | Why (short) | Official validation |
|---|--------|-------------|---------------------|
| **C1** | **A** | Skills: queue/process back-end ops with Service Bus. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [Service Bus messaging](https://learn.microsoft.com/en-us/azure/service-bus-messaging/) |
| **C2** | **B** | Skills include DLQ handling; docs define DLQ after max deliveries / failures. | [Service Bus dead-letter queues](https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-dead-letter-queues); [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200) |
| **C3** | **B** | Skills: topics and subscriptions. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [Service Bus topics](https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-messaging-overview) |
| **C4** | **A** | Skills: Event Grid filters, custom events, retries. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [Event Grid](https://learn.microsoft.com/en-us/azure/event-grid/) |
| **C5** | **B** | Messaging vs eventing roles as assessed under C1. | [Service Bus](https://learn.microsoft.com/en-us/azure/service-bus-messaging/); [Event Grid concepts](https://learn.microsoft.com/en-us/azure/event-grid/concepts) |
| **C6** | **B** | Skills: triggers/bindings; configure and deploy function apps. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [Azure Functions](https://learn.microsoft.com/en-us/azure/azure-functions/) |
| **C7** | **B** | Service Bus trigger is the standard Functions integration for queues/topics. | [Functions Service Bus bindings](https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-service-bus); [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200) |
| **C8** | **B** | At-least-once delivery implies idempotent consumers (production + exam reasoning). | [Service Bus](https://learn.microsoft.com/en-us/azure/service-bus-messaging/); related skill: DLQ/message processing |
| **C9** | **A** | Skills explicitly list Event Grid **filters**. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [Event Grid filtering](https://learn.microsoft.com/en-us/azure/event-grid/event-filtering) |
| **C10** | **B** | Async queueing is the assessed pattern for back-end AI operations under load. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [Service Bus overview](https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-messaging-overview) |

### Topic D answers

| Q | Answer | Why (short) | Official validation |
|---|--------|-------------|---------------------|
| **D1** | **B** | Skills: Key Vault including rotation and retrieval. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [Key Vault](https://learn.microsoft.com/en-us/azure/key-vault/); [Secret rotation tutorial](https://learn.microsoft.com/en-us/azure/key-vault/secrets/tutorial-rotation) |
| **D2** | **A** | Skills: store/retrieve app configuration via App Configuration. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [App Configuration](https://learn.microsoft.com/en-us/azure/azure-app-configuration/) |
| **D3** | **B** | Documented complementary pattern: references in App Config, values in Key Vault. | [Key Vault references (Python)](https://learn.microsoft.com/en-us/azure/azure-app-configuration/use-key-vault-references-python-provider) |
| **D4** | **B** | Skills: trace distributed systems with OpenTelemetry SDKs. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [Enable OpenTelemetry with Application Insights](https://learn.microsoft.com/en-us/azure/azure-monitor/app/opentelemetry-enable) |
| **D5** | **A** | Skills: write KQL to analyze logs and metrics. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [Kusto Query Language](https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/) |
| **D6** | **B** | Least privilege aligns with Key Vault secure access guidance + audience security responsibilities. | [Key Vault RBAC](https://learn.microsoft.com/en-us/azure/key-vault/general/rbac-guide); certification overview security lifecycle |
| **D7** | **B** | Microsoft documents Event Grid–driven rotation near expiry. | [Tutorial: rotation](https://learn.microsoft.com/en-us/azure/key-vault/secrets/tutorial-rotation) |
| **D8** | **B** | Responsible production practice; exam expects secure monitoring without leaking secrets/PII. | [App Insights / OTel](https://learn.microsoft.com/en-us/azure/azure-monitor/app/opentelemetry-enable); certification security/monitoring domain |
| **D9** | **B** | OpenTelemetry is the measured tracing approach for Azure solutions on this exam. | [OpenTelemetry enable](https://learn.microsoft.com/en-us/azure/azure-monitor/app/opentelemetry-enable); [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200) |
| **D10** | **B** | Combines both measured monitoring skills: OTel + KQL analysis before rollback/fix. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [KQL](https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/); [OTel](https://learn.microsoft.com/en-us/azure/azure-monitor/app/opentelemetry-enable) |

---

## 7. Quick service chooser (exam intuition)

| Need | Prefer |
|------|--------|
| Document DB + vectors + change-driven sync | **Cosmos DB for NoSQL** |
| Relational metadata + pgvector RAG filters | **Azure Database for PostgreSQL** |
| Ultra-low-latency cache + vector index | **Azure Managed Redis** |
| Durable work queue / DLQ / topics | **Service Bus** |
| Reactive notifications / filters / retries | **Event Grid** |
| Short event-driven compute + bindings | **Azure Functions** |
| Registry + cloud build | **ACR / ACR Tasks** |
| Simple container web API | **App Service (containers)** |
| Serverless containers + revisions + KEDA | **Container Apps** |
| Full Kubernetes control via YAML | **AKS** |
| Secrets + rotation | **Key Vault** |
| Dynamic non-secret config | **App Configuration** |
| Distributed traces | **OpenTelemetry → Azure Monitor** |
| Log/metric investigation | **KQL** |

---

## 8. Official links checklist

- [Certification page](https://learn.microsoft.com/en-us/credentials/certifications/azure-ai-cloud-developer-associate/?practice-assessment-type=certification)
- [Study guide (skills measured)](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200)
- [Exam sandbox](https://aka.ms/examdemo)
- [Exam scoring](https://learn.microsoft.com/en-us/credentials/certifications/exam-scoring-reports)
- [Renewal](https://learn.microsoft.com/en-us/credentials/certifications/renew-your-microsoft-certification)
- [Schedule (Pearson Vue)](https://learn.microsoft.com/en-us/credentials/certifications/schedule-through-pearson-vue?examUid=exam.AI-200)

---

## 9. Local course map (optional deep dive)

| Need | Path |
|------|------|
| Index | [`AI-200-topics.md`](./AI-200-topics.md) |
| AI tutor prompt | [`AI-200-INSTRUCTOR.md`](./AI-200-INSTRUCTOR.md) |
| Roadmap | [`topics_details/00-exam-roadmap.md`](./topics_details/00-exam-roadmap.md) |
| Topic deep dives | [`topics_details/`](./topics_details/) |
| Labs | [`topics_details/labs/`](./topics_details/labs/) |
| Exam traps | [`topics_details/reference/exam-traps.md`](./topics_details/reference/exam-traps.md) |

---

*Last aligned to Microsoft Learn certification page and AI-200 study guide skills measured (April 15, 2026). Re-check the study guide before your exam date — Microsoft may update skills measured.*
