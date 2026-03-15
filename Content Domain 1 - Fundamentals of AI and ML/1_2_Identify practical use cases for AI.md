# AWS Certified AI Practitioner (AIF-C01)
## Content Domain 1: Fundamentals of AI and ML
### Task Statement 1.2: Identify Practical Use Cases for AI

---

## Table of Contents
1. [Where AI/ML Provides Value](#1-where-aiml-provides-value)
2. [When AI/ML Is NOT Appropriate](#2-when-aiml-is-not-appropriate)
3. [Selecting the Right ML Technique](#3-selecting-the-right-ml-technique)
4. [Real-World AI Applications](#4-real-world-ai-applications)
5. [AWS Managed AI/ML Services](#5-aws-managed-aiml-services)
6. [Sample Exam Questions](#6-sample-exam-questions)

---

## 1. Where AI/ML Provides Value

AI and ML are not universal solutions, but there are well-defined categories of problems where they deliver exceptional value. Understanding *why* AI adds value in each category is key to the exam.

---

### 🧠 Assisting Human Decision Making
**What it means:** AI augments human judgment by processing more data, faster, and surfacing insights humans might miss — but humans remain in the loop for final decisions.

**Why AI adds value here:**
- Humans have cognitive limits (attention, memory, speed)
- AI can analyze millions of data points simultaneously
- AI provides probability scores rather than binary answers, giving humans calibrated confidence

**Examples:**
- A doctor reviewing cancer diagnoses is assisted by an AI that highlights suspicious regions in MRI scans — the doctor makes the final call
- A loan officer uses an AI risk score (0–100) to prioritize which applications need closer review
- A cybersecurity analyst is alerted by an AI system when unusual network behavior is detected

> **Real-world example:** Amazon's warehouse operations use AI to suggest optimal picking routes to human workers, reducing walking time by up to 20%. Humans still pick the items; AI optimizes the path.

---

### 📈 Solution Scalability
**What it means:** AI can handle workloads that would be impossible or prohibitively expensive to scale with human labor alone.

**Why AI adds value here:**
- A trained model scores 1 or 1 million records with nearly the same infrastructure cost
- AI runs 24/7 without fatigue, sick days, or salary
- Once built, marginal cost per prediction approaches zero

**Examples:**
- Moderating 500 million social media posts per day for harmful content
- Translating content into 70+ languages for a global product
- Sending personalized recommendations to 200 million e-commerce customers simultaneously
- Real-time fraud screening for 10,000+ card transactions per second

> **Real-world example:** Netflix serves personalized movie recommendations to 260+ million subscribers globally. No human team could manually curate recommendations at this scale — ML makes it economically viable.

---

### 🤖 Automation
**What it means:** AI eliminates the need for human involvement in repetitive, well-defined tasks — freeing people for higher-value work.

**Why AI adds value here:**
- Reduces operational costs
- Eliminates human error in repetitive tasks
- Speeds up processes from hours/days to milliseconds

**Examples:**
- Automatically extracting data from invoices and entering it into accounting systems (instead of manual data entry)
- Auto-routing customer support emails to the right department based on content
- Automatically tagging and categorizing product images in an e-commerce catalog
- Scheduling and dispatching field technicians based on predicted equipment failures

> **Real-world example:** Insurance companies use AI to automatically process and approve/deny simple claims (e.g., minor car dents) in under a minute by analyzing submitted photos — what used to take days of human adjuster work.

---

### Other Key Value Drivers

| Value Driver | Description | Example |
|-------------|-------------|---------|
| **Pattern recognition** | Detecting patterns too subtle for humans | Early disease detection from medical images |
| **Personalization** | Tailoring experiences to individuals at scale | Dynamic website content per user |
| **Predictive maintenance** | Predicting failures before they happen | Alerting before a factory machine breaks down |
| **Natural language interfaces** | Enabling machines to understand human language | Voice-controlled applications |
| **Cost reduction** | Reducing cost per task over time | Automated document processing |

---

## 2. When AI/ML Is NOT Appropriate

Knowing when *not* to use AI is just as important as knowing when to use it. This is a common exam theme.

---

### 💰 Unfavorable Cost-Benefit Analysis
**The problem:** AI development and operation have real costs: data collection, labeling, model training (compute), deployment infrastructure, monitoring, and maintenance. Sometimes the ROI doesn't justify it.

**Signs that AI may not be worth it:**
- The problem can be solved simply with rule-based logic (if/else statements)
- The volume of predictions is low (not enough scale to justify cost)
- A small mistake by the model would be very costly
- Training data is expensive to obtain and the dataset is too small

> **Real-world example:** A small family restaurant wants to predict daily customer volume. A simple spreadsheet averaging the last 4 weeks of data might be 90% as accurate as an ML model — without the cost of data pipelines, model training, and ongoing monitoring.

**Decision framework — ask:**
- How often will this prediction be needed? (Low frequency → may not justify AI)
- What is the cost of a wrong prediction?
- Can simpler logic (rules, statistics) achieve similar results?
- Is there enough quality training data?

---

### 🎯 When a Specific, Exact Outcome Is Required (Not a Prediction)
**The problem:** ML models produce *probabilistic outputs* — they give the most likely answer, not a guaranteed correct answer. Some domains require exact, deterministic outcomes.

**Do NOT use ML when:**
- The output must always be 100% correct (e.g., financial transaction amounts, legal calculations)
- The process requires a fully auditable, deterministic decision trail
- The rules are perfectly known and never change (just code the rules directly)
- Regulatory or compliance requirements demand explainability that ML cannot provide

> **Real-world example:** Calculating how much tax a business owes is a deterministic problem — you apply tax law rules to financial figures. An ML model "predicting" taxes would be inappropriate; the tax code defines exact rules to follow, and a wrong answer has serious legal consequences.

---

### 📉 Insufficient or Poor-Quality Data
**The problem:** ML models are only as good as their training data. Without sufficient volume, diversity, or quality, models will perform poorly or introduce bias.

**Do NOT use ML when:**
- Less than a few hundred to a few thousand labeled examples exist for supervised learning
- Historical data doesn't represent the current real-world situation
- Data is too noisy or inconsistently recorded to train a reliable model

> **Real-world example:** A startup wants to build an AI credit risk model but only has 200 loan records. With so few examples, the model would likely overfit and be unreliable. A better option is to use traditional statistical scorecards or partner with a credit bureau.

---

### ⚙️ Problem Is Better Solved with Traditional Programming
**The problem:** If you can write a clear set of rules that cover all cases, a rule-based system is simpler, cheaper, more reliable, and easier to audit.

**Prefer traditional code when:**
- The logic is fully defined and deterministic
- All edge cases are known and manageable
- Correctness and traceability are critical

> **Real-world example:** Validating that a date entered in a form is in MM/DD/YYYY format — a simple regular expression is faster, 100% accurate, and far cheaper than an ML model.

---

### Summary: AI vs. No AI Decision Checklist

| Factor | Favor AI/ML | Avoid AI/ML |
|--------|------------|-------------|
| Data availability | Large, labeled dataset exists | Little or no data |
| Task type | Pattern recognition, prediction | Exact calculation, rule application |
| Scale | High volume, repetitive | Low volume, infrequent |
| Tolerance for error | Approximate answers acceptable | Must be 100% correct |
| Explainability | Not critical | Regulatory/legal requirement |
| Cost | ROI is positive | Cost exceeds benefit |
| Complexity | Too complex for manual rules | Simple, well-defined logic exists |

---

## 3. Selecting the Right ML Technique

Choosing the correct technique depends on: what type of output you need, what your data looks like, and whether you have labels.

---

### 📉 Regression
**Use when:** You need to predict a **continuous numerical value**.

**Output:** A number (e.g., price, temperature, revenue, score)

**Key algorithms:**
- Linear Regression (simple, interpretable)
- Polynomial Regression
- Ridge / Lasso Regression (with regularization)
- Gradient Boosting Regression (e.g., XGBoost)
- Neural Network Regression

| Scenario | Why Regression? |
|----------|----------------|
| Predict a house's selling price | Output is a dollar amount (continuous) |
| Forecast next month's electricity demand | Output is kilowatt-hours (continuous) |
| Estimate patient hospital stay duration | Output is number of days (continuous) |
| Predict a student's exam score | Output is a score 0–100 (continuous) |

> **Real-world example:** Zillow's "Zestimate" uses regression models on thousands of home features (square footage, location, bedrooms, recent sales) to estimate a property's market value.

**AWS:** Amazon SageMaker Linear Learner, XGBoost built-in algorithm

---

### 🏷️ Classification
**Use when:** You need to assign an input to one of a **discrete set of categories/classes**.

**Output:** A class label (and often a probability score per class)

**Sub-types:**
- **Binary classification** — Two possible outputs (Yes/No, Spam/Not Spam, Fraud/Legitimate)
- **Multi-class classification** — More than two classes (dog/cat/bird, sentiment: positive/neutral/negative)
- **Multi-label classification** — An input can belong to multiple classes simultaneously (a news article tagged as both "Politics" and "Economy")

**Key algorithms:**
- Logistic Regression (binary)
- Decision Trees, Random Forest
- Gradient Boosting (XGBoost)
- Support Vector Machines
- Neural Networks / Deep Learning

| Scenario | Classification Type |
|----------|-------------------|
| Email: spam or not spam? | Binary |
| Customer sentiment: positive, neutral, negative? | Multi-class |
| Medical diagnosis: which disease? | Multi-class |
| Document tags (can have multiple) | Multi-label |
| Fraud detection: fraudulent or legitimate? | Binary |

> **Real-world example:** Gmail's spam filter classifies every incoming email as "spam" or "not spam" (binary classification) using features like sender reputation, email content, and user behavior.

**AWS:** Amazon SageMaker XGBoost, Linear Learner, Amazon Comprehend (text classification)

---

### 🔵 Clustering
**Use when:** You want to **group similar items together** without predefined labels (unsupervised).

**Output:** Cluster assignments (which group each item belongs to)

**Key algorithms:**
- k-Means (most common; you specify number of clusters k)
- DBSCAN (density-based; discovers clusters of arbitrary shape)
- Hierarchical Clustering

| Scenario | Why Clustering? |
|----------|----------------|
| Segment customers by behavior | No predefined segments; let data reveal groups |
| Group news articles by topic | No labels; group by content similarity |
| Detect anomalies in network traffic | Unusual points form their own "cluster" |
| Organize products into categories | Natural groupings emerge from attributes |

> **Real-world example:** Spotify uses clustering on listening behavior to group users into "taste communities" — people with similar music taste — and then uses these clusters to recommend new artists.

**AWS:** Amazon SageMaker k-Means built-in algorithm

---

### Quick Technique Selection Reference

| Question to ask | Technique |
|----------------|-----------|
| "Predict a number/amount?" | Regression |
| "Predict a category?" (with labels) | Classification |
| "Find natural groups?" (no labels) | Clustering |
| "Find relationships between items?" | Association Rules |
| "Reduce data dimensions?" | Dimensionality Reduction (PCA) |
| "Learn optimal decisions over time?" | Reinforcement Learning |
| "Generate new content?" | Generative AI / LLMs |
| "Detect unusual/anomalous behavior?" | Anomaly Detection |

---

## 4. Real-World AI Applications

### 👁️ Computer Vision
**What it does:** Enables machines to interpret visual content — images and video.

**Applications:**
- **Object detection:** Identify and locate objects in an image (self-driving cars detecting pedestrians)
- **Image classification:** Categorize an image (defect detection in manufacturing)
- **Facial recognition:** Verify or identify individuals
- **Medical imaging:** Detect tumors, fractures, diabetic retinopathy in scans
- **Document digitization (OCR):** Extract text from scanned images
- **Video surveillance:** Detect unusual behavior in security feeds
- **Augmented reality:** Overlay digital content on real-world images

> **Real-world example:** Tesla's Autopilot system uses computer vision (cameras + deep learning) to detect lane markings, traffic lights, pedestrians, and other vehicles in real time.

**AWS Services:** Amazon Rekognition (object detection, facial analysis, content moderation), Amazon Textract (OCR/document analysis)

---

### 💬 Natural Language Processing (NLP)
**What it does:** Enables machines to understand, interpret, and generate human language.

**Applications:**
- **Sentiment analysis:** Determine if text is positive, negative, or neutral
- **Named entity recognition (NER):** Extract names, dates, places, organizations from text
- **Text classification:** Categorize documents or support tickets automatically
- **Machine translation:** Translate between languages
- **Text summarization:** Condense long documents
- **Question answering:** Answer questions from a document or knowledge base
- **Chatbots/virtual assistants:** Understand and respond to natural language queries

> **Real-world example:** Airlines use NLP to analyze thousands of customer survey responses, automatically categorizing feedback by topic (baggage, service, delays) and sentiment — replacing weeks of manual analysis.

**AWS Services:** Amazon Comprehend (sentiment, entities, topics), Amazon Translate, Amazon Lex (chatbot), Amazon Textract

---

### 🎙️ Speech Recognition
**What it does:** Converts spoken audio into written text (Automatic Speech Recognition — ASR), or synthesizes speech from text (Text-to-Speech — TTS).

**Applications:**
- **Transcription:** Converting call center recordings to text for analysis
- **Voice interfaces:** Hands-free control of devices and applications
- **Live captioning:** Real-time subtitles for meetings or broadcasts
- **Voice authentication:** Identify users by their voice
- **Accessibility tools:** Assistive technology for users with disabilities

> **Real-world example:** Contact centers use speech recognition to transcribe all customer calls in real time, then use NLP to automatically score agent performance, detect compliance violations, and identify trending customer issues — across thousands of simultaneous calls.

**AWS Services:**
- **Amazon Transcribe** — Speech-to-text (ASR)
- **Amazon Polly** — Text-to-speech (TTS)

---

### 🎯 Recommendation Systems
**What it does:** Suggests relevant items to users based on their preferences, behavior, or similarity to other users.

**Types:**
- **Collaborative filtering:** "Users like you also liked..." (based on user behavior patterns)
- **Content-based filtering:** "Because you liked X, here's Y..." (based on item attributes)
- **Hybrid:** Combines both approaches

**Applications:**
- Product recommendations (e-commerce)
- Movie/show recommendations (streaming)
- News article suggestions
- Music playlist generation
- Job matching (recruiting platforms)
- "Similar items" suggestions

> **Real-world example:** Amazon reports that 35% of its revenue comes from its recommendation engine, which analyzes purchase history, browsing behavior, and what similar customers bought to surface relevant products.

**AWS Service:** Amazon Personalize — fully managed recommendation system service that requires no ML expertise

---

### 🕵️ Fraud Detection
**What it does:** Identifies anomalous or suspicious transactions, behaviors, or patterns that indicate fraudulent activity.

**Techniques used:**
- Binary classification (fraud / not fraud)
- Anomaly detection (flag statistically unusual behavior)
- Graph neural networks (detect fraud rings/networks)
- Real-time scoring at transaction time

**Features used (examples):**
- Transaction amount vs. historical average
- Geographic location vs. typical purchase locations
- Time of day and frequency of transactions
- Device fingerprint and IP address
- Merchant category

> **Real-world example:** Mastercard processes over 150 million transactions per hour. Its AI fraud detection scores each transaction in under 100 milliseconds, blocking fraudulent ones before they're approved — with minimal impact to legitimate purchases.

**AWS Service:** Amazon Fraud Detector — purpose-built managed service for fraud detection using ML

---

### 📊 Forecasting
**What it does:** Predicts future values of a variable based on historical data and related factors.

**Applications:**
- **Demand forecasting:** How many units will sell next month? (retail, supply chain)
- **Financial forecasting:** Revenue, cash flow projections
- **Energy forecasting:** Electricity demand prediction for grid management
- **Weather forecasting:** Temperature, precipitation prediction
- **Workforce planning:** Staffing needs based on predicted demand
- **Capacity planning:** Cloud infrastructure needs

> **Real-world example:** Walmart uses ML-based demand forecasting to optimize inventory across 10,500 stores, reducing food waste and ensuring products are in stock. Accurate forecasting is worth billions in reduced holding costs and lost sales prevention.

**AWS Service:** Amazon Forecast — purpose-built time-series forecasting service

---

### Additional AI Application Areas

| Application | Description | AWS Service |
|-------------|-------------|-------------|
| **Search & ranking** | Intelligent search with semantic understanding | Amazon Kendra |
| **Code generation** | AI-assisted software development | Amazon Q Developer |
| **Document processing** | Extract structured data from forms, PDFs | Amazon Textract |
| **Anomaly detection** | Detect unusual metrics in time-series data | Amazon Lookout for Metrics |
| **Personalized marketing** | Targeted campaigns and content | Amazon Personalize |
| **Industrial defect detection** | Visual quality inspection | Amazon Lookout for Vision |

---

## 5. AWS Managed AI/ML Services

AWS offers two tiers of AI services:
- **AI Services (high-level):** Pre-built, API-driven services that require no ML expertise (e.g., Rekognition, Transcribe)
- **ML Platform (Amazon SageMaker):** Full ML development platform for building custom models

---

### 🏗️ Amazon SageMaker AI
**Category:** ML Platform (custom model development)

**What it is:** Amazon SageMaker is AWS's **fully managed, end-to-end ML platform** that covers the entire ML lifecycle — from data preparation through model training, deployment, and monitoring.

**Core capabilities:**

| Capability | Description |
|-----------|-------------|
| **SageMaker Studio** | Integrated IDE for ML development (notebooks, experiments, pipelines) |
| **SageMaker Data Wrangler** | Visual data preparation and feature engineering |
| **SageMaker Feature Store** | Centralized repository for ML features |
| **SageMaker Training** | Managed distributed model training on any framework (TensorFlow, PyTorch, etc.) |
| **SageMaker Autopilot** | AutoML — automatically builds and tunes models for tabular data |
| **SageMaker Endpoints** | Deploy models for real-time and batch inference |
| **SageMaker Clarify** | Bias detection and model explainability |
| **SageMaker Pipelines** | MLOps — automated CI/CD pipelines for ML workflows |
| **SageMaker Model Monitor** | Detect data drift and model degradation in production |
| **SageMaker JumpStart** | Pre-built solution templates and pre-trained models |
| **SageMaker Ground Truth** | Data labeling service with human + automated labeling |

**When to use SageMaker:**
- You need a **custom ML model** trained on your own data
- You need full control over the algorithm, hyperparameters, and architecture
- You're building an end-to-end ML pipeline for production

> **Real-world example:** A bank builds a custom credit risk scoring model using SageMaker. Data scientists use SageMaker Studio to prepare data, train an XGBoost model, evaluate it with Clarify for bias, deploy it as an endpoint, and monitor it with Model Monitor for data drift.

---

### 🎙️ Amazon Transcribe
**Category:** AI Service — Speech-to-Text (ASR)

**What it does:** Automatically converts **audio speech to text** with support for multiple languages, speaker identification, custom vocabulary, and real-time or batch transcription.

**Key features:**
- **Automatic speech recognition (ASR)** for 100+ languages
- **Speaker diarization** — identifies and labels different speakers ("Speaker 1:", "Speaker 2:")
- **Custom vocabulary** — add domain-specific terms (medical jargon, brand names)
- **Redaction** — automatically remove PII (names, phone numbers, SSNs) from transcripts
- **Real-time transcription** — live captions for meetings, broadcasts
- **Medical variant:** Amazon Transcribe Medical for clinical documentation

**Common use cases:**
- Transcribing call center recordings for analysis
- Generating meeting notes and searchable archives
- Providing subtitles and closed captions
- Creating searchable podcast/video content
- Clinical documentation from doctor-patient conversations

> **Real-world example:** A telecommunications company transcribes 500,000 customer service calls per month using Amazon Transcribe, then feeds the text to Amazon Comprehend to identify top complaint categories, reducing the time to insight from weeks to hours.

---

### 🌐 Amazon Translate
**Category:** AI Service — Machine Translation

**What it does:** Provides **fast, affordable, and accurate neural machine translation** between languages, supporting 75+ language pairs.

**Key features:**
- Real-time and batch translation
- **Custom terminology** — ensure brand names or technical terms are translated correctly
- **Active Custom Translation** — fine-tune translation for your domain with your own data
- Supports 75+ languages
- Can be used inline within applications

**Common use cases:**
- Localizing websites, apps, and product catalogs for global markets
- Translating user-generated content (reviews, comments) for analysis
- Cross-language customer support (translate tickets before routing)
- Real-time communication between speakers of different languages
- Multilingual content moderation

> **Real-world example:** An e-commerce platform uses Amazon Translate to instantly translate product descriptions and reviews into 20 languages, enabling global customers to shop in their native language — without hiring 20 teams of human translators.

---

### 🔍 Amazon Comprehend
**Category:** AI Service — Natural Language Processing (NLP)

**What it does:** Analyzes text to **extract insights and meaning** — including sentiment, entities, key phrases, language, and topics — using pre-trained NLP models (no ML experience needed).

**Key features:**

| Feature | Description | Example |
|---------|-------------|---------|
| **Sentiment analysis** | Positive / Negative / Mixed / Neutral | "Great product!" → Positive |
| **Entity recognition** | People, places, organizations, dates, quantities | "Jeff Bezos founded Amazon in 1994" |
| **Key phrase extraction** | Identify the most important phrases in text | "affordable pricing", "fast delivery" |
| **Language detection** | Identify the language of a text | "Bonjour" → French |
| **Topic modeling** | Discover topics across a large document collection | 10,000 articles → 20 topic clusters |
| **Custom classification** | Train a classifier on your own categories | Route support tickets by product type |
| **Custom entity recognition** | Recognize your own domain-specific entities | Detect drug names in medical records |
| **PII detection** | Identify personally identifiable information | Flag SSNs, credit card numbers in text |

**Comprehend Medical:** Specialized variant for extracting medical information from clinical text (diagnoses, medications, dosages, procedures).

> **Real-world example:** A financial services firm processes thousands of analyst reports daily with Amazon Comprehend to automatically extract company names, sentiment, and key financial topics, feeding a dashboard that tracks market sentiment in near real-time.

---

### 🤖 Amazon Lex
**Category:** AI Service — Conversational AI / Chatbot Builder

**What it does:** Provides the technology to **build conversational interfaces (chatbots and voice bots)** using the same deep learning technology that powers Amazon Alexa.

**Key concepts:**

| Term | Definition | Example |
|------|-----------|---------|
| **Intent** | What the user wants to do | "BookFlight", "CheckBalance", "CancelOrder" |
| **Utterances** | Example phrases that express an intent | "I want to fly to NYC", "Book me a flight" |
| **Slots** | Variables/parameters needed to fulfill an intent | Destination, date, seat preference |
| **Fulfillment** | Action taken when intent is recognized | Lambda function that actually books the flight |
| **Session** | A single conversation with a user | One customer service interaction |

**Key features:**
- Automatic speech recognition (ASR) + NLP intent detection
- Multi-turn conversation management
- Integrates with AWS Lambda for fulfillment logic
- Deployable on web, mobile, Slack, Facebook Messenger, Twilio
- Multi-language support

**Common use cases:**
- Customer service chatbots (handle FAQs, check order status)
- IT help desk automation (reset passwords, check ticket status)
- Booking systems (appointments, reservations, flights)
- HR self-service bots (check vacation days, submit expenses)
- Voice interfaces for applications

> **Real-world example:** A bank deploys an Amazon Lex chatbot on its website that handles common queries (account balance, transaction history, branch locations) for 80% of customer inquiries — freeing human agents for complex issues and reducing support costs significantly.

---

### 🔊 Amazon Polly
**Category:** AI Service — Text-to-Speech (TTS)

**What it does:** Converts **text into lifelike speech** using advanced deep learning. Offers dozens of voices across many languages and accents.

**Key features:**
- **Neural TTS (NTTS):** Higher-quality, more natural-sounding voices using neural networks
- **Standard TTS:** Cost-effective, broad language support
- **70+ voices in 30+ languages** with different accents
- **SSML support:** Speech Synthesis Markup Language — control pronunciation, emphasis, pausing, speaking rate, pitch
- **Speaking styles:** Conversational, news broadcaster style
- **Lexicon customization:** Control pronunciation of custom words (brand names, acronyms)
- **Real-time streaming** or generate audio files (MP3, OGG)

**Common use cases:**
- Voicing e-learning courses and training content
- Adding voice to mobile apps and games
- Making websites accessible (read content aloud)
- Generating audio notifications and alerts
- Creating interactive voice response (IVR) systems
- Audiobook and podcast production
- Reading text to visually impaired users

> **Real-world example:** An online education platform uses Amazon Polly to automatically generate audio versions of all written course materials in 10 languages, making content accessible to learners with visual impairments and those who prefer audio learning — without recording studios or voice actors.

---

### AWS AI/ML Services Quick Reference

| Service | Category | Input → Output | Key Use Case |
|---------|----------|----------------|-------------|
| **SageMaker** | ML Platform | Data → Custom Models | Build, train, deploy custom ML models |
| **Transcribe** | AI Service | Audio → Text | Call center transcription, captions |
| **Translate** | AI Service | Text → Translated Text | Multilingual apps, content localization |
| **Comprehend** | AI Service | Text → Insights | Sentiment, entities, topics from text |
| **Lex** | AI Service | Voice/Text → Conversation | Chatbots and voice bots |
| **Polly** | AI Service | Text → Audio | Voice-enable apps, accessibility |
| **Rekognition** | AI Service | Images/Video → Labels | Object detection, facial analysis |
| **Textract** | AI Service | Documents → Structured Data | Form extraction, OCR |
| **Personalize** | AI Service | User data → Recommendations | Product/content recommendations |
| **Forecast** | AI Service | Time-series → Forecasts | Demand, revenue forecasting |
| **Fraud Detector** | AI Service | Transaction data → Risk Score | Online fraud prevention |
| **Kendra** | AI Service | Documents → Search Results | Intelligent enterprise search |
| **Bedrock** | GenAI Platform | Prompts → Generated Content | LLM access, GenAI apps |

---

## 6. Sample Exam Questions

### Question 1
**A retail company wants to automatically predict how many units of each product to order for the holiday season, based on 5 years of sales data. Which AWS service is purpose-built for this use case?**

- A) Amazon Rekognition
- B) Amazon Comprehend
- C) Amazon Forecast
- D) Amazon Lex

> ✅ **Answer: C** — Amazon Forecast is purpose-built for time-series forecasting, including demand forecasting for retail inventory planning.

---

### Question 2
**A company wants to add a chatbot to their website that can understand customer questions about account balances and recent transactions. Which AWS service should they use to build this conversational interface?**

- A) Amazon Polly
- B) Amazon Transcribe
- C) Amazon Lex
- D) Amazon Comprehend

