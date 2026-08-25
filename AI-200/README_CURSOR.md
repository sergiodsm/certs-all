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
2. Drill **one topic** at a time (20 MCQs). Cover answers until you attempt.
3. For each miss: read the **Official source** link, then re-answer from memory.
4. Target **≥ 16/20** per topic before scheduling.
5. Optional deeper material in this folder: [`AI-200-topics.md`](./AI-200-topics.md), [`AI-200-INSTRUCTOR.md`](./AI-200-INSTRUCTOR.md), [`topics_details/`](./topics_details/).

---

## 5. Exam-style practice questions (20 per topic)

Format: single best answer unless noted.  
**Answers, explanations, and official sources** are in [Section 6](#6-answer-key-with-official-source-validation).

---

### Topic A — Azure data management for AI (20 questions)

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

**A11.** Your Cosmos DB items store large embedding arrays that are never used in `WHERE`/`ORDER BY` property filters. Writes are expensive. What indexing practice reduces RU cost while still enabling vector search?

- A) Index every property including the embedding path with the default policy only
- B) Exclude the embedding path from the standard property index and define a **vector index** on that path
- C) Turn indexing mode to `none` for the entire container permanently
- D) Store embeddings as the partition key string

**A12.** A RAG sync must remove vectors when source documents are deleted. Latest-version change feed alone is insufficient because:

- A) Change feed is never enabled by default
- B) Latest-version mode does **not** capture deletes; you need **all versions and deletes** mode (or another delete signal)
- C) Change feed only works for MongoDB API
- D) Deletes always appear as inserts in latest-version mode

**A13.** You implement a change feed processor for parallel consumers. What extra store does the processor use for leases/checkpoints?

- A) Azure Front Door rules
- B) A **lease container** in Cosmos DB for checkpointing and partition ownership
- C) Azure DNS TXT records
- D) ACR Tasks logs only

**A14.** Before using pgvector on Azure Database for PostgreSQL flexible server, what must you do in the target database?

- A) Install Redis modules inside PostgreSQL
- B) Allowlist the extension and run `CREATE EXTENSION vector;`
- C) Convert the server to Cosmos DB API for PostgreSQL only
- D) Disable all indexes

**A15.** The skills outline calls out connection optimization for PostgreSQL AI workloads. Which approach improves throughput and lowers latency under many concurrent RAG queries?

- A) Open a new TCP connection for every single query with no pooling
- B) Use **connection pooling** (and appropriate pool sizing) so clients reuse connections
- C) Restart the flexible server after every query
- D) Store connection strings in public GitHub gists

**A16.** Cached RAG answers in Azure Managed Redis become stale after document updates. Which operations match the skills outline?

- A) Never expire keys; hope clients forget them
- B) Use **expiration (TTL)** and **invalidation** when source data changes
- C) Delete the entire Redis instance nightly
- D) Replace Redis with Azure DNS caching

**A17.** Official Cosmos DB RU guidance: compared with more relaxed levels, Strong and Bounded staleness reads typically:

- A) Cost about the same RUs always
- B) Consume roughly **~2× more RUs** for reads
- C) Are free of RU charges
- D) Only affect write RUs, never reads

**A18.** For a known document `id` and partition key, the cheapest Cosmos DB read pattern is:

- A) A cross-partition `SELECT *` query
- B) A **point read** (read item by id + partition key)
- C) A full container scan with `ORDER BY`
- D) Export to CSV then grep locally

**A19.** To use vector similarity search on Azure Managed Redis, which requirement is documented?

- A) RediSearch (vector) capabilities via modules configured appropriately (for example at create time; modules can’t be added later on Managed Redis)
- B) Only the Basic Azure Cache SKU without search modules
- C) Disabling all clustering policies forever
- D) Storing vectors exclusively as unindexed strings named `vec`

**A20.** Enabling the `vector` extension name on Azure PostgreSQL — what is the correct extension identifier used in `CREATE EXTENSION`?

- A) `pgvector` (the community nickname only)
- B) `vector` (binary/extension name is `vector`)
- C) `cosmosdb`
- D) `redissearch`

---

### Topic B — Containerized solutions on Azure (20 questions)

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

