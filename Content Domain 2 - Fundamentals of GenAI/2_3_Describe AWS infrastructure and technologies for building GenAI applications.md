# AIF-C01 | Task 2.3: AWS Infrastructure and Technologies for Building GenAI Applications

---

## 1. AWS Services and Features for GenAI Development

AWS provides a layered portfolio of GenAI services — from fully managed no-code tools to flexible ML platforms — so builders at every skill level can develop GenAI applications.

---

### Amazon Bedrock
- AWS's **core managed GenAI platform** providing access to a wide selection of foundation models via a single, unified API.
- **Key features**:
  - Access to models from Anthropic (Claude), Meta (Llama), Mistral, Amazon (Titan), Cohere, Stability AI, and more.
  - **Amazon Bedrock Knowledge Bases**: Managed RAG pipeline — ingest documents, auto-embed, store vectors, retrieve at query time.
  - **Amazon Bedrock Agents**: Build multi-step agentic workflows with tool use and knowledge retrieval.
  - **Amazon Bedrock Guardrails**: Apply safety filters — block harmful content, PII redaction, topic denial, grounding checks.
  - **Amazon Bedrock Model Evaluation**: Compare and evaluate FM performance automatically or with human reviewers.
  - **Fine-tuning**: Customize supported FMs on your own labeled data.
  - **Continued Pre-training**: Extend FM knowledge with unlabeled domain data.
  - **Prompt Management**: Save, version, and share prompt templates across teams.
- **Who uses it**: Developers building GenAI-powered applications on AWS.

---

### Amazon SageMaker JumpStart
- A feature within **Amazon SageMaker** that provides a **model hub** with hundreds of pre-trained, open-source FMs and ML models ready to deploy with one click.
- **Key capabilities**:
  - Browse, deploy, and fine-tune models from providers like Hugging Face, Meta, Mistral, and more.
  - Pre-built solution templates for common ML use cases.
  - Fine-tune models on custom data using SageMaker's managed training infrastructure.
  - Deploy models to SageMaker real-time or batch inference endpoints.
- **Difference from Bedrock**: JumpStart gives you access to open-source models you host yourself on SageMaker compute; Bedrock provides serverless access to models managed by AWS.
- **Who uses it**: ML practitioners who want more control over model hosting, fine-tuning, and infrastructure.

> 💡 **Exam Tip**: **SageMaker JumpStart** = model hub for open-source models with hands-on infrastructure control. **Amazon Bedrock** = fully managed, serverless FM access via API. If the scenario mentions "deploy an open-source model with control over compute," think JumpStart.

---

### Amazon Bedrock PartyRock
- A **no-code, playground-style application** built on Amazon Bedrock for experimenting with GenAI.
- Allows anyone — including non-developers — to build and share GenAI-powered apps visually.
- **Key features**:
  - Build multi-widget apps by chaining FM prompts (text generation, image generation, chatbots).
  - No AWS account required — accessible via a web browser.
  - Share apps publicly with a shareable link.
  - Great for prototyping, demos, and learning GenAI concepts.
- **Who uses it**: Business users, students, non-technical builders exploring GenAI.

> 💡 **Exam Tip**: PartyRock = **no-code GenAI experimentation**. If a question describes a non-developer or someone with no ML expertise wanting to quickly try out GenAI, PartyRock is the answer.

---

### Amazon Q
- AWS's family of **GenAI-powered assistants** tailored for specific business and developer use cases.
- Powered by Amazon Bedrock under the hood.

**Amazon Q variants:**

| Product | Purpose | Primary Users |
|---|---|---|
| **Amazon Q Business** | Enterprise AI assistant that answers questions from company data (connected to internal docs, wikis, Salesforce, S3, etc.) | Business users, employees |
| **Amazon Q Developer** | AI coding assistant for generating, explaining, debugging, and refactoring code; also handles AWS-specific questions | Developers, DevOps |
| **Amazon Q in QuickSight** | Natural language querying and data story generation within Amazon QuickSight dashboards | Business analysts |
| **Amazon Q in Connect** | Real-time AI assistance for customer service agents in Amazon Connect contact centers | Customer service agents |

- **Key differentiator**: Amazon Q is a **purpose-built business AI assistant**, not a general-purpose FM API. It is pre-integrated with enterprise data sources and AWS services.

> 💡 **Exam Tip**: **Amazon Q Business** = enterprise knowledge assistant (connects to company docs). **Amazon Q Developer** = coding assistant for developers. Know both variants for the exam.

---

