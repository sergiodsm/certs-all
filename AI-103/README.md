# MS AI-103 Certification

**Exam:** Developing AI Apps and Agents on Azure  
**Source:** [Study guide for Exam AI-103](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-103)  
**Skills measured as of:** April 16, 2026  
**Passing score:** 700+

## Study materials

| Resource | Description |
| --- | --- |
| [study-guides/](./study-guides/) | Deep-dive study guide per exam section |
| [practice/](./practice/) | 10-question mock tests per section (50 total) |

| Section | Study guide | Mock test |
| --- | --- | --- |
| 1. Plan and manage (25–30%) | [01-plan-manage.md](./study-guides/01-plan-manage.md) | [domain-1-questions.md](./practice/domain-1-questions.md) |
| 2. Generative AI & agents (30–35%) | [02-generative-agentic.md](./study-guides/02-generative-agentic.md) | [domain-2-questions.md](./practice/domain-2-questions.md) |
| 3. Computer vision (10–15%) | [03-computer-vision.md](./study-guides/03-computer-vision.md) | [domain-3-questions.md](./practice/domain-3-questions.md) |
| 4. Text analysis (10–15%) | [04-text-analysis.md](./study-guides/04-text-analysis.md) | [domain-4-questions.md](./practice/domain-4-questions.md) |
| 5. Information extraction (10–15%) | [05-information-extraction.md](./study-guides/05-information-extraction.md) | [domain-5-questions.md](./practice/domain-5-questions.md) |

## Audience profile

Azure AI engineer who builds, manages, and deploys agents and AI solutions using **Microsoft Foundry**.

**Prerequisites / familiarity:**
- Developing apps with **Python**
- General AI, generative AI, and Azure services

**Responsibilities:**
- Planning and managing Azure AI solutions
- Implementing generative AI and agentic solutions
- Implementing computer vision solutions
- Implementing text analysis solutions
- Implementing information extraction solutions

---

## Skills at a glance

| Domain | Weight |
| --- | --- |
| Plan and manage an Azure AI solution | 25–30% |
| Implement generative AI and agentic solutions | 30–35% |
| Implement computer vision solutions | 10–15% |
| Implement text analysis solutions | 10–15% |
| Implement information extraction solutions | 10–15% |

---

## 1. Plan and manage an Azure AI solution (25–30%)

### 1.1 Choose the appropriate Foundry services for generative AI and agents

- Choose an appropriate model for each task (LLMs, small language models, multimodal models, Foundry Tools)
- Choose the appropriate Foundry services for generative tasks, grounding, vector search, agent workflows, or multimodal processing
- Choose an appropriate method for retrieval and indexing
- Choose appropriate memory, tool, and knowledge integration services for agent solutions

### 1.2 Set up AI solutions in Foundry

- Design Azure infrastructure for AI apps and agent-based solutions
- Choose appropriate deployment options
- Configure model and agent deployments
- Integrate Foundry projects with CI/CD pipelines

### 1.3 Manage, monitor, and secure AI systems

- Manage quotas, scaling, rate limits, and cost footprints for model and agent workloads
- Monitor model performance, drift, safety events, and grounding quality
- Monitor data ingestion quality, search index health, and relevance performance
- Configure security (managed identity, private networking, keyless credentials, role policies)

### 1.4 Implement responsible AI across generative AI and agentic systems

- Configure safety filters, guardrails, risk detection, and content moderation
- Apply responsible AI instrumentation (evaluators, safety evaluations, explanation tooling)
- Implement auditing (trace logging, provenance metadata, approval workflows)
- Govern agent behavior (oversight modes, constraints, tool-access controls)

---

## 2. Implement generative AI and agentic solutions (30–35%)

### 2.1 Build generative applications by using Foundry

- Deploy and consume LLMs, small models, code models, and multimodal models
- Implement retrieval-augmented generation (RAG) in an application
- Design workflows, tool-augmented flows, and multistep reasoning pipelines
- Evaluate models and apps (fabrications, relevance, quality, safety)
- Integrate generative workflows using Foundry SDKs and connectors
- Configure an application to connect to a Foundry project

### 2.2 Build agents by using Foundry