> ✅ **Answer: C** — Amazon Lex is AWS's conversational AI service for building chatbots and voice interfaces. It understands user intent and manages multi-turn conversations.

---

### Question 3
**A startup wants to determine whether they should build an AI model to validate that input dates are in MM/DD/YYYY format. Is this an appropriate use case for ML?**

- A) Yes, because ML can handle complex pattern recognition
- B) Yes, because ML can learn from examples of valid and invalid dates
- C) No, because this is a deterministic rule that can be implemented with simple code (e.g., a regular expression)
- D) No, because ML cannot process text data

> ✅ **Answer: C** — Date format validation has a clear, exact rule. A regex or simple validation function solves this perfectly without the cost and complexity of an ML model. ML is not appropriate when a specific, exact outcome is needed and rules are well-defined.

---

### Question 4
**A hospital wants to analyze thousands of doctor's notes to automatically extract patient diagnoses, medication names, and dosages. Which AWS service is MOST appropriate?**

- A) Amazon Lex
- B) Amazon Transcribe Medical
- C) Amazon Comprehend Medical
- D) Amazon Textract

> ✅ **Answer: C** — Amazon Comprehend Medical is specifically designed to extract medical entities (diagnoses, medications, dosages, procedures) from unstructured clinical text.

---

### Question 5
**A company has customer review data with no labels and wants to discover what major topics customers are discussing. Which ML technique should they use?**