### Amazon Bedrock Data Automation
- A feature within Amazon Bedrock that uses AI to **automatically extract, transform, and structure information from unstructured data** (documents, images, video, audio).
- Formerly related to capabilities in Amazon Textract and expanded with GenAI.
- **Key capabilities**:
  - Extract structured data from PDFs, forms, tables, images, and media files.
  - Automate document processing pipelines (invoices, contracts, medical forms).
  - Enrich unstructured data for downstream analytics, RAG indexing, or storage.
- **Use cases**: Intelligent document processing, media analysis, automated data pipelines.
- **Who uses it**: Developers building document automation or media analysis workflows.

---

### Other Relevant AWS GenAI Services

| Service | What It Does | Use Case |
|---|---|---|
| **Amazon Titan** | AWS's own family of FMs (text, embeddings, image) available on Bedrock | General text generation, embeddings for RAG, image generation |
| **Amazon CodeWhisperer** (now Amazon Q Developer) | AI coding assistant integrated in IDEs | Code generation, completion, security scanning |
| **AWS Trainium** | Custom ML training chip optimized for deep learning | Cost-efficient large-scale model training |
| **AWS Inferentia** | Custom ML inference chip for low-cost, high-throughput inference | Reducing inference costs for deployed models |
| **Amazon Kendra** | Intelligent enterprise search with ML | Semantic search over enterprise documents |
| **Amazon Personalize** | Managed ML service for real-time personalization and recommendations | Recommendation engines |
| **Amazon Rekognition** | Computer vision AI service | Image/video analysis, facial recognition, content moderation |

---

## 2. Advantages of Using AWS GenAI Services

### Accessibility
- FMs are accessible via **simple API calls** — no need to manage servers, GPU clusters, or ML frameworks.
- Amazon Bedrock provides a **unified API** to access models from multiple providers.
- Console-based tools (Bedrock Playground, PartyRock) allow experimentation without writing code.
- **Business value**: Any developer — regardless of ML expertise — can integrate GenAI into applications.

### Lower Barrier to Entry
- Pre-trained FMs eliminate the need to collect massive datasets, build model architectures, or run expensive training jobs.
- Managed services (Bedrock, SageMaker JumpStart) handle infrastructure, scaling, and model management.
- **Business value**: Startups and small teams can leverage the same powerful models as large enterprises without equivalent investment.

### Efficiency
- **Operational efficiency**: AWS handles patching, scaling, monitoring, and fault tolerance — teams focus on building, not managing.
- **Development efficiency**: Pre-built integrations (Bedrock ↔ S3, Lambda, CloudWatch) reduce integration time.
- Prompt Management, Knowledge Bases, and Agents reduce custom code needed for common GenAI patterns.
- **Business value**: Faster development cycles with less engineering overhead.

### Cost-Effectiveness
- **Pay-per-use pricing**: Only pay for tokens consumed (no idle infrastructure costs).
- **No upfront investment**: No need to buy or lease GPU hardware.
- Access to a range of models — choose smaller, cheaper models for simpler tasks; larger models only when needed.
- AWS Trainium and Inferentia chips offer lower-cost training and inference vs. standard GPU instances.
- **Business value**: Aligns cost directly to usage; scales economically from prototype to production.

### Speed to Market
- Start building GenAI applications **in minutes** using pre-trained FMs on Bedrock.
- Managed services remove the months of infrastructure setup, model training, and MLOps work.
- Solution templates and example architectures (via SageMaker JumpStart, AWS reference architectures) further accelerate development.
- **Business value**: Competitive advantage from deploying features faster than building from scratch.

### Ability to Meet Business Objectives
- AWS services provide enterprise-grade **reliability, scalability, and integrations** with existing AWS infrastructure.
- Compliance certifications (HIPAA, SOC 2, FedRAMP, GDPR) allow GenAI applications to be deployed in regulated industries.
- Guardrails, monitoring, and audit logging ensure responsible use aligned with governance requirements.
- **Business value**: GenAI can be deployed with the trust, security, and compliance needed for enterprise adoption.

---

## 3. Benefits of AWS Infrastructure for GenAI Applications

### Security
- **Data encryption**: All data encrypted at rest (AES-256) and in transit (TLS).
- **Network isolation**: Deploy within a **VPC (Virtual Private Cloud)** to prevent data from traversing the public internet.
- **IAM (Identity and Access Management)**: Fine-grained access control over who can call which models and access which data.
- **Private endpoints (AWS PrivateLink)**: Access Bedrock and other services privately without internet exposure.
- **Key Management (AWS KMS)**: Customer-managed encryption keys for full control over data protection.
- **Amazon Bedrock specific**: Your prompts and model outputs are **not used to train AWS models** — data is not shared across customers.