- Define agent roles, goals, conversation-tracking approach, and tool schemas
- Build agents that integrate retrieval, function-calling, and conversation memory
- Integrate agent tools (APIs, knowledge stores, search, content understanding, custom functions)
- Implement orchestrated multi-agent solutions
- Build autonomous or semiautonomous workflows with safeguards and approval flow controls
- Integrate monitoring into deployed agents; evaluate agent behavior and perform error analysis

### 2.3 Optimize and operationalize generative AI systems

- Tune generation behavior (prompt engineering, model parameters)
- Implement model reflection, chain-of-thought evaluations, and self-critique loops
- Set up observability (tracing, token analytics, safety signals, latency breakdowns)
- Orchestrate multiple models, flows, or hybrid LLM and rules engines

---

## 3. Implement computer vision solutions (10–15%)

### 3.1 Design and implement image- and video-generation solutions

- Generate images from text prompts and reference media
- Generate videos from text prompts and reference media
- Configure image-editing workflows (inpainting, mask-based edits, prompt-driven modifications)
- Implement workflows to edit generated videos
- Select and apply appropriate generation and editing controls

### 3.2 Design and implement multimodal understanding workflows

- Analyze visual context using multimodal models
- Produce concise or detailed captions for single or multiple images
- Enable question-answering grounded in visual evidence
- Generate alt-text and extended image descriptions for accessibility
- Configure Azure Content Understanding in Foundry Tools to extract visual characteristics
- Implement video analysis workflows for video segments
- Configure single-task and pro-mode Content Understanding pipelines
- Identify objects, components, or regions within images or video

### 3.3 Implement responsible AI for multimodal content

- Filter unsafe or disallowed visual content
- Detect and mitigate indirect prompt injection via embedded text in images
- Enforce visual policy rules (watermarks, prohibited symbols, brand usage, inappropriate content)

---

## 4. Implement text analysis solutions (10–15%)

### 4.1 Apply language model text analysis

- Extract entities, topics, summaries, and structured JSON outputs (generative prompting and Foundry Tools)
- Detect sentiment, tone, safety issues, and sensitive content
- Translate text (Azure Translator in Foundry Tools or LLM-powered translation flows)
- Customize language model outputs for domain tasks (compliance summarization, domain extraction)

### 4.2 Implement speech solutions

- Convert speech to text and text to speech for agentic interactions
- Integrate speech as an agent modality, including custom speech models
- Enable multimodal reasoning from audio inputs
- Translate speech into other languages (language models and Foundry Tools)

---

## 5. Implement information extraction solutions (10–15%)

### 5.1 Build retrieval and grounding pipelines

- Ingest and index content (documents, images, audio, video)
- Configure semantic search, hybrid search, and vector search for grounding
- Implement enrichment with custom or built-in skills (text, images, layout)
- Configure RAG ingestion flow (documents + OCR)
- Connect retrieval pipelines to workflows and agent tools

### 5.2 Extract content from documents

- Extract information with multimodal pipelines (OCR, layout analysis, field extraction)
- Produce clean, grounded representations for agents and RAG using Content Understanding
- Implement analyzers for structured or markdown outputs for downstream reasoning (Content Understanding)

---

## Study resources

| Resource | Link |
| --- | --- |
| Official study guide | https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ai-103 |
| Training options | https://learn.microsoft.com/en-us/credentials/certifications/exams/AI-103#two-ways-to-prepare |
| Azure AI services | https://learn.microsoft.com/en-us/azure/ai-services/ |
| Azure AI Vision | https://learn.microsoft.com/en-us/azure/cognitive-services/computer-vision/ |
| Azure AI Video Indexer | https://learn.microsoft.com/en-us/azure/azure-video-indexer/ |
| Azure AI Language | https://learn.microsoft.com/en-us/azure/ai-services/language-service/ |
| Azure AI Speech | https://learn.microsoft.com/en-us/azure/ai-services/speech-service/ |
| Azure AI Search | https://learn.microsoft.com/en-us/azure/search/ |
| Azure OpenAI | https://learn.microsoft.com/en-us/azure/ai-services/openai/ |
| Azure AI Document Intelligence | https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/ |
| Exam sandbox | https://aka.ms/examdemo |

**Notes from Microsoft:**
- Bullets illustrate how skills are assessed; related topics may also appear.
- Most questions cover GA features; Preview features may appear if commonly used.