**B11.** You deploy a container to App Service and need secrets without putting values in plain app settings. What documented pattern fits?

- A) Commit secrets to the Dockerfile `ENV`
- B) Use **Key Vault references** in App Service app settings with a **managed identity** that can read the vault
- C) Print secrets to container stdout for ops to copy
- D) Store secrets only in public ACR labels

**B12.** You update only Container Apps **ingress traffic splitting** between existing revisions. What change type is this?

- A) Revision-scope (always creates a new revision)
- B) **Application-scope** (applies globally; does not create a new revision)
- C) ACR Tasks–scope
- D) Cosmos DB indexing-scope

**B13.** An idle AI worker on Container Apps should cost near-zero when the queue is empty. Which scaling behavior is supported?

- A) Containers can never scale below 3 replicas
- B) Configure scale rules (including KEDA) so the app can **scale to zero** when there is no work
- C) Only vertical scaling of a single VM is allowed
- D) Scaling requires deleting and recreating the environment daily

**B14.** Skills require versioning container images in ACR. Which practice is correct?

- A) Always overwrite the same mutable `latest` tag with no other tags and no digests tracked
- B) Push **immutable tags** (for example git SHA / semver) and promote those tags through environments
- C) Store images only as untagged manifests forever
- D) Version images by renaming the ACR resource group

**B15.** AKS pods serve traffic before the AI model client is ready, causing 5xx. What should manifests define?

- A) Only a single `sleep infinity` command
- B) **Readiness** (and usually liveness) **probes** so traffic waits until the container is ready
- C) `hostNetwork: true` only
- D) Disable the kubelet

**B16.** You need two Container Apps revisions active with 10%/90% traffic for a canary. Which revision mode supports this?

- A) Single revision mode only (exactly one active revision)
- B) **Multiple** revision mode with traffic weights
- C) ACR Tasks timer mode
- D) Event Grid push mode

**B17.** Your base OS image in ACR is patched. How can ACR Tasks help application images stay current?

- A) They cannot detect base image updates
- B) Configure tasks with **base image update triggers** to rebuild dependent app images
- C) Manually FTP patched layers into running containers
- D) Disable immutable containers and patch in place with SSH

**B18.** Container Apps must pull a private image from ACR. Preferred auth approach?

- A) Embed ACR admin password in the image
- B) Use managed identity / registry credentials configured on the Container App (avoid hard-coded passwords in code)
- C) Make the ACR fully anonymous for the internet
- D) Copy images to public Docker Hub only

**B19.** You manage an AKS deployment declared as YAML in Git. Which workflow matches the skills outline?

- A) Only click Deploy in the portal with no files
- B) Apply/update workloads using **manifest files** (for example `kubectl apply -f`) as part of CI/CD
- C) Store YAML only inside Redis keys
- D) Convert all YAML to CSV first

**B20.** When configuring Container Apps HTTP or KEDA scale rules, which bounds should you set for cost and capacity control?

- A) No min/max — unbounded scale only
- B) Explicit **min replicas** and **max replicas** (and scale rule metadata) appropriate to the SLO and budget
- C) Max replicas must always equal zero
- D) Min replicas must equal the number of Cosmos partitions

---

### Topic C — Connect to and consume Azure services (20 questions)

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

**C11.** A Service Bus receiver uses peek-lock. What must the app do after successful processing?

- A) Nothing — messages auto-complete without settlement
- B) **Complete** (settle) the message so it is removed; otherwise it may redeliver after lock expiry
- C) Delete the entire queue namespace
- D) Move the message to Azure DNS

**C12.** Your microservice needs to publish application-defined AI pipeline events (not only built-in Azure resource events). Which Event Grid feature fits?

- A) Only Storage account system topics
- B) A **custom topic** (or custom events) that your app publishes to
- C) ACR Tasks only
- D) Key Vault soft-delete events exclusively

**C13.** Event Grid keeps failing delivery to a webhook after retries. How do you avoid silently losing events?

- A) There is no option; events always vanish
- B) Configure **dead-lettering** (for example to a storage account) on the event subscription
- C) Increase Cosmos DB RUs
- D) Disable TLS on the webhook