### Compliance
- AWS maintains certifications across global standards:

| Standard | Coverage |
|---|---|
| **HIPAA** | Healthcare data (US) |
| **SOC 1, 2, 3** | Security, availability, confidentiality |
| **ISO 27001 / 27017 / 27018** | Information security |
| **FedRAMP** | US federal government |
| **GDPR** | EU data privacy |
| **PCI DSS** | Payment card data |

- **AWS Artifact**: Provides on-demand access to compliance reports and certifications.
- **Data residency**: Regional deployment options allow data to remain within required geographic boundaries.
- **CloudTrail logging**: Full audit trail of all API calls for compliance and forensic analysis.

### Responsibility (Shared Responsibility Model)
- AWS and the customer share responsibility for security:

```
┌──────────────────────────────────────────────┐
│              CUSTOMER Responsibility          │
│  - Data content and classification           │
│  - Application security                      │
│  - Identity and access management (IAM)      │
│  - Prompt design and output validation       │
│  - Compliance with data usage policies       │
└──────────────────────────────────────────────┘
┌──────────────────────────────────────────────┐
│               AWS Responsibility              │
│  - Physical infrastructure security         │
│  - Hypervisor and virtualization security    │
│  - Managed service patching and updates      │
│  - Foundation model security                 │
│  - Global network infrastructure             │
└──────────────────────────────────────────────┘
```

- In the GenAI context: AWS secures the FM infrastructure; customers are responsible for responsible use, data governance, and application-level safety.

### Safety (Responsible AI)
- **Amazon Bedrock Guardrails**: Apply configurable safety controls:
  - **Content filters**: Block harmful, toxic, or inappropriate content (violence, hate speech, adult content).
  - **Denied topics**: Prevent the model from discussing specific off-limits subjects.
  - **PII redaction**: Automatically detect and mask personally identifiable information.
  - **Grounding checks**: Detect and reduce hallucinations by verifying responses against retrieved context.
  - **Word filters**: Block specific words or phrases.
- **Model cards**: Transparency documentation on model capabilities, limitations, and intended use.
- **AWS Responsible AI principles**: Fairness, explainability, privacy, robustness, transparency, and governance.

> 💡 **Exam Tip**: For any exam question about **safety, content filtering, or blocking harmful outputs** in an AWS GenAI application → the answer is **Amazon Bedrock Guardrails**.

---

## 4. Cost Tradeoffs of AWS GenAI Services

Understanding cost tradeoffs helps select the right deployment model for a given use case.

---

### Token-Based Pricing
- Most FM APIs on Bedrock charge **per token** (input tokens + output tokens).
- **Tradeoffs**:
  - Longer prompts = higher cost per request.
  - More capable (larger) models cost more per token.
  - Efficient prompt engineering directly reduces cost.
- **Cost optimization**:
  - Use **prompt caching** to avoid reprocessing repeated prompt prefixes.
  - Minimize unnecessary tokens in prompts (concise prompts = lower cost).
  - Use smaller/cheaper models for simpler subtasks.

---

### Provisioned Throughput
- Purchase a **dedicated amount of model processing capacity** (measured in Model Units) for a fixed time period.
- **When to use**: High, consistent traffic where on-demand pricing would be more expensive.
- **Tradeoffs**:

| Aspect | On-Demand | Provisioned Throughput |
|---|---|---|
| **Cost structure** | Pay per token, no commitment | Fixed hourly rate, regardless of usage |
| **Best for** | Variable/unpredictable traffic | High, consistent traffic |
| **Availability** | Shared capacity, may be throttled | Dedicated capacity, predictable performance |
| **Commitment** | None | 1-month or 6-month term |

> 💡 **Exam Tip**: Provisioned Throughput = **reserved capacity for predictable, high-volume workloads**. On-demand = **pay-as-you-go for variable or low workloads**.

---

### Responsiveness vs. Cost
- Larger, more capable models produce higher-quality outputs but have **higher latency and cost**.
- Smaller models are **faster and cheaper** but may sacrifice quality.
- **Tradeoff strategy**:
  - Simple queries → small/fast model.
  - Complex reasoning → larger model.
  - Use **prompt routing** to automatically direct requests to the right-sized model.

---

### Availability and Redundancy
- **Multi-region deployment**: Deploy across AWS regions for higher availability and disaster recovery.
- **Cost tradeoff**: Multi-region increases infrastructure cost but improves fault tolerance and meets data residency needs.
- **Cross-region inference (Bedrock)**: Automatically routes requests to available capacity in other regions during peak demand — improves availability at potential latency cost.

