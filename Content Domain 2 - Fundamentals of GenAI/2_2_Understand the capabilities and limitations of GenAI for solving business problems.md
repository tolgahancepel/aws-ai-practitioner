# AIF-C01 | Task 2.2: Capabilities and Limitations of GenAI for Solving Business Problems

---

## 1. Advantages of Generative AI

GenAI offers a unique set of advantages that make it well-suited for a broad range of business applications — advantages that traditional software and rule-based systems cannot match.

---

### Adaptability
- GenAI models can **handle a wide variety of tasks** without being explicitly reprogrammed for each one.
- The same base model can summarize, translate, write code, answer questions, and generate images — all from natural language instructions.
- Models can be **adapted to new domains** through prompting, RAG, or fine-tuning without rebuilding from scratch.
- **Business value**: Reduces the need to build and maintain separate systems for different tasks.

**Examples of adaptability:**
- A single LLM deployed as a customer service agent, an internal knowledge assistant, AND a code reviewer.
- Switching a model's behavior from formal to casual simply by changing the prompt.
- Adding a new product line to a support bot by updating the knowledge base (RAG) — no retraining needed.

---

### Responsiveness
- GenAI systems can **generate responses in real time** to dynamic, open-ended user inputs.
- Unlike rule-based systems (which only handle pre-defined scenarios), GenAI can respond to **novel, unanticipated queries**.
- Enables **natural language interfaces** — users interact in plain language rather than structured menus.
- Scales responsiveness across millions of simultaneous users without proportional staffing increases.
- **Business value**: Dramatically improves user experience by enabling fluid, human-like interactions at scale.

**Examples of responsiveness:**
- A chatbot that handles any customer question — not just FAQs.
- Real-time code suggestions in an IDE as the developer types.
- Instant document summaries on demand without a pre-built template.

---

### Simplicity
- GenAI abstracts away complexity — users interact via **natural language** rather than structured queries, code, or complex interfaces.
- Democratizes access to powerful capabilities: non-technical users can query databases, generate reports, and analyze data using plain English.
- Reduces the need for specialized expertise in narrow tools (SQL, Excel formulas, coding) for common tasks.
- **Business value**: Lowers the skill barrier, increases user adoption, and broadens who can benefit from AI.

**Examples of simplicity:**
- "Show me last quarter's top 10 customers by revenue" → LLM generates and runs the SQL query.
- Non-developers using Amazon Q to explore data without knowing query syntax.
- Dragging and dropping documents to get instant AI-generated summaries.

---

### Other Key Advantages

| Advantage | Description |
|---|---|
| **Scalability** | Serve millions of users simultaneously with consistent quality, no human bottleneck |
| **Creativity** | Generate novel content — writing, images, code, designs — that would require significant human effort |
| **Speed** | Produce outputs in seconds that would take humans hours (reports, summaries, translations) |
| **Personalization** | Tailor content and responses to individual users at scale |
| **Multilingual capability** | Understand and generate content in dozens of languages without separate systems |
| **Cross-domain knowledge** | A single FM has knowledge across science, law, medicine, finance, code, and more |
| **Continuous improvement** | Models can be updated with new data and feedback without rebuilding from scratch |

---

## 2. Disadvantages and Limitations of GenAI

Understanding where GenAI falls short is just as important as knowing where it excels — and is heavily tested on the exam.

---

### Hallucinations
- **Definition**: The model generates **plausible-sounding but factually incorrect or fabricated information** with confidence.
- Hallucinations occur because LLMs generate text based on statistical patterns, not verified facts — they predict likely next tokens, not truth.
- **Types of hallucinations**:
  - **Factual hallucination**: Inventing false facts ("The Eiffel Tower was built in 1750.")
  - **Source hallucination**: Citing non-existent papers, books, or URLs.
  - **Intrinsic hallucination**: Contradicting the provided context.
  - **Extrinsic hallucination**: Adding information not supported by context.
- **Business risk**: Incorrect medical advice, fabricated legal citations, wrong financial figures.
- **Mitigations**:
  - RAG (ground responses in retrieved factual sources).
  - Prompt engineering (instruct the model to say "I don't know" when uncertain).
  - Output verification and human-in-the-loop review.
  - Amazon Bedrock Guardrails for factual grounding checks.

> 💡 **Exam Tip**: Hallucination is the **most commonly tested limitation** of GenAI. The primary mitigation is **RAG** — grounding responses in retrieved, verified documents.