- A) Regression — to predict review scores
- B) Binary classification — to classify reviews as positive or negative
- C) Clustering or topic modeling — to discover natural groupings in unlabeled text
- D) Reinforcement learning — to reward accurate topic identification

> ✅ **Answer: C** — When you have unlabeled data and want to discover natural groupings or topics, unsupervised techniques like clustering or topic modeling are appropriate. Amazon Comprehend's topic modeling feature can do this directly.

---

### Question 6
**An e-learning platform wants to read article text aloud to visually impaired users in a natural-sounding voice across 15 languages. Which AWS service is MOST appropriate?**

- A) Amazon Transcribe
- B) Amazon Lex
- C) Amazon Polly
- D) Amazon Translate

> ✅ **Answer: C** — Amazon Polly converts text to lifelike speech and supports 30+ languages. This is a text-to-speech (TTS) use case.

---

### Question 7
**A data science team needs to build a custom fraud detection model, train it on their proprietary transaction data, deploy it as a real-time endpoint, and monitor it for model drift in production. Which AWS service provides ALL of these capabilities?**

- A) Amazon Fraud Detector
- B) Amazon SageMaker
- C) Amazon Comprehend
- D) Amazon Rekognition

> ✅ **Answer: B** — Amazon SageMaker is the full ML platform covering data prep, training, deployment, and monitoring. Amazon Fraud Detector is a managed service but doesn't offer the full custom model development lifecycle that SageMaker does.