**C14.** A Function should write a processed result to Blob Storage without manual SDK boilerplate. What Functions concept is this?

- A) An **output binding**
- B) A Container Apps revision
- C) A Kusto cluster
- D) An ACR geo-replica

**C15.** You expose a lightweight serverless HTTP API for RAG query orchestration. Which Functions trigger matches?

- A) Blob trigger only
- B) **HTTP trigger** (with optional other bindings)
- C) Cosmos DB change feed is the only allowed trigger
- D) FTP trigger

**C16.** Producers may send the same embedding job message twice within a short window. Which Service Bus feature helps?

- A) **Duplicate detection** (requires enabling on the queue/topic with a history window)
- B) Event Grid subject filtering only
- C) App Configuration feature flags only
- D) AKS Horizontal Pod Autoscaler only

**C17.** Event Grid retry policy can be customized with which pair of settings (classic subscriptions)?

- A) CPU quota and memory quota only
- B) **Maximum delivery attempts** and **event time-to-live (TTL)**
- C) Partition key and RU/s only
- D) Docker HEALTHCHECK interval only

**C18.** Skills require configuring and deploying function apps. Where do connection strings and non-secret settings typically live for a deployed Function App?

- A) Only inside the ZIP package as plaintext secrets committed to Git
- B) **Application settings** (and Key Vault references where needed) on the Function App
- C) Azure DNS CNAME records
- D) ACR anonymous manifests

**C19.** You need strict ordered processing of per-document reindex commands. Which Service Bus capability is designed for this?

- A) **Sessions** (session-enabled queue/subscription) so messages with the same session ID are processed in order
- B) Random competing consumers with no session id
- C) Event Grid push with no ordering guarantees as the only option
- D) Dropping message IDs

**C20.** A Function uses a trigger plus an input binding. What is the accurate mental model from Functions docs?

- A) Triggers and bindings are the same thing always
- B) A **trigger** starts the function; **bindings** declaratively connect input/output data without always writing custom client code
- C) Bindings replace the need for any host runtime
- D) Triggers only work on-premises

---

### Topic D — Secure, monitor, and troubleshoot Azure solutions (20 questions)

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

**D11.** After rotating a Key Vault secret, clients still see the old value. What should you verify?

- A) That clients retrieve the **current secret version** (or refresh references) and that apps reload configuration after rotation
- B) That soft-delete is disabled forever
- C) That the secret name changed daily
- D) That RBAC is set to Owner on the subscription only

**D12.** You need different App Configuration values for `dev`, `test`, and `prod` without separate stores for every key. What feature helps?

- A) **Labels** (and/or separate stores) to select environment-specific configuration
- B) Only Cosmos DB consistency levels
- C) ACR Tasks timer triggers
- D) Service Bus sessions

**D13.** Apps should pick up App Configuration changes without full redeploy. Which documented pattern is common?

- A) Rebuild the container image on every flag flip
- B) Use the configuration provider **refresh** mechanism (often with a sentinel key) to reload settings
- C) Restart every Azure subscription
- D) Disable managed identity

**D14.** You want exception counts per 5-minute bin in Log Analytics. Which skill applies?

- A) Write a **KQL** query using operators such as `summarize` and `bin(timestamp, 5m)`
- B) Only download CSVs and chart in Excel by hand (exam skill is KQL)
- C) Delete the Application Insights resource
- D) Use FTP directory listing

**D15.** OpenTelemetry traces across Functions and Container Apps don’t stitch together. What is usually missing?

- A) Propagation of **trace context / correlation** across service boundaries
- B) A larger App Service plan SKU only
- C) Disabling HTTPS
- D) Turning off all instrumentation

**D16.** Someone accidentally deletes a Key Vault secret. What protection should already be enabled?

- A) **Soft-delete** (and purge protection in production) so secrets can be recovered
- B) Public anonymous blob access to a backup JSON
- C) Storing the only copy in chat history
- D) Disabling versioning always

**D17.** Feature enablement for a new RAG path should be toggled without redeploying containers. Best home for the flag?

