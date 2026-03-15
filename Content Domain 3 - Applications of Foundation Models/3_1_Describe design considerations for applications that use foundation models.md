# AIF-C01 | Task 3.1: Design Considerations for Applications That Use Foundation Models (FMs)

---

## 1. Selecting a Pre-Trained Foundation Model

Choosing the right FM is one of the most important architectural decisions. There is no single "best" model — the right choice depends on your specific use case, constraints, and priorities.

### Key Selection Criteria

| Criterion | What to Consider |
|---|---|
| **Cost** | Larger/more capable models cost more per token. Balance capability vs. budget. |
| **Modality** | Does the model support your data type? (text, image, audio, video, multimodal) |
| **Latency** | How fast must the response be? Smaller models respond faster. |
| **Multi-lingual** | Does the app need to support multiple languages? Check supported languages. |
| **Model Size** | Larger models are more capable but slower and costlier. Smaller models are faster/cheaper but may be less accurate. |
| **Model Complexity** | More complex models handle nuanced tasks better but require more compute. |
| **Customization** | Can the model be fine-tuned? Does the provider allow customization? |
| **Input/Output Length** | What is the context window size? Can it handle long documents or generate long outputs? |
| **Prompt Caching** | Some providers cache prompt prefixes to reduce latency and cost on repeated requests. |

### Modality Guide

| Modality | Use Case | Example Models |
|---|---|---|
| **Text → Text** | Chat, summarization, Q&A, code generation | Claude, Llama, Titan Text |
| **Text → Image** | Image generation from descriptions | Stable Diffusion, Titan Image |
| **Image → Text** | Image captioning, visual Q&A | Claude 3 (multimodal), Llava |
| **Text → Embedding** | Semantic search, RAG | Amazon Titan Embeddings |
| **Text → Speech** | TTS applications | Amazon Polly |
| **Multimodal** | Mixed inputs (text + image) | Claude 3, GPT-4V |

> 💡 **Exam Tip**: Match the **modality** to the task first, then narrow down by cost/latency/context window. A question asking about choosing a model for long document analysis should steer toward **large context window** as a key criterion.

---

## 2. Inference Parameters and Their Effect on Model Responses

Inference parameters control how the model generates its output. Understanding these is critical for tuning model behavior.

### Temperature
- Controls the **randomness / creativity** of the model's output.
- Range: typically **0.0 to 1.0** (some models allow up to 2.0).

| Temperature Value | Behavior | Best For |
|---|---|---|
| **Low (0.0 – 0.3)** | Deterministic, focused, consistent | Factual Q&A, data extraction, classification |
| **Medium (0.4 – 0.7)** | Balanced creativity and coherence | General chat, summarization |
| **High (0.8 – 1.0+)** | Creative, diverse, unpredictable | Brainstorming, creative writing, poetry |

> 💡 **Exam Tip**: **Low temperature = predictable and precise**. **High temperature = creative and varied**. For a legal document summarizer, you'd use low temperature. For a creative story generator, use high temperature.

### Top-P (Nucleus Sampling)
- Controls the **diversity of word choices** by limiting the pool of candidate tokens.
- The model samples from the smallest set of tokens whose combined probability exceeds P.
- **Low Top-P** → fewer choices, more focused output.
- **High Top-P** → wider variety of word choices.

### Top-K
- Limits the model to choosing from the **top K most probable** next tokens.
- **Low K** → more conservative/predictable.
- **High K** → more diverse.

### Input/Output Length
- **Max input tokens**: Defines how much context the model can receive (context window).
- **Max output tokens**: Limits how long the generated response can be.
- Longer outputs = higher cost and latency.
- Setting this too low can **truncate** responses.

### Stop Sequences
- Strings that signal the model to **stop generating** (e.g., `"\n"`, `"END"`).
- Useful for controlling the format of structured outputs.

### Summary of Inference Parameters

| Parameter | Controls | Low Value | High Value |
|---|---|---|---|
| **Temperature** | Randomness | Deterministic, precise | Creative, unpredictable |
| **Top-P** | Token diversity (probability) | Conservative | Diverse |
| **Top-K** | Token diversity (count) | Focused | Varied |
| **Max Output Tokens** | Response length | Short/truncated | Long/detailed |

---

## 3. Retrieval-Augmented Generation (RAG)

### What Is RAG?
RAG is an architecture that **enhances an LLM's responses by retrieving relevant external information** at query time before generating an answer. Instead of relying solely on the model's trained knowledge, RAG connects the model to a **real-time knowledge source**.

### How RAG Works (Step by Step)

```
User Query
    │
    ▼
[1] Convert query to embedding (vector)
    │
    ▼
[2] Search vector database for similar document chunks
    │
    ▼
[3] Retrieve top-K relevant chunks
    │
    ▼
[4] Inject retrieved chunks into the prompt as context
    │
    ▼
[5] LLM generates a response grounded in the retrieved context
    │
    ▼
Answer (grounded in your data)
```