---

### Question 8
**Which of the following scenarios represents an appropriate reason to AVOID using machine learning?**

- A) A company wants to recommend products to 10 million customers based on purchase history
- B) A company needs to calculate exact employee payroll amounts based on hours worked and pay rates
- C) A company wants to detect fraudulent transactions in real time
- D) A company wants to forecast demand across 50,000 products for the next quarter

> ✅ **Answer: B** — Payroll calculation is a deterministic problem with exact, known rules. A wrong answer has legal and financial consequences. ML produces probabilistic outputs and is inappropriate here — traditional software logic should be used.

---

### Question 9
**A global media company publishes content in English and wants to make it available in 75 languages automatically. Which AWS service should they use?**

- A) Amazon Comprehend
- B) Amazon Polly
- C) Amazon Translate
- D) Amazon Lex

> ✅ **Answer: C** — Amazon Translate provides neural machine translation supporting 75+ language pairs, making it ideal for multilingual content localization.

---

### Question 10
**A company is trying to predict house prices. They have a dataset with 50 features (square footage, number of rooms, location, age of house, etc.) and historical sale prices. Which ML technique is most appropriate?**

- A) Clustering — to group similar houses
- B) Classification — to classify houses as expensive or affordable
- C) Regression — to predict a continuous numerical value (price)
- D) Reinforcement learning — to learn optimal pricing strategies