- A) Hard-coded boolean in the image
- B) **Azure App Configuration** (feature flags / dynamic settings)
- C) Azure DNS MX records
- D) The ACR admin password

**D18.** A sample KQL starting point to find recent failures in Application Insights–style tables is closest to:

- A) `exceptions | where timestamp > ago(1h) | summarize count() by problemId`
- B) `DELETE FROM cosmos`
- C) `docker system prune`
- D) `az group delete --yes`

**D19.** Python code should authenticate to Key Vault and App Configuration in both local dev and Azure with minimal branching. Which credential type is recommended?

- A) Hard-coded access keys in source
- B) **`DefaultAzureCredential`** from `azure-identity` (tries managed identity in Azure, developer creds locally)
- C) Anonymous public access
- D) Shared SAS tokens committed to Git

**D20.** To analyze Container Apps or App Service logs with KQL, logs must first land in a queryable store. What do you typically configure?

- A) **Diagnostic settings** (or built-in Log Analytics integration) so logs/metrics flow to a Log Analytics workspace
- B) Only local debugger breakpoints in production
- C) Printing secrets to the console as the only signal
- D) Disabling all logging sinks

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
| **A11** | **B** | Large embedding vectors inflate write RUs if indexed as normal properties; exclude them from the property index and use a dedicated **vector index**. | [Vector search indexing](https://learn.microsoft.com/en-us/azure/cosmos-db/vector-search); [Optimize write costs / indexing](https://learn.microsoft.com/en-us/azure/cosmos-db/optimize-cost-reads-writes) |
| **A12** | **B** | Latest-version change feed surfaces latest insert/update versions and does **not** include deletes; all versions and deletes mode (continuous backup) captures deletes. | [Change feed](https://learn.microsoft.com/en-us/azure/cosmos-db/change-feed); [Change feed modes](https://learn.microsoft.com/en-us/azure/cosmos-db/change-feed-modes) |
| **A13** | **B** | The change feed processor uses a **lease container** for checkpoints and distributed partition ownership (“at least once” with managed checkpointing). | [Change feed processor](https://learn.microsoft.com/en-us/azure/cosmos-db/change-feed-processor); [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200) |
| **A14** | **B** | Allowlist the extension on the flexible server, then `CREATE EXTENSION vector;` per database. | [pgvector on Azure Database for PostgreSQL](https://learn.microsoft.com/en-us/azure/postgresql/flexible-server/how-to-use-pgvector) |
| **A15** | **B** | Connection pooling is the standard way to improve throughput and reduce connection setup latency under concurrent query load (skills: connection optimization). | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [Connection pooling best practices](https://learn.microsoft.com/en-us/azure/postgresql/flexible-server/concepts-connection-pooling-best-practices); [PgBouncer](https://learn.microsoft.com/en-us/azure/postgresql/connectivity/concepts-pgbouncer) |
| **A16** | **B** | Skills explicitly list caching, **expiration**, and **invalidation** for Managed Redis in AI solutions. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [Azure Managed Redis overview](https://learn.microsoft.com/en-us/azure/redis/overview) |
| **A17** | **B** | Microsoft documents that Strong and Bounded staleness reads consume about **two times** more RUs than more relaxed levels. | [Request units](https://learn.microsoft.com/en-us/azure/cosmos-db/request-units); [Consistency levels](https://learn.microsoft.com/en-us/azure/cosmos-db/consistency-levels) |
| **A18** | **B** | Point reads by id + partition key cost fewer RUs than queries — official RU guidance. | [Request units](https://learn.microsoft.com/en-us/azure/cosmos-db/request-units) |
| **A19** | **A** | Vector similarity on Azure Managed Redis uses RediSearch-based vector capabilities; modules must be enabled when the instance is created. | [Vector similarity overview](https://learn.microsoft.com/en-us/azure/redis/overview-vector-similarity); [Redis modules](https://learn.microsoft.com/en-us/azure/redis/redis-modules) |
| **A20** | **B** | Docs: community name is “pgvector”, but `CREATE EXTENSION` uses **`vector`**. | [pgvector how-to](https://learn.microsoft.com/en-us/azure/postgresql/flexible-server/how-to-use-pgvector) |

#### Topic A — explanations (11–20)

- **A11:** Default indexing indexes many paths and write RU cost grows with indexed properties and item size. Vector search docs show excluding the embedding path from `includedPaths` while adding `vectorIndexes`. That keeps semantic search without paying full property-index write cost on huge arrays.
- **A12:** For delete-aware RAG sync, latest-version mode is the wrong assumption. Use all versions and deletes mode (needs continuous backup) or another explicit delete pipeline.
- **A13:** Skills call out the change feed **processor**. Official components include the monitored container plus a lease container that stores continuation state so multiple workers can share work safely.
- **A14:** Without `CREATE EXTENSION vector`, vector types/operators are unavailable. Azure also requires allowlisting the extension on the flexible server first.
- **A15:** Opening a connection per request thrashes CPU and latency. Pooling (app-side or PgBouncer-style) is how you “implement connection optimization” under load.
- **A16:** Stale semantic cache answers are a classic AI bug. TTL bounds freshness; explicit invalidation on document change keeps correctness.
- **A17:** Consistency is an RU lever on the exam. Prefer Session/Eventual when Strong isn’t required for the read path.
- **A18:** If you know id + PK, don’t query — point read. Saves RUs and latency for lookup-heavy AI backends.
- **A19:** Managed Redis vector search isn’t “plain GET/SET”. You need the search/vector module stack configured correctly at provisioning time.
- **A20:** Easy exam trap: typing `CREATE EXTENSION pgvector` fails; the extension name is `vector`.

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
| **B11** | **B** | App Service resolves Key Vault references into settings using the app’s managed identity. | [App Service Key Vault references](https://learn.microsoft.com/en-us/azure/app-service/app-service-key-vault-references); [AI-200 study guide — App Service secrets](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200) |
| **B12** | **B** | Traffic splitting / ingress settings are **application-scope** configuration and do not create a new revision. | [Container Apps revisions](https://learn.microsoft.com/en-us/azure/container-apps/revisions) |
| **B13** | **B** | Container Apps can scale to zero with scale rules / KEDA for many workloads. | [Scale in Azure Container Apps](https://learn.microsoft.com/en-us/azure/container-apps/scale-app); [Container Apps overview](https://learn.microsoft.com/en-us/azure/container-apps/overview) |
| **B14** | **B** | Skills require versioning images; immutable tags (SHA/semver) are the operational practice for promotions. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [ACR](https://learn.microsoft.com/en-us/azure/container-registry/) |
| **B15** | **B** | Readiness probes gate traffic until dependencies are up — standard AKS/container troubleshooting. | [AKS reliability best practices — probes](https://learn.microsoft.com/en-us/azure/aks/best-practices-app-cluster-reliability); [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200) |
| **B16** | **B** | Multiple revision mode enables simultaneous active revisions and traffic splitting (canary/blue-green). | [Container Apps revisions](https://learn.microsoft.com/en-us/azure/container-apps/revisions) |
| **B17** | **B** | ACR Tasks can trigger rebuilds when a base image is updated — OS/framework patching for immutable images. | [ACR Tasks overview](https://learn.microsoft.com/en-us/azure/container-registry/container-registry-tasks-overview) |
| **B18** | **B** | Private ACR pulls should use identity/registry auth configured on the app — not passwords in images. | [Container Apps / ACR](https://learn.microsoft.com/en-us/azure/container-apps/containers); [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200) |
| **B19** | **B** | Skills measured: deploy/manage AKS apps using **manifest files**. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [Deploy to AKS](https://learn.microsoft.com/en-us/azure/aks/kubernetes-walkthrough) |
| **B20** | **B** | Scale rules include min/max replica bounds to protect cost and capacity. | [Scale in Azure Container Apps](https://learn.microsoft.com/en-us/azure/container-apps/scale-app) |

#### Topic B — explanations (11–20)

- **B11:** Skills say configure App Service to supply secrets. Key Vault references keep secret material out of plaintext settings while the platform injects values at runtime via managed identity.
- **B12:** Exam trap: not every change creates a revision. Image/scale-template changes do; ingress traffic rules are application-scope.
- **B13:** Queue-driven AI workers often set min replicas to 0 with KEDA so you pay only when messages exist (within platform rules).
- **B14:** `latest`-only workflows make rollbacks and audit hard. Tag with commit SHA or semver and deploy that digest/tag.
- **B15:** If the process is “up” but the model client isn’t ready, readiness must fail until warm — otherwise AKS routes traffic too early.
- **B16:** Single mode auto-shifts traffic after new revision is healthy; multiple mode is required for explicit percentage canaries.
- **B17:** Base-image triggers automate patching without developers manually rebuilding every dependent AI API image.
- **B18:** Admin passwords in env/images are an exam anti-pattern; use managed identity / integrated registry auth.
- **B19:** Manifest-driven GitOps/CI (`kubectl apply`, Helm, etc.) is what “using manifest files” means on the outline.
- **B20:** Unbounded max replicas can exhaust quota/cost during embedding storms; set max and meaningful scale metadata.

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
| **C11** | **B** | Peek-lock requires settlement (`Complete`); otherwise lock expires and the message is redelivered. | [Service Bus messaging](https://learn.microsoft.com/en-us/azure/service-bus-messaging/); [Peek-lock](https://learn.microsoft.com/en-us/azure/service-bus-messaging/message-transfers-locks-settlement) |
| **C12** | **B** | Skills include **custom events**; custom topics let apps publish their own event schema. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [Custom topics](https://learn.microsoft.com/en-us/azure/event-grid/custom-topics) |
| **C13** | **B** | After retries are exhausted (or for certain non-retryable failures without DLQ), events can be dropped — configure dead-letter destination. | [Event Grid delivery and retry](https://learn.microsoft.com/en-us/azure/event-grid/delivery-and-retry) |
| **C14** | **A** | Output bindings declaratively write to services (Blob, queues, etc.) as part of Functions programming model. | [Functions triggers and bindings](https://learn.microsoft.com/en-us/azure/azure-functions/functions-triggers-bindings) |
| **C15** | **B** | Skills: build serverless APIs with triggers — HTTP trigger is the API entry point. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [HTTP trigger](https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-http-webhook) |
| **C16** | **A** | Service Bus duplicate detection drops copies with the same MessageId within the history window when enabled. | [Duplicate detection](https://learn.microsoft.com/en-us/azure/service-bus-messaging/duplicate-detection) |
| **C17** | **B** | Retry policy knobs: max delivery attempts (1–30) and event TTL in minutes (1–1440). | [Delivery and retry](https://learn.microsoft.com/en-us/azure/event-grid/delivery-and-retry); [Manage event delivery](https://learn.microsoft.com/en-us/azure/event-grid/manage-event-delivery) |
| **C18** | **B** | Deployed Function Apps are configured via application settings (and Key Vault references), not secrets in source. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [App settings](https://learn.microsoft.com/en-us/azure/azure-functions/functions-how-to-use-azure-function-app-settings) |
| **C19** | **A** | Sessions provide ordered processing per session ID — useful for per-document pipelines. | [Message sessions](https://learn.microsoft.com/en-us/azure/service-bus-messaging/message-sessions) |
| **C20** | **B** | Official Functions model: trigger invokes; bindings bind data in/out. | [Triggers and bindings](https://learn.microsoft.com/en-us/azure/azure-functions/functions-triggers-bindings); [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200) |

#### Topic C — explanations (11–20)

- **C11:** If you process but forget to complete, the message reappears — classic duplicate side effects unless your consumer is idempotent.
- **C12:** System topics cover Azure resource events; custom topics cover your domain events (chunk ready, reindex requested).
- **C13:** Skills mention retries; production exams also expect you to know delivery can fail permanently — dead-letter to investigate.
- **C14:** Prefer bindings for simple I/O; use SDK when you need complex control. Exam loves “output binding” language.
- **C15:** Serverless API = HTTP trigger Function App, often fronting queue fan-out for heavy AI work.
- **C16:** Duplicate detection is not on by default everywhere — enable it when producers may retry sends.
- **C17:** You cannot customize the exact backoff schedule, but you can cap attempts and TTL; events drop or dead-letter when limits hit.
- **C18:** “Configure and deploy” includes host settings, connection strings, and identity — not baking secrets into packages.
- **C19:** Competing consumers alone do not preserve per-key order; sessions do.
- **C20:** Don’t confuse trigger (why it runs) with binding (how data is attached). Both appear on the skills outline.

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
| **D11** | **A** | Rotation creates new versions; apps must read current version and refresh Key Vault references / config. | [Key Vault secrets](https://learn.microsoft.com/en-us/azure/key-vault/secrets/); [Rotation tutorial](https://learn.microsoft.com/en-us/azure/key-vault/secrets/tutorial-rotation); [Reload Key Vault secrets](https://learn.microsoft.com/en-us/azure/azure-app-configuration/reload-key-vault-secrets-dotnet) |
| **D12** | **A** | Labels select environment-specific keys from App Configuration. | [App Configuration](https://learn.microsoft.com/en-us/azure/azure-app-configuration/); [Use labels](https://learn.microsoft.com/en-us/azure/azure-app-configuration/howto-labels-aspnet-core) |
| **D13** | **B** | Dynamic configuration refresh (sentinel key pattern) avoids redeploy for setting changes. | [Dynamic configuration](https://learn.microsoft.com/en-us/azure/azure-app-configuration/enable-dynamic-configuration-aspnet-core); [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200) |
| **D14** | **A** | Skills require writing KQL; `summarize` + `bin` is the standard time-series aggregation pattern. | [Kusto Query Language](https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/); [summarize operator](https://learn.microsoft.com/en-us/kusto/query/summarize-operator) |
| **D15** | **A** | Distributed tracing only correlates when W3C/trace context is propagated across hops. | [OpenTelemetry enable](https://learn.microsoft.com/en-us/azure/azure-monitor/app/opentelemetry-enable) |
| **D16** | **A** | Soft-delete (and purge protection) is the Key Vault recovery control for accidental deletion. | [Key Vault soft-delete](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview) |
| **D17** | **B** | App Configuration is the skills-measured store for app configuration / feature-style toggles. | [AI-200 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-200); [Feature flags](https://learn.microsoft.com/en-us/azure/azure-app-configuration/concept-feature-management) |
| **D18** | **A** | Realistic KQL against `exceptions` (or similar) is what the monitoring skill tests. | [KQL](https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/); [Application Insights query examples](https://learn.microsoft.com/en-us/azure/azure-monitor/app/analytics-using-kusto) |
| **D19** | **B** | `DefaultAzureCredential` is the documented identity chain for local + Azure with managed identity. | [Azure Identity / DefaultAzureCredential](https://learn.microsoft.com/en-us/python/api/overview/azure/identity-readme); [Key Vault references Python](https://learn.microsoft.com/en-us/azure/azure-app-configuration/use-key-vault-references-python-provider) |
| **D20** | **A** | KQL needs data in Log Analytics; diagnostic settings / platform Log Analytics integration is how logs arrive. | [Diagnostic settings](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/diagnostic-settings); [Container Apps log monitoring](https://learn.microsoft.com/en-us/azure/container-apps/log-monitoring) |

#### Topic D — explanations (11–20)

- **D11:** Rotation without refresh leaves workers on old credentials — failures look like “Key Vault is broken” when the app cached v1.
- **D12:** Same key name + different labels is the clean multi-environment pattern for App Configuration.
- **D13:** Sentinel-key refresh is the usual exam-friendly story for “change config without redeploy.”
- **D14:** Know basic KQL shape: filter → summarize by bin → render/sort. That’s the measured skill, not portal clicking alone.
- **D15:** Broken distributed traces almost always mean missing context propagation between API → queue → worker → model call.
- **D16:** Soft-delete is on by default for newer vaults; purge protection blocks permanent purge — production hardening.
- **D17:** Don’t bake feature flags into images; App Configuration is the skills-aligned dynamic settings service.
- **D18:** Be ready to recognize a correct KQL sketch vs nonsense commands.
- **D19:** Avoid keys in code; `DefaultAzureCredential` matches Entra ID / managed identity guidance end-to-end.
- **D20:** You can’t query what you never collected — wire diagnostics before writing KQL in an incident.

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