---

### Performance vs. Cost
- **Higher performance** (lower latency, higher throughput) typically requires:
  - Provisioned throughput (vs. on-demand).
  - Deployment in the same region as the application.
  - Smaller models optimized for speed.
- **Cost optimization options**:
  - **Batch inference**: Process large volumes asynchronously at lower cost than real-time endpoints.
  - **AWS Inferentia**: Cheaper inference chips vs. standard GPU instances for SageMaker-hosted models.
  - **Model distillation**: Use a smaller distilled model at a fraction of the cost.

---

### Regional Coverage
- Not all models are available in all AWS regions.
- Deploying in a region closer to users reduces latency but may limit model selection.
- **Cost tradeoff**: Data transfer costs may apply if the model region differs from the application region.
- **Compliance tradeoff**: Some regions are required for data residency; limited model availability in those regions may require compromises.

---

### Custom Models
- Fine-tuned or continuously pre-trained custom models have **additional costs**:
  - **Training job cost**: Compute time × instance type × training hours.
  - **Model storage cost**: Storing fine-tuned model weights.
  - **Dedicated deployment**: Custom models may require provisioned throughput (cannot use shared on-demand capacity).
- **Tradeoff**: Higher upfront cost, but better task-specific accuracy → potentially lower cost per correct output and fewer retries.

---

### Cost Tradeoff Summary

| Factor | Lower Cost Option | Higher Cost Option | Key Tradeoff |
|---|---|---|---|
| **Model size** | Small/cheap model | Large/capable model | Cost vs. quality |
| **Pricing model** | On-demand (token-based) | Provisioned throughput | Variable vs. fixed |
| **Inference type** | Batch inference | Real-time inference | Latency vs. cost |
| **Customization** | Prompting / RAG | Fine-tuning / pre-training | Cost vs. specialization |
| **Availability** | Single region | Multi-region | Cost vs. resilience |
| **Compute** | AWS Inferentia | GPU instances | Cost vs. flexibility |
| **Prompt length** | Short, optimized prompts | Long, detailed prompts | Cost vs. context richness |

---

## 5. AWS GenAI Service Selection Guide

| Scenario | Recommended Service |
|---|---|
| Access multiple FMs via a single API | Amazon Bedrock |
| Non-developer wants to prototype a GenAI app | Amazon Bedrock PartyRock |
| Deploy and fine-tune an open-source model with infrastructure control | Amazon SageMaker JumpStart |
| Build an enterprise Q&A assistant over company documents | Amazon Q Business |
| AI coding assistant for developers | Amazon Q Developer |
| Build a multi-step agentic workflow | Amazon Bedrock Agents |
| Add safety filters and content moderation to FM outputs | Amazon Bedrock Guardrails |
| Extract structured data from documents/images | Amazon Bedrock Data Automation |
| Compare and evaluate multiple FMs | Amazon Bedrock Model Evaluation |
| Reduce inference costs for high-volume models | AWS Inferentia |
| High-volume, consistent FM traffic requiring dedicated capacity | Bedrock Provisioned Throughput |

---

## 6. Exam Tips Recap

- ✅ **Amazon Bedrock** = unified managed FM API. **SageMaker JumpStart** = open-source model hub with infrastructure control.
- ✅ **PartyRock** = no-code GenAI playground, no AWS account needed — for non-developers.
- ✅ **Amazon Q Business** = enterprise knowledge assistant. **Amazon Q Developer** = coding assistant.
- ✅ **Bedrock Guardrails** = safety and content filtering for GenAI apps (harmful content, PII, denied topics).
- ✅ **Advantages of AWS GenAI**: accessibility, lower barrier, efficiency, cost-effectiveness, speed to market, compliance.
- ✅ **Your prompts are NOT used to train AWS models** on Bedrock — key security/privacy point.
- ✅ **Provisioned Throughput** = reserved capacity for predictable high-volume traffic. **On-demand** = pay-per-token for variable traffic.
- ✅ **Token-based pricing** means prompt length directly impacts cost — shorter, efficient prompts save money.
- ✅ **Shared Responsibility Model**: AWS secures the infrastructure; customers are responsible for data, prompts, and application safety.
- ✅ **Cross-region inference** on Bedrock improves availability but may add latency — an availability vs. performance tradeoff.
- ✅ **AWS Inferentia** reduces inference costs; **AWS Trainium** reduces training costs — both are custom ML chips.