> ✅ **Answer: C** — Predicting a continuous numerical value (house price in dollars) is a regression problem. Clustering would be unsupervised with no price labels. Classification would work if the output were a category (cheap/expensive) rather than an actual price.

---

### Question 11
**A contact center records all customer calls. A manager wants to automatically convert these recordings to text so they can be searched and analyzed. Which AWS service handles this?**

- A) Amazon Polly
- B) Amazon Transcribe
- C) Amazon Comprehend
- D) Amazon Lex

> ✅ **Answer: B** — Amazon Transcribe converts audio speech to text (ASR). Amazon Polly does the opposite (text to speech). After transcription, Amazon Comprehend could then analyze the resulting text.

---

*End of Task Statement 1.2 Study Notes*

> 💡 **Exam Tips:**
> - The exam frequently presents scenarios asking you to identify the **right AWS service** — memorize the service-to-capability mapping table above
> - Know the **"when NOT to use AI"** scenarios: exact/deterministic outcomes, insufficient data, simple rule-based logic, poor cost-benefit
> - For technique selection: **regression = predict a number**, **classification = predict a category**, **clustering = find groups (no labels)**
> - **Transcribe** = audio → text | **Polly** = text → audio (they are opposites — a common trick question)
> - **Comprehend** = understand text (NLP) | **Lex** = build a chatbot | **Translate** = change language
> - **SageMaker** is for custom models; the other services (Rekognition, Comprehend, etc.) are pre-built AI APIs requiring no ML expertise