### Why Use RAG?
- Provides LLMs with **up-to-date or proprietary information** not in training data.
- **Reduces hallucinations** by grounding responses in factual retrieved content.
- **No model retraining** required — just update the knowledge base.
- More **cost-effective** than fine-tuning for knowledge updates.

### Business Applications of RAG

| Application | Description |
|---|---|
| **Enterprise search** | Search internal documents, wikis, and policies using natural language |
| **Customer support** | Answer questions grounded in up-to-date product documentation |
| **Legal/compliance Q&A** | Retrieve relevant regulations or contracts to answer specific questions |
| **Healthcare** | Answer clinical questions from medical literature |
| **Financial analysis** | Query earnings reports, filings, or market data |
| **HR assistants** | Answer employee questions from HR policies and handbooks |

### Amazon Bedrock Knowledge Bases
- AWS's **fully managed RAG solution** within Amazon Bedrock.
- Automates the full RAG pipeline: document ingestion, chunking, embedding, vector storage, and retrieval.
- Connects to data sources (S3, Confluence, SharePoint, etc.).
- Uses **Amazon Titan Embeddings** or other models to convert documents into vectors.
- Integrates with vector stores (OpenSearch Serverless, Aurora, etc.).
- Used with **Amazon Bedrock Agents** for more complex workflows.

> 💡 **Exam Tip**: RAG is the go-to answer when a question involves giving an LLM access to **private/proprietary/up-to-date data** without retraining. Amazon Bedrock Knowledge Bases is the AWS-managed way to implement RAG.

---

## 4. Vector Databases on AWS

Embeddings generated during RAG indexing must be stored in a **vector database** that supports **similarity search** (finding the most semantically similar chunks to a query).

### AWS Services for Storing Embeddings / Vector Search

| AWS Service | Type | Notes |
|---|---|---|
| **Amazon OpenSearch Service** | Search & analytics engine | Supports k-NN (k-nearest neighbor) vector search; most common choice for RAG on AWS |
| **Amazon Aurora** (PostgreSQL-compatible) | Relational database | Supports `pgvector` extension for vector similarity search |
| **Amazon RDS for PostgreSQL** | Relational database | Also supports `pgvector` extension; good if already using RDS |
| **Amazon Neptune** | Graph database | Supports vector search alongside graph queries; good for knowledge graphs + RAG |
| **Amazon MemoryDB** | In-memory database | Fast vector search for low-latency use cases |

### Key Concept: k-NN Search
- **k-Nearest Neighbor (k-NN)** search finds the K most similar vectors to a query vector.
- This is how RAG retrieves the most relevant document chunks given a user's query.

> 💡 **Exam Tip**: **OpenSearch Service** is the most commonly tested vector database for RAG on AWS. Know that **Aurora and RDS for PostgreSQL** use the **pgvector** extension. Neptune is used when graph relationships are also needed.

---

## 5. FM Customization Approaches and Cost Tradeoffs

There are several ways to adapt an FM to your specific needs. They vary significantly in **cost, complexity, data requirements, and flexibility**.

### In-Context Learning (Prompting)
- **What it is**: Provide examples or instructions directly in the prompt at inference time — no model changes.
- **Techniques**: Zero-shot, few-shot, chain-of-thought prompting.
- **Cost**: Lowest — only pay for inference tokens.
- **Data needed**: None to a few examples.
- **Complexity**: Low.
- **Limitations**: Limited by context window size; doesn't persist learning.
- **Best for**: Quick tasks, low-volume use cases, prototyping.

### Retrieval-Augmented Generation (RAG)
- **What it is**: Dynamically retrieve relevant external knowledge at inference time.
- **Cost**: Low-to-medium — indexing cost (one-time or periodic) + inference.
- **Data needed**: Knowledge base documents (no labels needed).
- **Complexity**: Medium (requires vector DB, embedding pipeline).
- **Limitations**: Only as good as retrieved content; adds latency.
- **Best for**: Keeping model updated with proprietary/dynamic knowledge.

### Fine-Tuning
- **What it is**: Further train a pre-trained FM on a **custom labeled dataset** to specialize its behavior or knowledge.
- **Cost**: Medium-to-high — requires labeled data + training compute.
- **Data needed**: Hundreds to thousands of labeled examples.
- **Complexity**: High (data prep, training jobs, evaluation).
- **Limitations**: Expensive to update; risk of catastrophic forgetting.
- **Best for**: Adapting model tone/style, domain-specific tasks, improving accuracy on a narrow task.
- **AWS Service**: Amazon Bedrock fine-tuning, SageMaker.

### Pre-Training (from scratch)
- **What it is**: Train an entirely new model on massive datasets from the ground up.
- **Cost**: Extremely high — millions of dollars in compute, massive datasets.
- **Data needed**: Billions of tokens of training data.
- **Complexity**: Very high — requires deep ML expertise and infrastructure.
- **Limitations**: Only feasible for large organizations.
- **Best for**: Building a proprietary FM with unique capabilities.

### Cost & Complexity Comparison