---

### Interpretability (Explainability)
- **Definition**: It is **difficult or impossible to understand *why* a model produced a specific output** — models are often "black boxes."
- LLMs have billions of parameters and complex, non-linear computations — there is no simple rule to trace.
- **Business risk**: Cannot easily audit decisions for compliance, legal challenges, or debugging.
- **Impact areas**: Regulated industries (healthcare, finance, legal) where decisions must be explainable.
- **Mitigations**:
  - Chain-of-thought prompting (makes reasoning visible in the output).
  - LIME, SHAP, or other explainability tools applied at the output level.
  - Human-in-the-loop review for high-stakes decisions.
  - Use simpler, inherently interpretable ML models for high-stakes regulated decisions.

---

### Inaccuracy
- **Definition**: Beyond hallucinations, GenAI models may produce outputs that are **imprecise, incomplete, or out-of-date**.
- Causes:
  - **Training data cutoff**: Model knowledge ends at a fixed point in time.
  - **Domain gaps**: General FMs may lack depth in highly specialized areas.
  - **Ambiguous prompts**: Vague instructions lead to vague answers.
  - **Context window limitations**: Long documents may be truncated, causing missed context.
- **Mitigations**:
  - RAG to inject up-to-date information.
  - Fine-tuning for domain specialization.
  - Clear, specific prompt engineering.
  - Human review for critical outputs.

---

### Nondeterminism
- **Definition**: Given the **same input, a GenAI model may produce different outputs** on different runs.
- Caused by temperature and sampling parameters introducing randomness into token selection.
- **Business risk**: Inconsistent user experiences, unreliable automated pipelines, difficulty in testing and debugging.
- **Mitigations**:
  - Set **temperature = 0** for deterministic (or near-deterministic) outputs.
  - Use fixed **random seeds** where supported.
  - Design systems to tolerate output variation (e.g., validate outputs programmatically).

> 💡 **Exam Tip**: Nondeterminism is why you can't always rely on a model to give the exact same answer twice. Setting **temperature to 0** minimizes (but may not fully eliminate) variation.

---

### Other Key Limitations

| Limitation | Description | Mitigation |
|---|---|---|
| **High Cost** | LLM inference and training can be expensive at scale | Prompt caching, smaller models, batch inference |
| **Latency** | Generating long responses takes time — may not meet real-time SLAs | Streaming, smaller models, prompt optimization |
| **Bias** | Models inherit biases from training data, producing unfair or stereotyped outputs | Diverse training data, RLHF, bias auditing, guardrails |
| **Privacy risks** | Models may memorize and reproduce sensitive training data | Data sanitization, PII redaction, access controls |
| **Intellectual property concerns** | Generated content may resemble or reproduce copyrighted material | Legal review, content filtering, guardrails |
| **Context window limits** | Cannot process arbitrarily long documents in one request | Chunking, RAG, summarization pipelines |
| **Prompt sensitivity** | Small changes in wording can drastically change output quality | Prompt templates, testing, versioning |
| **No real-time knowledge** | Base models have a training cutoff and don't know recent events | RAG, web search integration |

---

### Advantages vs. Disadvantages Summary

| ✅ Advantages | ❌ Disadvantages |
|---|---|
| Adaptability across tasks | Hallucinations (fabricated facts) |
| Real-time responsiveness | Poor interpretability / black box |
| Simplicity of natural language interface | Inaccuracy and outdated knowledge |
| Scale and speed | Nondeterminism (inconsistent outputs) |
| Cross-domain knowledge | Bias inherited from training data |
| Creativity and content generation | High cost at scale |
| Multilingual capability | Privacy and IP risks |

---

## 3. Factors to Consider When Selecting GenAI Models

Selecting the right FM for a business application requires evaluating multiple dimensions — not just capability.

---

### Model Types
- Match the **model architecture and modality** to the task:

| Task | Model Type |
|---|---|
| Text generation, Q&A, summarization | Text-to-text LLM (decoder-only) |
| Image generation | Diffusion model (Stable Diffusion, Titan Image) |
| Visual understanding (image + text input) | Multimodal model (Claude 3, GPT-4V) |
| Speech recognition | ASR model (Amazon Transcribe) |
| Text-to-speech | TTS model (Amazon Polly) |
| Semantic search / RAG | Embedding model (Titan Embeddings) |
| Translation | NMT model (Amazon Translate) |

