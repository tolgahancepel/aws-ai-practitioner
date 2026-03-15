# AWS AI Practitioner Exam – Machine Learning Services Study Notes

> **Exam Tip:** Focus on *what each service does*, *when to use it*, *key features*, and *how it integrates* with other AWS services. Understand the difference between managed AI services (pre-built) vs. custom ML platforms (SageMaker).

---

## Table of Contents

1. [Amazon Augmented AI (A2I)](#1-amazon-augmented-ai-amazon-a2i)
2. [Amazon Bedrock](#2-amazon-bedrock)
3. [Amazon Comprehend](#3-amazon-comprehend)
4. [Amazon Fraud Detector](#4-amazon-fraud-detector)
5. [Amazon Kendra](#5-amazon-kendra)
6. [Amazon Lex](#6-amazon-lex)
7. [Amazon Nova](#7-amazon-nova)
8. [Amazon Personalize](#8-amazon-personalize)
9. [Amazon Polly](#9-amazon-polly)
10. [Amazon Q Developer](#10-amazon-q-developer)
11. [Amazon Q Business](#11-amazon-q-business)
12. [Amazon Rekognition](#12-amazon-rekognition)
13. [Amazon SageMaker AI](#13-amazon-sagemaker-ai)
14. [Amazon Textract](#14-amazon-textract)
15. [Amazon Transcribe](#15-amazon-transcribe)
16. [Amazon Translate](#16-amazon-translate)

---

## 1. Amazon Augmented AI (Amazon A2I)

### What It Is
A fully managed service that makes it easy to build the workflows required for **human review of ML predictions**. It integrates a human-in-the-loop step into ML pipelines when confidence scores are low or when compliance demands human oversight.

### Key Concepts
- **Human review workflow:** Routes low-confidence predictions to human reviewers.
- **Worker task templates:** Define the UI displayed to human reviewers.
- **Private, Amazon Mechanical Turk, or vendor workforce:** Three options for who performs the review.
- **Built-in integrations:** Works natively with Amazon Rekognition (content moderation) and Amazon Textract (document analysis).
- **Custom workflows:** Can be configured for any ML model, not just AWS-native ones.

### When to Use
- When regulatory or compliance requirements mandate human oversight of AI decisions.
- When model confidence is below a defined threshold.
- For tasks such as medical image review, content moderation, data labeling, and document processing.

### Key Facts for the Exam
- A2I does **not** train models – it reviews predictions made by other models.
- The three workforce types: **Amazon Mechanical Turk** (crowd), **private** (internal employees), **vendor** (third-party specialists).
- Works with **any ML model**, not just AWS services.
- Integrated with SageMaker for custom ML workflows.

---

## 2. Amazon Bedrock

### What It Is
A **fully managed service** that provides access to **Foundation Models (FMs)** from Amazon and leading AI companies via a single API, without the need to manage infrastructure. It is the central hub for **Generative AI** on AWS.

### Key Concepts
- **Foundation Models (FMs):** Large pre-trained models (text, image, embeddings) available on-demand.
- **Model providers available:** Amazon (Nova, Titan), Anthropic (Claude), Meta (Llama), Mistral, Cohere, Stability AI, and others.
- **Fine-tuning:** Customize a base FM with your own labeled data (without managing compute).
- **Continued Pre-training:** Further pre-train a base model with unlabeled domain-specific data.
- **Retrieval-Augmented Generation (RAG):** Augment model responses with data from your own knowledge bases using **Amazon Bedrock Knowledge Bases**.
- **Agents:** Bedrock Agents can orchestrate multi-step tasks by calling APIs and data sources autonomously.
- **Guardrails:** Apply content filters, topic restrictions, PII redaction, and hallucination detection to model responses.
- **Model Evaluation:** Compare and evaluate FM responses using built-in or custom metrics.
- **Serverless:** No infrastructure to manage; pay per token (API call).

### When to Use
- Building generative AI applications (chatbots, summarization, code generation, content creation).
- When you need to compare multiple FMs side-by-side.
- When you need RAG to ground responses in proprietary data.
- When compliance requires content filtering (Guardrails).

### Key Facts for the Exam
- Bedrock is **not** for training models from scratch – that is SageMaker.
- **Knowledge Bases** store vector embeddings and enable RAG without custom infrastructure.
- **Agents** can invoke Lambda functions and APIs to take actions based on user requests.
- **Guardrails** help enforce responsible AI policies (content safety, PII protection).
- Data sent to Bedrock is **not used** to train the underlying foundation models.
- Supports both **on-demand** and **provisioned throughput** pricing modes.

---

## 3. Amazon Comprehend

### What It Is
A **Natural Language Processing (NLP)** service that uses ML to find insights and relationships in unstructured text. It requires **no ML expertise** to use.

### Key Concepts
- **Entity recognition:** Identifies people, places, organizations, dates, quantities, etc.
- **Sentiment analysis:** Determines if text is positive, negative, neutral, or mixed.
- **Key phrase extraction:** Identifies the most important phrases in text.
- **Language detection:** Identifies the dominant language of a document.
- **Syntax analysis:** Tokenizes text and identifies parts of speech.
- **Topic modeling:** Groups documents into topics using Latent Dirichlet Allocation (LDA).
- **Custom classification:** Train a custom text classifier with your own labels.
- **Custom entity recognition:** Train the model to identify domain-specific entities.
- **Amazon Comprehend Medical:** A specialized version for extracting medical information (diagnoses, medications, dosages) from clinical notes.
- **PII detection and redaction:** Identifies and optionally redacts Personally Identifiable Information.

### When to Use
- Analyzing customer feedback, reviews, or social media at scale.
- Classifying support tickets automatically.
- Extracting medical entities from clinical documents (Comprehend Medical).
- Detecting and redacting PII from documents.

### Key Facts for the Exam
- Comprehend is **pre-trained** but also supports **custom models** (custom classification and entity recognition).
- **Comprehend Medical** is a separate, specialized service for healthcare NLP.
- Works with **real-time** (synchronous) and **batch** (asynchronous) modes.
- Integrates with S3, Lambda, and Kinesis for pipeline automation.

---

## 4. Amazon Fraud Detector

### What It Is
A **fully managed service** that uses ML to identify potentially fraudulent activity and catch more online fraud faster. It is purpose-built for fraud detection use cases.

### Key Concepts
- **Event types:** Define the type of event you are evaluating (e.g., online payment, account registration).
- **Variables:** Data inputs used to make predictions (IP address, email, device ID, transaction amount).
- **Models:** Fraud Detector trains models using your historical data (labeled fraud/legitimate) and Amazon's fraud detection expertise.
- **Detectors:** Logic engines that combine model scores with rules to produce fraud outcomes.
- **Rules:** Business logic (written in a rule engine) that supplements ML predictions.
- **Outcomes:** The result of a detector evaluation (e.g., approve, review, reject).
- **Model types:**
  - **Online Fraud Insights (OFI):** Best for transaction fraud.
  - **Transaction Fraud Insights (TFI):** Uses time-ordered transaction data.
  - **Account Takeover Insights (ATI):** Detects compromised account logins.

### When to Use
- Detecting fraudulent online payments, registrations, or account logins.
- When you want a managed solution without building fraud ML from scratch.
- When you need to combine ML scores with business rules in real-time.

### Key Facts for the Exam
- Amazon Fraud Detector **requires your own labeled historical data** to train models.
- It combines ML + **business rules** – not purely an ML service.
- Designed for **real-time** fraud scoring at low latency.
- Three model types: **OFI**, **TFI**, and **ATI** – each suited to different fraud scenarios.
- Integrates with AWS Lambda and Amazon EventBridge for automated responses.

---

## 5. Amazon Kendra

### What It Is
An **intelligent enterprise search** service powered by ML. It enables users to search across multiple data repositories using **natural language queries** and returns precise, relevant answers rather than just a list of links.

### Key Concepts
- **Index:** A central store of searchable content, ingested from data sources.
- **Data sources (connectors):** Pre-built connectors to S3, SharePoint, Confluence, Salesforce, ServiceNow, RDS, OneDrive, Google Workspace, and more.
- **Natural language understanding:** Understands the intent behind queries (e.g., "How many days of PTO do I have?" returns a direct answer, not a document list).
- **Incremental crawling:** Automatically keeps the index updated when source data changes.
- **FAQs:** Ingest structured Q&A pairs to return direct answers.
- **Relevance tuning:** Adjust ranking based on freshness, document type, or custom attributes.
- **Access control:** Respects document-level permissions from source systems.
- **Kendra GenAI Index:** Enhanced version with generative AI capabilities for conversational search.

### When to Use
- Internal enterprise search across HR documents, wikis, ticketing systems, etc.
- Customer-facing search portals for knowledge bases.
- When users need precise answers, not just document retrieval.

### Key Facts for the Exam
- Kendra is a **search service**, not a general-purpose NLP service.
- It understands **natural language** – not just keyword matching.
- Supports **structured and unstructured** data sources.
- Access control is enforced so users only see documents they have permission to view.
- Kendra can be used as a **knowledge base** data source for Amazon Bedrock RAG applications.
- Differs from OpenSearch: Kendra is purpose-built for natural language enterprise search; OpenSearch is a general-purpose search/analytics engine.

---

## 6. Amazon Lex

### What It Is
A **fully managed service** for building **conversational interfaces** (chatbots and voice bots) using the same deep learning technologies that power Amazon Alexa.

### Key Concepts
- **Bot:** The conversational application you build.
- **Intents:** The action a user wants to perform (e.g., "BookFlight", "CheckOrderStatus").
- **Utterances:** Sample phrases that trigger an intent (e.g., "I want to book a flight", "Reserve a ticket").
- **Slots:** Variables that capture specific information within an intent (e.g., departure city, date). Each slot has a **slot type** (built-in or custom).
- **Fulfillment:** The logic that executes once all slots are filled – typically an AWS Lambda function.
- **Elicitation:** The process of prompting the user to fill missing slots.
- **Session management:** Maintains context across turns of a conversation.
- **Multi-turn dialogue:** Supports back-and-forth conversations to gather all required information.
- **Channels:** Deploy bots to web, mobile, Slack, Twilio, Facebook Messenger, and more.
- **Integration with Amazon Connect:** Build call center bots for voice interactions.

### When to Use
- Building customer service chatbots.
- Automating FAQ answering in call centers (with Amazon Connect).
- Creating voice-enabled applications.
- Automating order placement, appointment scheduling, etc.

### Key Facts for the Exam
- Lex handles **Automatic Speech Recognition (ASR)** for voice and **Natural Language Understanding (NLU)** for text.
- Lex does **not** generate open-ended responses – responses are scripted or fetched via Lambda.
- For **generative conversational AI**, use Amazon Bedrock + Agents.
- Lex V2 supports **streaming** conversations for real-time voice.
- HIPAA eligible and supports PCI DSS compliance.

---

## 7. Amazon Nova

### What It Is
Amazon Nova is a family of **state-of-the-art foundation models** developed by Amazon and available through **Amazon Bedrock**. Nova models are designed to deliver a strong balance of intelligence, speed, and cost-effectiveness across a range of tasks.

### Nova Model Tiers
| Model | Type | Best For |
|---|---|---|
| **Nova Micro** | Text only | Lowest latency, lowest cost; simple text tasks |
| **Nova Lite** | Multimodal | Fast, low-cost; processes text, image, and video |
| **Nova Pro** | Multimodal | Highest accuracy; complex reasoning, agentic tasks |
| **Nova Canvas** | Image generation | High-quality image generation and editing |
| **Nova Reel** | Video generation | Short video generation from text or images |
| **Nova Sonic** | Speech-to-speech | Real-time voice conversations (speech in, speech out) |

### Key Concepts
- **Multimodal:** Nova Lite and Pro accept text, images, and video as input.
- **Agentic capabilities:** Nova Pro supports complex multi-step reasoning and tool use.
- **Fine-tuning:** Nova models support fine-tuning through Bedrock for domain customization.
- **Context window:** Nova models support large context windows for processing long documents.
- **Responsible AI:** Built with Amazon's responsible AI principles and integrates with Bedrock Guardrails.

### When to Use
- When you need Amazon's own FMs for cost-effective text, image, or video AI tasks.
- Nova Micro/Lite for high-volume, latency-sensitive applications.
- Nova Pro for complex reasoning, agentic workflows, and multi-step tasks.
- Nova Canvas/Reel for content generation pipelines.
- Nova Sonic for real-time conversational voice AI.

### Key Facts for the Exam
- Nova models are accessed exclusively through **Amazon Bedrock**.
- Nova is Amazon's **answer to third-party FMs** (e.g., Claude, GPT) – optimized for AWS workloads.
- **Nova Pro** is the most capable for reasoning and agentic use cases.
- **Nova Sonic** enables **real-time bidirectional voice** interaction (unlike Polly/Transcribe which are one-way).

---

## 8. Amazon Personalize

### What It Is
A **fully managed ML service** that enables developers to build real-time **personalized recommendation** systems without requiring ML expertise. It uses the same technology as Amazon.com's product recommendations.

### Key Concepts
- **Dataset groups:** A container for your data (interactions, users, items).
- **Interaction data:** The core dataset – logs of user-item events (purchases, clicks, views, ratings). This is **required**.
- **User data:** Optional metadata about users (age, membership level, etc.).
- **Item data:** Optional metadata about items (category, genre, price, etc.).
- **Recipes (algorithms):** Pre-configured algorithms for specific use cases:
  - **User Personalization:** Recommend items to users based on history.
  - **Similar Items:** Find items similar to a given item.
  - **Personalized Ranking:** Re-rank a given list of items for a user.
  - **Trending Now:** Recommend currently popular items.
  - **Next Best Action:** Predict the next best action for a user.
- **Solutions and solution versions:** A trained model using a recipe and your data.
- **Campaigns:** A deployed solution version that serves real-time recommendations via API.
- **Batch inference jobs:** Generate recommendations for all users/items at once (offline).
- **Filters:** Rules to exclude certain items (e.g., items already purchased) from recommendations.
- **Context:** Pass real-time contextual data (device type, time of day) to improve recommendations.

### When to Use
- E-commerce product recommendations.
- Media content recommendations (movies, articles, music).
- Personalized marketing campaigns.
- Re-ranking search results for individual users.

### Key Facts for the Exam
- Personalize requires **historical interaction data** to train – minimum 1,000 interactions from at least 25 users.
- It is **not** a general recommendation engine – it is specifically for **item-user interaction recommendations**.
- Real-time recommendations use **campaigns**; offline bulk recommendations use **batch inference jobs**.
- **Filters** prevent recommending already-purchased or ineligible items.
- Supports **cold-start** (new users/items with no history) through item/user metadata.

---

## 9. Amazon Polly

### What It Is
A **Text-to-Speech (TTS)** service that converts text into lifelike speech. It uses deep learning to synthesize natural-sounding human voices in multiple languages.

### Key Concepts
- **Standard voices:** Concatenative synthesis; natural but less expressive.
- **Neural TTS (NTTS):** Uses a neural network for more natural, human-like speech quality.
- **Generative voices (long-form):** Most natural-sounding option for longer content.
- **Speech Synthesis Markup Language (SSML):** XML-based language to control pronunciation, speed, pitch, volume, pauses, and emphasis.
- **Lexicons:** Custom pronunciation dictionaries for domain-specific terms (e.g., brand names, abbreviations).
- **Speech marks:** Metadata about synthesized speech (word timing, phoneme markers) for synchronizing animations.
- **Output formats:** MP3, OGG, PCM (raw audio), and speech marks (JSON).
- **Languages supported:** 30+ languages with 60+ voices.
- **Asynchronous synthesis:** For long text, store output to S3 via asynchronous job.

### When to Use
- Adding voice narration to applications or games.
- Generating audio content for accessibility (screen readers, audio books).
- Creating voice responses in IVR systems.
- Automating podcast or notification generation.

### Key Facts for the Exam
- Polly is **one-way**: text → speech only. For speech → text, use **Amazon Transcribe**.
- **Neural TTS** produces better quality than standard but costs more.
- **SSML** gives fine-grained control over how text is spoken.
- **Lexicons** are custom pronunciation guides; **SSML** controls speech style.
- Polly does **not** understand content – it only synthesizes audio from text.

---

## 10. Amazon Q Developer

### What It Is
An AI-powered **coding assistant and developer tool** that helps software developers write, understand, debug, refactor, and improve code. It is integrated into popular IDEs (VS Code, JetBrains) and the AWS console.

### Key Concepts
- **Code generation:** Generate code from natural language descriptions.
- **Code completion:** Real-time inline code suggestions as you type.
- **Code explanation:** Understand what existing code does using natural language explanations.
- **Code transformation:** Automatically upgrade code (e.g., Java 8 → Java 17) or migrate frameworks.
- **Bug detection and security scanning:** Identifies vulnerabilities (OWASP Top 10, CWEs) in code.
- **Unit test generation:** Auto-generate unit tests for existing functions.
- **AWS resource integration:** Provides AWS-aware suggestions (e.g., correct SDK usage, IAM policy patterns).
- **Agent for software development:** Can implement features end-to-end by planning, writing, and reviewing code.
- **Amazon Q Developer in the console:** Answers AWS questions, generates CLI commands, explains CloudWatch logs, helps with IAM policies.

### When to Use
- Accelerating software development with AI code suggestions.
- Performing security audits on codebases.
- Automatically upgrading legacy code to newer language versions.
- Onboarding new developers to a codebase.
- Generating unit tests to improve test coverage.

### Key Facts for the Exam
- Q Developer is a **developer-focused** tool; Q Business is for **business users**.
- Q Developer replaces and extends what was previously called **Amazon CodeWhisperer**.
- It supports **30+ programming languages** including Python, Java, TypeScript, C#, Go, Rust, and more.
- The security scanning feature checks for **vulnerabilities and exposed credentials**.
- The **transformation agent** can upgrade an entire Java application automatically.
- Available in **free tier** (basic) and **Pro tier** (advanced features, org-level controls).

---

## 11. Amazon Q Business

### What It Is
A **fully managed generative AI assistant** for the enterprise. It allows employees to ask questions in natural language and get answers sourced from the company's own data and documents, without accessing the internet.

### Key Concepts
- **Connectors (data sources):** Ingest content from 40+ sources including S3, SharePoint, Confluence, Salesforce, ServiceNow, Google Drive, Jira, Zendesk, and more.
- **Index:** Stores processed and vectorized content from all connected sources.
- **Retrieval-Augmented Generation (RAG):** Answers are generated by combining the FM with retrieved chunks from the index.
- **Access control:** Respects the source system's permission model – users only see data they are authorized to access.
- **Admin controls:** Admins can block certain topics, set guardrails, and control which plugins are enabled.
- **Plugins:** Extend Q Business with actions (e.g., create Jira ticket, send email, submit ServiceNow request) via pre-built or custom plugins.
- **Amazon Q Apps:** Business users can create simple, no-code applications from Q Business conversations.
- **Identity integration:** Works with IAM Identity Center, Okta, Azure AD, and other IdPs for user authentication.

### When to Use
- Employee-facing knowledge assistant ("company chatbot") for HR, IT, legal, etc.
- Enabling non-technical employees to get answers from internal documents.
- Replacing traditional intranet search with conversational AI.
- Automating workflows by combining retrieval with action plugins.

### Key Facts for the Exam
- Q Business is for **enterprise/business users**; Q Developer is for **developers/engineers**.
- It does **not** rely on public internet – answers come from **your company's own data**.
- Access control is **enforced at query time** based on user identity.
- Responses include **citations** linking back to the source documents.
- Built on **Amazon Bedrock** under the hood.
- Supports **web experience** (browser-based chat UI) out of the box, or embed via API.

---

## 12. Amazon Rekognition

### What It Is
A **fully managed computer vision** service that makes it easy to add image and video analysis capabilities to applications. It uses deep learning models that do not require ML expertise.

### Key Concepts

**Image Analysis:**
- **Object and scene detection:** Identifies thousands of objects, scenes, and concepts (e.g., "beach", "car", "sunset").
- **Facial analysis:** Detects faces and analyzes attributes (emotions, age range, gender, wearing glasses, etc.). Does **not** identify who a person is by default.
- **Facial recognition (comparison and search):** Compares a face against another, or searches a face collection to identify known individuals.
- **Face collections:** Store face vectors for recognition (e.g., employee database, known bad actors).
- **Celebrity recognition:** Identifies well-known public figures.
- **Text in image (OCR):** Detects and extracts text visible in images.
- **Content moderation:** Detects explicit, suggestive, or violent content.
- **Custom labels:** Train a custom object/scene detection model with your own images and labels.
- **PPE detection:** Detects personal protective equipment (hard hats, masks, gloves) for workplace safety.

**Video Analysis:**
- All image features available on stored video (S3) and streaming video (Kinesis Video Streams).
- **Person tracking:** Track individuals across frames in a video.
- **Segment detection:** Detect scenes, credits, shot changes in video content.
- **Unsafe content in video:** Moderate video content at scale.

### When to Use
- Content moderation for user-generated content platforms.
- Verifying identities in banking/insurance applications.
- Workplace safety compliance (PPE detection).
- Media analysis and metadata tagging.
- Detecting custom defects on a production line (Custom Labels).

### Key Facts for the Exam
- Rekognition **does not require ML expertise** – it is a pre-trained API service.
- **Custom Labels** allows training on domain-specific images (e.g., industrial parts, medical images).
- Facial **analysis** (emotions, attributes) ≠ facial **recognition** (identifying who a person is). Recognition requires a **face collection**.
- Works on **images** (JPEG, PNG via S3 or bytes) and **videos** (S3 or Kinesis Video Streams).
- **Content moderation** returns a confidence score and category hierarchy.
- HIPAA eligible; supports compliance use cases.

---

## 13. Amazon SageMaker AI

### What It Is
A **fully managed end-to-end ML platform** for data scientists and ML engineers to **build, train, tune, and deploy** custom ML models at scale. SageMaker covers the entire ML lifecycle.

### Key Concepts & Components

**Data Preparation:**
- **SageMaker Data Wrangler:** Visual tool for data preparation, feature engineering, and transformation without coding.
- **SageMaker Feature Store:** Centralized repository to store, retrieve, and share ML features across teams and models.
- **SageMaker Ground Truth:** Managed data labeling service using human annotators (private, Mechanical Turk, or vendor workforce) with active learning to reduce labeling costs.

**Model Development:**
- **SageMaker Studio:** Web-based integrated development environment (IDE) for all ML tasks.
- **SageMaker Notebooks:** Fully managed Jupyter notebooks with pre-installed ML frameworks.
- **SageMaker Experiments:** Track, compare, and manage ML training runs and experiments.
- **SageMaker Autopilot:** AutoML tool that automatically explores algorithms and hyperparameters to build the best model. Provides full visibility into the generated code.
- **SageMaker JumpStart:** Model hub with pre-trained models, solution templates, and algorithms for quick start.

**Training:**
- **Managed training jobs:** Spin up compute, run training, and automatically terminate instances.
- **Distributed training:** Train large models across multiple instances (model parallelism, data parallelism).
- **Spot training:** Use EC2 Spot Instances to reduce training costs by up to 90%.
- **Hyperparameter Tuning (HPO):** Automatically find the best hyperparameters using Bayesian optimization.
- **SageMaker Debugger:** Monitor and debug training in real-time to detect issues (vanishing gradients, overfitting).

**Deployment & Inference:**
- **Real-time endpoints:** Low-latency, always-on endpoints for synchronous predictions.
- **Serverless inference:** Auto-scales to zero when not in use; ideal for intermittent traffic.
- **Asynchronous inference:** For large payloads or long processing times; queues requests and stores results in S3.
- **Batch transform:** Run bulk predictions on large datasets stored in S3.
- **Multi-model endpoints:** Host multiple models on a single endpoint to save costs.
- **SageMaker Pipelines:** CI/CD pipeline for automating the ML workflow (data prep → train → evaluate → deploy).

**Monitoring & Governance:**
- **SageMaker Model Monitor:** Detects data drift and model quality degradation in production.
- **SageMaker Clarify:** Detects bias in data and models; explains model predictions (explainability/SHAP values).
- **SageMaker Model Registry:** Version, catalog, and manage model approvals for production deployment.
- **SageMaker Role Manager:** Simplifies IAM permission management for ML teams.

### When to Use
- When you need to **train a custom model** on your own data.
- When pre-built AI services (Rekognition, Comprehend, etc.) don't meet your specific requirements.
- When you need full control over model architecture, training, and serving.
- For large-scale ML operations (MLOps) with pipelines, monitoring, and governance.

### Key Facts for the Exam
- SageMaker is for **custom ML** – use managed AI services (Rekognition, Comprehend, etc.) when possible for simpler use cases.
- **Autopilot** = AutoML within SageMaker (no code required, but fully visible).
- **JumpStart** provides pre-trained FMs and solution templates for fast prototyping.
- **Ground Truth** is for **data labeling**; **A2I** is for **human review of predictions**.
- **Model Monitor** detects **data drift**; **Clarify** detects **bias** and explains predictions.
- **Pipelines** = MLOps automation (similar concept to CI/CD but for ML).
- SageMaker supports frameworks: TensorFlow, PyTorch, scikit-learn, XGBoost, MXNet, Hugging Face, and custom containers.

---

## 14. Amazon Textract

### What It Is
A **fully managed ML service** that automatically extracts text and structured data (forms, tables, signatures) from scanned documents and images. It goes beyond simple OCR by understanding document structure.

### Key Concepts
- **DetectDocumentText:** Basic OCR – extracts raw text (lines and words) from a document.
- **AnalyzeDocument:** Extracts structured data:
  - **Forms (key-value pairs):** Extracts labeled fields (e.g., "Name: John Doe", "Date: 01/01/2024").
  - **Tables:** Extracts table structure with rows and columns.
  - **Signatures:** Detects the presence of signatures on documents.
  - **Queries:** Ask specific questions about the document (e.g., "What is the patient's date of birth?").
- **AnalyzeExpense:** Specialized for **invoices and receipts** – extracts vendor name, total, line items, taxes.
- **AnalyzeID:** Specialized for **identity documents** (passports, driver's licenses) – extracts standardized fields.
- **Lending document analysis:** Extracts data from mortgage documents (W-2s, 1040s, paystubs).
- **Asynchronous API:** For multi-page PDFs and large documents, use StartDocument* and GetDocument* APIs.
- **Confidence scores:** Each extracted item includes a confidence score.

### When to Use
- Automating data entry from scanned forms, contracts, or invoices.
- Processing insurance claims, loan applications, or medical records.
- Extracting tables from financial reports.
- Digitizing and indexing archived paper documents.
- Verifying identity documents (with AnalyzeID).

### Key Facts for the Exam
- Textract is **not** just OCR – it understands document **structure** (forms, tables).
- Use **AnalyzeExpense** for invoices/receipts and **AnalyzeID** for identity documents.
- For **simple text extraction**, use DetectDocumentText; for **structured data**, use AnalyzeDocument.
- Supports **JPEG, PNG, PDF, TIFF** formats.
- Integrates with A2I for human review of low-confidence extractions.
- Pairs with **Comprehend** for NLP analysis after extraction.
- Asynchronous APIs are required for **multi-page PDFs**.

---

## 15. Amazon Transcribe

### What It Is
A **fully managed automatic speech recognition (ASR)** service that converts audio and video speech into accurate text. It supports batch and real-time (streaming) transcription.

### Key Concepts
- **Batch transcription:** Submit audio files stored in S3; receive transcript as output.
- **Streaming transcription:** Real-time transcription via WebSocket or HTTP/2 streaming (for live audio).
- **Language support:** 100+ languages and dialects.
- **Speaker diarization (identification):** Differentiates between multiple speakers in an audio file (e.g., "Speaker 1:", "Speaker 2:").
- **Custom vocabulary:** Improve accuracy for domain-specific terms (product names, medical terms, jargon) by providing a list of words.
- **Custom language models:** Fine-tune the ASR model with domain-specific text data for higher accuracy.
- **Vocabulary filters:** Mask, remove, or tag profanity or unwanted words.
- **Automatic content redaction:** Automatically identifies and redacts PII from transcripts.
- **Channel identification:** Separate transcription for each audio channel (e.g., agent and customer in a call).
- **Amazon Transcribe Medical:** HIPAA-eligible ASR for clinical speech, trained on medical terminology.
- **Amazon Transcribe Call Analytics:** Specialized for contact center calls – includes sentiment analysis, call categorization, and agent/customer talk time metrics.
- **Subtitles:** Generate WebVTT or SRT subtitle files from transcription.

### When to Use
- Transcribing call center recordings for analysis.
- Generating subtitles and closed captions for videos.
- Enabling voice search in applications.
- Transcribing doctor-patient conversations (Transcribe Medical).
- Indexing meeting recordings or interviews.

### Key Facts for the Exam
- Transcribe is **speech → text**; Polly is **text → speech**. They are complementary.
- **Speaker diarization** identifies *who* spoke, not *what* they said (that's NLU, handled by Comprehend or Lex).
- **Custom vocabulary** = word list for better recognition accuracy; **Custom language model** = trained on domain text.
- **Call Analytics** is a specialized, higher-level product for contact center insights on top of Transcribe.
- **Transcribe Medical** is HIPAA eligible and optimized for clinical settings.
- PII redaction in transcripts is a built-in feature (no separate service needed).

---

## 16. Amazon Translate

### What It Is
A **fully managed neural machine translation (NMT)** service that delivers fast, high-quality, and customizable language translation. It supports real-time and batch translation.

### Key Concepts
- **Real-time translation:** Translate text synchronously via API (up to 10,000 characters per request).
- **Batch translation:** Submit large volumes of documents in S3 for asynchronous translation.
- **Active Custom Translation (ACT):** Customize translation output using parallel data (pairs of source/target sentences) to adapt to domain-specific terminology or style without training a full model.
- **Custom terminology:** Provide a glossary of terms that must always be translated a specific way (e.g., brand names, technical terms).
- **Supported languages:** 75+ languages.
- **Auto language detection:** Automatically detects the source language using Amazon Comprehend under the hood.
- **Formality setting:** Control the level of formality (formal vs. informal) in the output for supported languages.
- **Profanity masking:** Replace profanity in translations with masked characters.
- **Translation memory:** Consistent translations using stored previously translated content.

### When to Use
- Translating user-generated content (reviews, posts) in real time for multilingual platforms.
- Localizing application content, documentation, or product descriptions.
- Processing multilingual documents in batch (contracts, support tickets).
- Enabling multilingual chatbots (combined with Lex or Bedrock).
- Translating communication in contact centers for non-native speakers.

### Key Facts for the Exam
- Translate uses **Neural Machine Translation (NMT)** – not rule-based; produces more natural output.
- **Custom terminology** = always translate a specific term a specific way (glossary).
- **Active Custom Translation (ACT)** = domain fine-tuning using parallel sentence pairs.
- Translate integrates with **Comprehend** for automatic source language detection.
- For multilingual NLP pipelines: Translate → Comprehend → store results.
- HIPAA eligible and supports in-transit and at-rest encryption.

---

## Quick Comparison Reference

| Service | Category | Input | Output | Key Differentiator |
|---|---|---|---|---|
| A2I | Human-in-the-loop | ML predictions | Human review workflow | Human review for any ML model |
| Bedrock | Generative AI platform | Text, image, video | Text, image, video | Access to multiple FMs + RAG + Agents |
| Comprehend | NLP | Text | Entities, sentiment, topics | Pre-built + custom NLP |
| Fraud Detector | Fraud detection | Event data | Fraud score / outcome | ML + rules engine |
| Kendra | Enterprise search | Documents | Search results / answers | Natural language enterprise search |
| Lex | Conversational AI | Text, voice | Conversation / intent | Chatbot & voice bot builder |
| Nova | Foundation models | Text, image, video, audio | Text, image, video, audio | Amazon's own FM family |
| Personalize | Recommendations | User-item interactions | Recommendations | Real-time personalized recommendations |
| Polly | Text-to-speech | Text | Audio (speech) | Lifelike neural TTS |
| Q Developer | Dev assistant | Code, natural language | Code, explanations, fixes | AI coding assistant + security scanning |
| Q Business | Enterprise assistant | Company data + queries | Answers with citations | Employee-facing RAG assistant |
| Rekognition | Computer vision | Images, video | Labels, faces, text | Pre-built + custom image/video analysis |
| SageMaker AI | ML platform | Any data | Custom ML models | End-to-end custom ML lifecycle |
| Textract | Document AI | Documents, images | Extracted text & structure | OCR + form/table structure extraction |
| Transcribe | Speech-to-text | Audio, video | Text transcript | ASR with diarization & redaction |
| Translate | Translation | Text | Translated text | NMT with custom terminology |

---

## Key Exam Themes

### Managed AI Services vs. Custom ML
- **Use managed AI services** (Rekognition, Comprehend, Polly, Translate, etc.) when the use case fits – they are pre-trained, require no ML expertise, and integrate quickly.
- **Use SageMaker** when you need a custom model, have unique data, or need full control over the ML process.
- **Use Bedrock** for generative AI and foundation model access.

### Generative AI on AWS
- **Bedrock** = access to multiple foundation models (FMs) including Amazon Nova, Claude, Llama, and others.
- **Nova** = Amazon's own FM family, available via Bedrock.
- **Q Business** = enterprise generative AI assistant built on Bedrock.
- **Q Developer** = developer coding assistant.
- **Bedrock Guardrails** = responsible AI controls (content filtering, PII, topic blocking).
- **Bedrock Agents** = agentic AI that can take actions and orchestrate multi-step tasks.

### Human-in-the-Loop
- **Amazon A2I** adds human review to any ML prediction workflow.
- **SageMaker Ground Truth** is for **labeling training data** (not reviewing predictions).

### Speech and Language Pipeline
- **Transcribe** (speech → text) → **Comprehend** (NLP analysis) → **Translate** (translation) → **Polly** (text → speech) is a common end-to-end pipeline pattern.

### Search vs. Recommendation
- **Kendra** = find information (search). Users query, get relevant documents/answers.
- **Personalize** = surface relevant items proactively (recommendations). System predicts what users will want.

### Document Processing Pipeline
- **Textract** (extract text + structure) → **Comprehend** (analyze text) → **A2I** (human review if needed) → store in database.

---

*Last updated: March 2026 | AWS AI Practitioner Exam (AIF-C01)*