| Approach | Cost | Data Needed | Complexity | Persistence |
|---|---|---|---|---|
| **In-Context Learning** | 💲 Lowest | None / few examples | Low | No |
| **RAG** | 💲💲 Low-Medium | Unlabeled documents | Medium | Knowledge base |
| **Fine-Tuning** | 💲💲💲 Medium-High | Labeled dataset | High | Model weights |
| **Pre-Training** | 💲💲💲💲 Highest | Billions of tokens | Very High | New model |

> 💡 **Exam Tip**: This is a heavily tested comparison. Remember the progression: **In-context → RAG → Fine-tuning → Pre-training** = increasing cost, complexity, and data requirements. Use the **cheapest option that solves the problem**.

---

## 6. The Role of Agents in Multi-Step Tasks

### What Is an AI Agent?
An AI agent is an LLM-powered system that can **plan, reason, and take actions** to complete multi-step tasks autonomously. Unlike a basic chatbot that only responds, an agent can:
- Break a complex task into sub-steps.
- Decide which **tools or APIs** to call.
- Execute actions (query databases, call APIs, run code).
- Observe results and adjust its plan.
- Loop until the task is complete.

### Agentic AI
- Refers to AI systems that exhibit **autonomous, goal-directed behavior**.
- The agent operates in a **reasoning loop**: *Think → Act → Observe → Repeat*.
- Key characteristics:
  - **Goal-driven**: Works toward a defined objective.
  - **Tool use**: Calls external APIs, databases, services.
  - **Memory**: Maintains context across steps.
  - **Planning**: Decomposes complex goals into steps.

### Amazon Bedrock Agents
- AWS's **fully managed agent service** within Amazon Bedrock.
- Allows you to build agents that can orchestrate multi-step tasks using FMs.
- **Key capabilities**:
  - **Action groups**: Define APIs/Lambda functions the agent can call.
  - **Knowledge Bases integration**: Agent can retrieve information from RAG pipelines.
  - **Orchestration**: Automatically plans and sequences steps.
  - **Session management**: Maintains conversation context across turns.
  - **Guardrails**: Apply safety filters to agent actions and outputs.
- **How it works**:
  1. User submits a goal/request.
  2. Agent uses an FM to reason and plan.
  3. Agent calls defined actions (APIs, Lambda, Knowledge Bases).
  4. Agent observes results and continues reasoning.
  5. Agent returns final response to user.

**Example**: A travel booking agent that:
1. Checks flight availability (API call)
2. Retrieves hotel recommendations (Knowledge Base)
3. Calculates total cost (Lambda function)
4. Confirms booking (API call)
5. Returns itinerary to user

### Model Context Protocol (MCP)
- An **open standard protocol** (introduced by Anthropic) that defines how AI models can **connect to external tools, data sources, and APIs** in a standardized way.
- Think of it as a **universal plug** for connecting AI agents to the outside world.
- Enables agents to discover and use tools without custom integration for each one.
- Promotes **interoperability** between different AI systems and tool providers.
- AWS and many third-party services are adopting MCP for agent tool integrations.

> 💡 **Exam Tip**: Agents are the answer when a scenario involves **multi-step tasks**, **calling external APIs**, **autonomous decision-making**, or **combining RAG with actions**. Amazon Bedrock Agents is the AWS-managed service. MCP is the open standard for connecting agents to tools.

---

## 7. Summary: Choosing the Right Architecture

| Scenario | Recommended Approach |
|---|---|
| Simple Q&A with a few examples in the prompt | In-context learning (few-shot prompting) |
| Q&A over company's internal documents | RAG (Amazon Bedrock Knowledge Bases) |
| Improve model tone/style for a brand voice | Fine-tuning |
| Model needs deep expertise in a niche domain | Fine-tuning |
| Automate a multi-step business workflow | Amazon Bedrock Agents |
| Search internal knowledge base with natural language | RAG + Vector DB (OpenSearch) |
| Build a completely proprietary LLM | Pre-training |
| Add vector search to existing PostgreSQL DB | RDS for PostgreSQL + pgvector |

---

## 8. Exam Tips Recap

- ✅ **Temperature**: Low = deterministic/factual. High = creative/varied.
- ✅ **RAG** = connect LLM to external knowledge without retraining. Best for proprietary/dynamic data.
- ✅ **Amazon Bedrock Knowledge Bases** = AWS managed RAG service.
- ✅ **OpenSearch** is the primary AWS vector database; Aurora/RDS use **pgvector**.
- ✅ Cost order (low → high): **In-context < RAG < Fine-tuning < Pre-training**.
- ✅ **Fine-tuning** needs labeled data; **RAG** needs unlabeled documents.
- ✅ **Amazon Bedrock Agents** orchestrate multi-step tasks using tools + knowledge bases.
- ✅ **MCP (Model Context Protocol)** is the open standard for connecting agents to external tools.
- ✅ Context window size matters for **long document processing** — key model selection criterion.
- ✅ **Prompt caching** reduces cost and latency when the same prompt prefix is reused frequently.