---

### Performance Requirements
- **Accuracy**: Does the model meet the minimum acceptable quality threshold for the task?
- **Latency**: What is the maximum acceptable response time? (Real-time chat vs. batch processing)
- **Throughput**: How many requests per second must the system handle?
- **Context window**: Is the model's context window large enough for the input documents?
- **Output length**: Can the model generate outputs of the required length?

---

### Capabilities
- **Task-specific strengths**: Some models excel at reasoning, others at coding, creative writing, or instruction-following.
- **Multilingual support**: How many languages does the model support, and at what quality?
- **Tool/function calling**: Can the model call external APIs or tools (needed for agents)?
- **Fine-tuning support**: Can the model be customized? Does the provider allow it?
- **Prompt caching**: Does the model/platform support caching repeated prompt prefixes?
- **Multimodal input/output**: Does the task require image, audio, or video processing?

---

### Constraints
- **Budget**: Cost per token for input and output; training/fine-tuning costs.
- **Infrastructure**: On-premises, cloud, or edge deployment requirements.
- **Model size**: Larger models have higher memory/compute requirements.
- **Latency SLAs**: Time-sensitive applications need faster (often smaller) models.
- **Data residency**: Must data stay within a specific geographic region?
- **Vendor lock-in**: Are you tied to a single provider's API format?

---

### Compliance
- **Data privacy regulations**: GDPR, HIPAA, CCPA — who processes the data, and where?
- **Industry-specific regulations**: Financial services (SOX), healthcare (HIPAA), government (FedRAMP).
- **Content policies**: Does the model provider's acceptable use policy align with your use case?
- **Auditability**: Can you log and audit all model inputs and outputs for compliance?
- **Data sovereignty**: Does the provider offer deployment within required regions?
- **Model transparency**: Does the provider disclose training data sources and safety practices?

**AWS compliance considerations:**
- Amazon Bedrock is designed with enterprise compliance in mind — supports logging via AWS CloudTrail, VPC isolation, encryption, and regional data residency.
- AWS offers HIPAA-eligible, SOC 2, ISO 27001, and FedRAMP-compliant services.

---

### Model Selection Decision Framework

| Factor | Key Question |
|---|---|
| **Model Type** | What modality does the task require? |
| **Performance** | What are the accuracy, latency, and throughput requirements? |
| **Capabilities** | Does the model support the required features (tool use, multilingual, long context)? |
| **Constraints** | What are the budget, compute, and deployment limitations? |
| **Compliance** | Are there data privacy, regulatory, or auditability requirements? |

> 💡 **Exam Tip**: A question describing a healthcare company needing to process patient records → **compliance (HIPAA)** and **data privacy** should be top selection criteria. A question about a real-time trading system → **latency** is the primary constraint.

---

## 4. Business Value and Metrics for GenAI Applications

Measuring the business impact of GenAI goes beyond technical accuracy — it must be tied to outcomes that matter to the organization.

---

### Cross-Domain Performance
- **Definition**: The ability of a single GenAI model to perform well **across multiple different business functions or domains**.
- A high-performing FM can handle HR, legal, finance, and technical support queries from one deployment.
- **Business value**: Reduces the need to build and maintain separate specialized systems.
- **Metric**: Task success rate measured across diverse domain-specific evaluation sets.

---

### Efficiency
- **Definition**: Reduction in time, cost, or human effort required to complete tasks with GenAI assistance.
- **Metrics**:
  - Time-to-completion per task (with AI vs. without)
  - Cost per output (e.g., cost to generate a support ticket response)
  - FTE (Full-Time Equivalent) hours saved per week
  - Number of tasks automated per unit time
- **Example**: A document review process that took 4 hours manually now takes 15 minutes with AI assistance → 94% time reduction.

---

### Conversion Rate
- **Definition**: The percentage of users or prospects who take a **desired action** (purchase, sign-up, inquiry) as a result of GenAI-powered interactions.
- Commonly used for **e-commerce, marketing, and sales applications**.
- **Metrics**:
  - Click-through rate (CTR) on AI-generated recommendations
  - Purchase conversion from AI product suggestions
  - Lead conversion from AI-powered outreach
- **Example**: An AI-powered product recommender increases add-to-cart rate from 3% to 5% → 67% conversion improvement.

---

### Average Revenue Per User (ARPU)
- **Definition**: Total revenue divided by number of active users — measures the **revenue impact of personalization and engagement** driven by GenAI.
- GenAI-powered personalization (recommendations, dynamic pricing, targeted offers) can increase ARPU.
- **Metrics**:
  - ARPU = Total Revenue / Total Active Users
  - Change in ARPU before vs. after GenAI implementation
- **Example**: Personalized AI recommendations increase average order value from $45 to $62 → ARPU improvement.

---

### Accuracy
- **Definition**: How often the GenAI system produces **correct, relevant, and factually sound outputs** for the intended task.
- Measured differently depending on the application:
  - Classification: precision, recall, F1 score
  - Generation: ROUGE, BLEU, BERTScore, human rating
  - Q&A: Exact match, faithfulness score
  - Code generation: Pass rate on test cases
- **Business relevance**: Inaccurate outputs erode user trust and may cause operational or legal risk.

---

### Customer Lifetime Value (CLV / CLTV)
- **Definition**: The **total predicted revenue** a customer will generate over their entire relationship with a business.
- GenAI can increase CLV through better personalization, proactive customer service, and improved retention.
- **How GenAI impacts CLV**:
  - Churn prediction: Identify at-risk customers and intervene proactively.
  - Personalized retention offers: Generate tailored re-engagement campaigns.
  - Improved support: Resolve issues faster, increasing loyalty.
- **Metric**: CLV = Average Purchase Value × Purchase Frequency × Customer Lifespan

---

### Additional Business Metrics

| Metric | Definition | Relevant GenAI Use Case |
|---|---|---|
| **Customer Satisfaction (CSAT)** | User rating of interaction quality (1–5 scale) | Chatbots, support agents |
| **Net Promoter Score (NPS)** | Likelihood of users recommending the product | AI-powered products overall |
| **First Contact Resolution (FCR)** | % of issues resolved in first interaction | Customer service agents |
| **Escalation Rate** | % of AI interactions requiring human takeover | Chatbots, virtual agents |
| **Adoption Rate** | % of eligible users actively using the AI feature | All GenAI applications |
| **Time-to-Value** | How quickly the solution delivers measurable ROI | GenAI project evaluation |
| **Cost per Interaction** | Total cost divided by number of AI interactions | Chatbots, content generation |
| **Error/Hallucination Rate** | % of outputs containing factual errors | All GenAI applications |

---

### Connecting Metrics to Business Objectives

| Business Objective | Primary Metrics |
|---|---|
| **Reduce operational costs** | Efficiency (time saved), FTE reduction, cost per interaction |
| **Increase revenue** | Conversion rate, ARPU, CLV |
| **Improve customer experience** | CSAT, NPS, FCR, escalation rate |
| **Accelerate product development** | Developer productivity, code generation accuracy |
| **Ensure quality and compliance** | Accuracy, hallucination rate, audit log completeness |
| **Scale operations** | Throughput, adoption rate, cross-domain performance |

> 💡 **Exam Tip**: Know which metrics align to which business goals. Revenue questions → ARPU, conversion rate, CLV. Operational questions → efficiency, FCR, cost per interaction. Quality questions → accuracy, hallucination rate.

---

## 5. Exam Tips Recap

- ✅ **Top 3 advantages**: Adaptability (many tasks), responsiveness (handles novel inputs), simplicity (natural language interface).
- ✅ **Hallucinations** = the #1 GenAI limitation. Primary mitigation = **RAG** (ground responses in facts).
- ✅ **Nondeterminism** = same input, different outputs. Fix: set **temperature = 0**.
- ✅ **Interpretability** = models are black boxes; hard to explain *why* they produced an output.
- ✅ Model selection factors: **model type, performance, capabilities, constraints, compliance** — all five may appear in scenario questions.
- ✅ For regulated industries (healthcare, finance): **compliance and data privacy** are the top selection criteria.
- ✅ For real-time applications: **latency** is the dominant constraint.
- ✅ Business metrics: **ARPU and conversion rate** = revenue. **Efficiency and FCR** = operations. **CSAT and NPS** = experience. **Accuracy and hallucination rate** = quality.
- ✅ **Customer Lifetime Value (CLV)** is increased by better personalization, retention, and churn prevention — all enabled by GenAI.
- ✅ **Cross-domain performance** measures how well one model handles diverse tasks — a key advantage of large FMs over narrow models.