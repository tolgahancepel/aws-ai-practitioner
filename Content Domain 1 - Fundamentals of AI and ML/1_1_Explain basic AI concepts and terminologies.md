# AWS Certified AI Practitioner (AIF-C01)
## Content Domain 1: Fundamentals of AI and ML
### Task Statement 1.1: Explain Basic AI Concepts and Terminologies

---

## Table of Contents
1. [Basic AI Terms Defined](#1-basic-ai-terms-defined)
2. [AI vs ML vs GenAI vs Deep Learning](#2-ai-vs-ml-vs-genai-vs-deep-learning)
3. [Types of Inferencing](#3-types-of-inferencing)
4. [Types of Data in AI Models](#4-types-of-data-in-ai-models)
5. [Supervised, Unsupervised, and Reinforcement Learning](#5-supervised-unsupervised-and-reinforcement-learning)
6. [Sample Exam Questions](#6-sample-exam-questions)

---

## 1. Basic AI Terms Defined

### 🤖 Artificial Intelligence (AI)
**Definition:** AI is the broad field of computer science focused on building systems that can perform tasks that typically require human intelligence — such as reasoning, learning, problem-solving, perception, and language understanding.

> **Real-world example:** A spam filter in your email that detects and moves junk mail is an early form of AI. Modern examples include virtual assistants like Amazon Alexa, self-driving cars, and fraud detection systems.

---

### 📊 Machine Learning (ML)
**Definition:** ML is a *subset of AI* where systems learn from data to improve their performance on a task *without being explicitly programmed* for every rule. Instead of hard-coding logic, developers feed data and let the algorithm find patterns.

> **Real-world example:** Netflix's recommendation engine learns from your viewing history to suggest shows you're likely to enjoy — it was never given explicit rules like "if user watched sci-fi, recommend sci-fi." It learned those patterns from millions of users.

---

### 🧠 Deep Learning
**Definition:** Deep learning is a *subset of ML* that uses **neural networks with many layers** (hence "deep") to learn representations of data. It excels at tasks like image recognition, speech recognition, and natural language understanding.

> **Real-world example:** Google Photos can identify faces in thousands of your photos and group them — this is deep learning at work. It recognizes complex visual patterns across millions of images.

---

### 🕸️ Neural Networks
**Definition:** Neural networks are computational models *inspired by the human brain*. They consist of layers of interconnected nodes (neurons):
- **Input Layer** — receives raw data (e.g., pixel values of an image)
- **Hidden Layers** — learn intermediate representations and patterns
- **Output Layer** — produces the final result (e.g., "cat" or "dog")

Each connection has a **weight** that is adjusted during training to reduce errors. More hidden layers = "deeper" network = deep learning.

> **Real-world example:** When you speak to Siri, a neural network processes the sound waves, converts them to text, and understands your intent — all in fractions of a second.

---

### 👁️ Computer Vision (CV)
**Definition:** Computer vision is an AI field that enables machines to **interpret and understand visual information** from images or videos. It uses deep learning to detect objects, classify scenes, track movement, and more.

**Common tasks:**
- Object detection (e.g., detecting pedestrians in a self-driving car)
- Image classification (e.g., identifying tumors in X-rays)
- Facial recognition
- Optical character recognition (OCR)

> **Real-world example:** Amazon Go stores use computer vision to track what items customers pick up and automatically charge them when they leave — no checkout needed.

**AWS Service:** Amazon Rekognition uses computer vision to analyze images and videos.

---

### 💬 Natural Language Processing (NLP)
**Definition:** NLP is an AI field focused on enabling machines to **understand, interpret, and generate human language** (text or speech). It bridges the gap between human communication and computer understanding.

**Common tasks:**
- Sentiment analysis (is this review positive or negative?)
- Machine translation (English → French)
- Named entity recognition (finding names, dates, places in text)
- Text summarization
- Question answering

> **Real-world example:** When you type "cancel my subscription" into a customer support chatbot, NLP understands the *intent* behind your words even without rigid keyword matching.

**AWS Service:** Amazon Comprehend performs NLP tasks like sentiment analysis and entity recognition.

---

### 📐 Model
**Definition:** A model is the **output of training an ML algorithm on data**. It is a mathematical function (or set of rules/weights) that takes inputs and produces predictions or decisions.

Think of it like this: the *algorithm* is the recipe, the *data* is the ingredients, and the *model* is the finished dish.

> **Real-world example:** A weather prediction model has been trained on decades of atmospheric data. When you give it today's temperature, humidity, and wind speed, it predicts whether it will rain tomorrow.

---

### ⚙️ Algorithm
**Definition:** An algorithm is a **step-by-step set of instructions or mathematical procedure** that an AI/ML system follows to learn from data or solve a problem. Different algorithms are suited for different tasks.

**Examples of ML algorithms:**
- Linear Regression (predicting continuous values)
- Decision Trees (classification/regression)
- k-Means Clustering (grouping data)
- Random Forest (ensemble of decision trees)
- Gradient Boosting (e.g., XGBoost)

> **Real-world example:** To detect fraudulent credit card transactions, a bank might use a gradient boosting algorithm that looks at transaction amount, location, time, and merchant type to classify transactions as "legitimate" or "fraud."

---

### 🏋️ Training
**Definition:** Training is the **process of feeding data to an ML algorithm** so it can learn patterns and adjust its internal parameters (weights) to minimize errors. The model iteratively improves by comparing its predictions against known correct answers.

**Key concepts in training:**
- **Training data** — the dataset used to teach the model
- **Loss function** — measures how wrong the model's predictions are
- **Optimizer** — adjusts weights to reduce the loss (e.g., gradient descent)
- **Epochs** — the number of times the model sees the entire training dataset

> **Real-world example:** Training an image classifier on 10,000 labeled cat and dog photos. The model starts with random weights, makes predictions, measures how wrong it is, and adjusts its weights — thousands of times — until it can accurately tell cats from dogs.

---

### 🔮 Inferencing (Inference)
**Definition:** Inferencing is the **process of using a trained model to make predictions on new, unseen data**. Once a model is trained, it is deployed and used in inference mode.

- **Training** = learning phase (done once or periodically)
- **Inferencing** = prediction phase (done continuously in production)

> **Real-world example:** After a fraud detection model is trained, every new credit card transaction runs through the model in milliseconds — that's inference. The model isn't learning anymore; it's just applying what it learned.

---

### ⚖️ Bias
**Definition:** Bias in AI refers to **systematic errors in model predictions** that result in unfair or skewed outcomes. Bias can come from:
- **Data bias** — training data doesn't represent the real world fairly (e.g., underrepresenting certain demographics)
- **Algorithmic bias** — the model's design favors certain outcomes
- **Historical bias** — real-world inequalities embedded in historical data

> **Real-world example:** A hiring algorithm trained on historical hiring data from a company that historically hired mostly men may learn to discriminate against women — even if gender isn't explicitly included as a feature.

**Important for AWS exam:** AWS provides tools like **Amazon SageMaker Clarify** to detect and measure bias in training data and models.

---

### ⚖️ Fairness
**Definition:** Fairness is the principle that an AI system should **treat all individuals or groups equitably** and not produce discriminatory outcomes. Fairness is achieved by measuring and mitigating bias.

**Key fairness metrics:**
- **Demographic parity** — equal prediction rates across groups
- **Equal opportunity** — equal true positive rates across groups

> **Real-world example:** A loan approval model should approve loans at similar rates for equally qualified applicants regardless of race or gender.

---

### 📏 Fit (Underfitting and Overfitting)
**Definition:** "Fit" describes how well a model's predictions match the data it was trained on and generalizes to new data.

| Term | Description | Problem |
|------|-------------|---------|
| **Underfitting** | Model is too simple; fails to capture patterns even in training data | Poor performance on both training and test data |
| **Good fit** | Model captures the true patterns and generalizes well | Ideal — accurate on both training and new data |
| **Overfitting** | Model memorizes training data but fails on new data | Great training performance, poor real-world performance |

**Techniques to prevent overfitting:**
- Regularization (L1, L2)
- Dropout (in neural networks)
- Cross-validation
- More training data

> **Real-world example:** An underfitting model trying to predict house prices using only the number of rooms misses key factors like location. An overfitting model memorizes specific houses in training data and can't price new houses it hasn't seen before.

---

### 🦙 Large Language Models (LLMs)
**Definition:** LLMs are **massive neural networks trained on vast amounts of text data** that can understand and generate human-like text. They use a **transformer architecture** and are trained with billions or even trillions of parameters.

**Key characteristics:**
- Trained on enormous datasets (web pages, books, code, etc.)
- Can perform diverse tasks with little or no task-specific training (zero-shot / few-shot)
- Foundation of modern generative AI

**Examples:** GPT-4, Claude, Amazon Titan, Meta LLaMA

> **Real-world example:** You ask an LLM "Summarize this 10-page legal contract in plain English." The model has never seen that specific contract, but because it learned language patterns from massive training data, it can understand and summarize it accurately.

**AWS Service:** Amazon Bedrock provides access to multiple LLMs (including Amazon Titan) for building generative AI applications.

---

## 2. AI vs ML vs GenAI vs Deep Learning

### The Relationship: A Nested Structure

```
┌─────────────────────────────────────────────┐
│                  AI                         │
│  ┌──────────────────────────────────────┐   │
│  │              ML                      │   │
│  │  ┌───────────────────────────────┐   │   │
│  │  │         Deep Learning         │   │   │
│  │  │  ┌────────────────────────┐   │   │   │
│  │  │  │       GenAI            │   │   │   │
│  │  │  │   (subset of DL)       │   │   │   │
│  │  │  └────────────────────────┘   │   │   │
│  │  └───────────────────────────────┘   │   │
│  └──────────────────────────────────────┘   │
└─────────────────────────────────────────────┘
```

### Comparison Table

| Feature | AI | ML | Deep Learning | GenAI |
|---------|----|----|--------------|-------|
| **Scope** | Broadest field | Subset of AI | Subset of ML | Subset of Deep Learning |
| **Approach** | Any method to mimic human intelligence | Learns from data | Multi-layer neural networks | Learns to generate new content |
| **Data needed** | Varies | Moderate | Large | Very large |
| **Computing power** | Low to high | Moderate | High | Very high |
| **Explainability** | Often high (rule-based) | Moderate | Low ("black box") | Very low |
| **Example** | Rule-based expert system | Spam classifier | Image recognition | ChatGPT, DALL-E |

### Similarities
- All involve **automated decision-making** by computers
- All rely on **data** to function effectively
- All aim to **solve problems** that are difficult to solve with traditional programming
- All can be deployed on **AWS cloud services**

### Key Differences
- **AI** can be rule-based (no learning required); ML, Deep Learning, and GenAI all require learning from data
- **ML** uses structured algorithms on well-defined tasks; Deep Learning handles unstructured data at scale
- **Deep Learning** uses neural networks with many layers; standard ML may use simpler models (decision trees, linear regression)
- **GenAI** specifically focuses on *creating new content* (text, images, code, audio) rather than just classifying or predicting

### What is Generative AI (GenAI)?
**Definition:** Generative AI is a type of AI that can **create new, original content** — text, images, code, audio, video — rather than just analyzing or classifying existing content.

**How it works:** GenAI models learn the underlying patterns and distributions in training data, then generate new samples that are statistically similar but original.

**Examples:**
- **Text generation:** Write an essay, summarize a document, answer a question
- **Image generation:** Create a painting from a text prompt (e.g., Stable Diffusion)
- **Code generation:** Write a Python function from a description (e.g., Amazon CodeWhisperer / Q Developer)
- **Audio/Video generation:** Create synthetic voices or videos

> **Real-world example:** A marketing team uses GenAI to generate 50 different ad copy variations from a single product brief — in minutes instead of days.

---

## 3. Types of Inferencing

Once a model is trained, it is deployed and used for **inferencing** — applying the model to new data to generate predictions. There are two primary modes:

### 🔄 Real-Time (Online) Inferencing
**Definition:** Predictions are made **immediately, on-demand**, as each request arrives. The system processes one input (or a small batch) and returns a result with very low latency.

**Characteristics:**
- Low latency (milliseconds to seconds)
- Typically synchronous (the user waits for the response)
- Higher per-prediction cost
- Always-on infrastructure required

**When to use:**
- Interactive applications requiring instant responses
- Any scenario where the user or system is waiting for the prediction

> **Real-world examples:**
> - Fraud detection: Every credit card swipe is evaluated instantly
> - Recommendation systems: Product suggestions appear as you browse
> - Chatbots: LLM responds to your message in real time
> - Medical diagnosis tools: Instant analysis of uploaded X-ray

**AWS Service:** Amazon SageMaker Real-Time Inference endpoints serve predictions with low latency.

---

### 📦 Batch Inferencing
**Definition:** Predictions are made on a **large dataset all at once**, typically on a scheduled basis. Results are stored and used later rather than returned immediately.

**Characteristics:**
- Higher latency (minutes to hours)
- Asynchronous (results are not needed immediately)
- More cost-efficient for large volumes
- No always-on endpoint needed

**When to use:**
- Processing large volumes of data overnight or periodically
- When results don't need to be instant
- Cost optimization when latency is not critical

> **Real-world examples:**
> - Monthly credit score updates for all customers
> - Nightly product recommendations pre-computed for a retail website
> - Weekly analysis of customer churn risk across all accounts
> - Batch translation of thousands of documents

**AWS Service:** Amazon SageMaker Batch Transform runs batch inference jobs on S3 datasets.

---

### ⚡ Additional Inferencing Types (Bonus Context)

| Type | Description | Use Case |
|------|-------------|---------|
| **Asynchronous Inference** | Queues large requests and returns results when ready | Long-running jobs (e.g., video analysis) |
| **Serverless Inference** | Auto-scales to zero when idle; spins up on demand | Intermittent, unpredictable traffic |
| **Edge Inference** | Runs inference on edge devices (IoT, mobile) without cloud | Low-latency, offline scenarios (e.g., smart cameras) |

---

## 4. Types of Data in AI Models

The quality, type, and structure of data fundamentally determines what AI approach you can use and how well a model will perform.

### 🏷️ Labeled vs. Unlabeled Data

#### Labeled Data
**Definition:** Data that includes **both the input features AND the correct output/answer** (called the label or target). Requires human annotation.

| Input | Label |
|-------|-------|
| Photo of a cat | "cat" |
| Email text | "spam" / "not spam" |
| House features | $450,000 (price) |

**Used in:** Supervised learning
**Challenge:** Expensive and time-consuming to create at scale

> **Real-world example:** Medical imaging datasets where radiologists manually label X-rays as "tumor present" or "no tumor" — each labeled image might cost $50+ to annotate.

#### Unlabeled Data
**Definition:** Data that contains only **input features, without any corresponding output labels**. Much cheaper and more abundant.

**Used in:** Unsupervised learning, self-supervised learning (pre-training LLMs)

> **Real-world example:** Billions of web pages scraped for training an LLM — the text exists but there are no human-provided labels. The model learns patterns from the raw text itself.

---

### 📋 Tabular Data
**Definition:** Data organized in **rows and columns**, like a spreadsheet or database table. Each row is one example (record), and each column is a feature (attribute).

**Characteristics:**
- Structured and well-organized
- Each column has a specific meaning
- Most traditional ML algorithms work well with this format

| CustomerID | Age | Income | Churned |
|-----------|-----|--------|---------|
| 001 | 34 | 75000 | No |
| 002 | 28 | 42000 | Yes |

> **Real-world example:** A bank uses tabular customer data (age, balance, transaction history) with a gradient boosting model to predict loan default risk.

**AWS Service:** Amazon SageMaker Autopilot automatically builds ML models for tabular data.

---

### 📈 Time-Series Data
**Definition:** Data points **collected or indexed in time order**, where the sequence and timestamp matter. The pattern over time is a key feature.

**Characteristics:**
- Has a temporal dimension (hourly, daily, weekly readings)
- Trend, seasonality, and cycles are important
- Past values are used to predict future values

> **Real-world example:**
> - Stock prices recorded every minute
> - IoT sensor readings from a factory machine every second
> - Daily electricity consumption for demand forecasting
> - COVID-19 case counts over time

**AWS Service:** Amazon Forecast is purpose-built for time-series forecasting.

---

### 🖼️ Image Data
**Definition:** Data represented as **grids of pixel values**. Each pixel has color channel values (e.g., RGB). Used in computer vision tasks.

**Characteristics:**
- High dimensionality (a 1080p image has ~6.2 million pixels × 3 channels)
- Requires convolutional neural networks (CNNs) for deep learning
- Preprocessing includes resizing, normalization, augmentation

> **Real-world example:** Satellite imagery analyzed by ML models to detect deforestation, monitor crop health, or identify illegal construction.

**AWS Service:** Amazon Rekognition performs image and video analysis.

---

### 📝 Text Data
**Definition:** Data in **natural language form** — sentences, paragraphs, documents. Used in NLP tasks.

**Characteristics:**
- Unstructured; meaning depends on context, grammar, and semantics
- Must be converted to numerical form (tokenization, embeddings) for ML
- Can be in any language

> **Real-world example:** Customer reviews on Amazon analyzed by NLP models to extract product feedback, identify common complaints, and calculate sentiment scores at scale.

**AWS Services:** Amazon Comprehend (NLP), Amazon Translate (translation), Amazon Textract (text extraction from documents).

---

### 🗂️ Structured vs. Unstructured Data

#### Structured Data
**Definition:** Data with a **predefined schema and format**, organized into clearly defined fields. Easy to store in relational databases and process with traditional tools.

- Tabular data is the classic example
- Examples: CSV files, SQL databases, spreadsheets

#### Unstructured Data
**Definition:** Data **without a predefined format or schema**. More complex to process and analyze but makes up ~80–90% of all data generated.

- Examples: Images, videos, audio files, text documents, social media posts, emails
- Requires AI/deep learning techniques to extract meaning

#### Semi-Structured Data
**Definition:** Has some organization but doesn't fit neatly into tabular rows/columns.

- Examples: JSON files, XML documents, log files, emails (structured headers + unstructured body)

> **Real-world example:** A hospital has structured data (patient age, diagnosis codes in a database) AND unstructured data (doctor's handwritten notes scanned to PDF, MRI images). AI is needed to extract insights from both.

---

## 5. Supervised, Unsupervised, and Reinforcement Learning

### 🎓 Supervised Learning
**Definition:** The model learns from **labeled training data** — data where the correct output (label) is provided for each input. The model learns a mapping from inputs → outputs.

**Analogy:** Like a student learning with an answer key. The student (model) sees questions (inputs) and correct answers (labels), and learns to answer similar questions correctly.

**Two main types:**

#### Classification
- Predicts a **category/class** from a discrete set of outputs
- Examples: Spam detection (spam/not spam), disease diagnosis (positive/negative), image classification (cat/dog/bird)

#### Regression
- Predicts a **continuous numerical value**
- Examples: House price prediction, stock price forecasting, temperature prediction

**Common algorithms:**
- Linear/Logistic Regression
- Decision Trees and Random Forests
- Support Vector Machines (SVM)
- Neural Networks

**When to use:** When you have labeled data and a clear target variable to predict.

> **Real-world example:** A bank trains a supervised model on 5 years of loan data (labeled "defaulted" or "repaid") to predict whether new loan applicants will default.

**AWS Service:** Amazon SageMaker supports all supervised learning algorithms and provides built-in algorithms like XGBoost and Linear Learner.

---

### 🔍 Unsupervised Learning
**Definition:** The model learns from **unlabeled data**, finding hidden patterns, structures, or groupings **without any predefined correct answers**.

**Analogy:** Like a librarian organizing books with no predefined categories — they look at the books' content and naturally group similar books together.

**Main types:**

#### Clustering
- Groups similar data points together
- Examples: Customer segmentation, anomaly detection, document grouping
- Algorithm: k-Means, DBSCAN, Hierarchical Clustering

#### Dimensionality Reduction
- Compresses data by reducing the number of features while preserving important information
- Used for visualization, noise reduction, and preprocessing
- Algorithm: PCA (Principal Component Analysis), t-SNE

#### Association Rule Learning
- Finds relationships between variables in large datasets
- Example: Market basket analysis ("customers who buy X also buy Y")
- Algorithm: Apriori, FP-Growth

**When to use:** When you have unlabeled data and want to discover structure or patterns.

> **Real-world example:** An e-commerce company uses k-Means clustering on customer purchase behavior data (no labels) to discover 5 distinct customer segments — "bargain hunters," "brand loyalists," "occasional buyers," etc. — and targets each with different marketing campaigns.

**AWS Service:** Amazon SageMaker includes built-in unsupervised algorithms like k-Means and PCA.

---

### 🎮 Reinforcement Learning (RL)
**Definition:** An agent **learns by interacting with an environment**, taking actions, receiving **rewards or penalties**, and optimizing its behavior over time to maximize cumulative reward. There is no labeled dataset — the agent learns through trial and error.

**Key components:**
| Component | Description |
|-----------|-------------|
| **Agent** | The learning entity making decisions |
| **Environment** | The world the agent interacts with |
| **State** | Current situation/observation of the environment |
| **Action** | What the agent can do in a given state |
| **Reward** | Feedback signal (positive or negative) after an action |
| **Policy** | The agent's strategy for choosing actions |

**Analogy:** Training a dog with treats. The dog (agent) tries different behaviors (actions), and when it does something right, it gets a treat (reward). Over time it learns which behaviors lead to more treats.

**When to use:**
- Sequential decision-making problems
- When the environment can be simulated
- When explicit labeled data is unavailable but a reward signal can be defined

> **Real-world examples:**
> - **Game playing:** DeepMind's AlphaGo learned to beat world champion Go players through RL — playing millions of games against itself
> - **Robotics:** A robotic arm learns to grasp objects through trial and error
> - **Ad bidding:** An RL agent learns optimal bid amounts to maximize ad ROI
> - **RLHF:** Reinforcement Learning from Human Feedback — used to fine-tune LLMs like ChatGPT and Claude to be more helpful and safe

**AWS Service:** Amazon SageMaker RL supports reinforcement learning with popular frameworks.

---

### Summary Comparison Table

| Aspect | Supervised | Unsupervised | Reinforcement |
|--------|-----------|--------------|---------------|
| **Training data** | Labeled | Unlabeled | No dataset; learns from environment |
| **Goal** | Predict output from input | Discover hidden patterns | Maximize cumulative reward |
| **Feedback** | Correct label provided | None | Reward/penalty from environment |
| **Output** | Class or value | Clusters, associations | Policy (action strategy) |
| **Examples** | Spam filter, price prediction | Customer segmentation, anomaly detection | Game AI, robotics, ad optimization |
| **Human effort** | High (labeling) | Low | Medium (designing reward function) |

---

## 6. Sample Exam Questions

### Question 1
**A data scientist wants to build a model to predict customer churn. She has a dataset of 100,000 customers with historical behavior data and a column indicating whether each customer churned ("Yes"/"No"). Which type of machine learning is most appropriate?**

- A) Unsupervised learning, because the patterns are unknown
- B) Reinforcement learning, because the model needs to interact with customers
- C) Supervised learning, because the dataset includes labeled outcomes
- D) Deep learning, because the dataset is very large

> ✅ **Answer: C** — The dataset has labels ("Yes"/"No" churn), making this a classic supervised classification problem.

---

### Question 2
**A company wants to group its 1 million products into categories based on their descriptions without using any predefined categories. Which machine learning approach is most appropriate?**

- A) Supervised learning — regression
- B) Supervised learning — classification
- C) Reinforcement learning
- D) Unsupervised learning — clustering

> ✅ **Answer: D** — There are no predefined labels, and the goal is to find natural groupings. Clustering (unsupervised learning) is the right approach.

---

### Question 3
**A media streaming company runs a nightly job that scores all 50 million users for their likelihood to subscribe to a premium plan. Results are stored in a database and used the next morning. Which inferencing type does this describe?**

- A) Real-time inferencing
- B) Batch inferencing
- C) Edge inferencing
- D) Synchronous inferencing

> ✅ **Answer: B** — Running predictions on a large dataset on a scheduled basis and storing results is batch inferencing.

---

### Question 4
**Which of the following BEST describes the difference between training and inferencing?**

- A) Training uses labeled data; inferencing uses unlabeled data
- B) Training is performed once; inferencing is only used during development
- C) Training teaches the model using historical data; inferencing uses the trained model to make predictions on new data
- D) Training requires GPUs; inferencing does not

> ✅ **Answer: C** — Training is the learning phase with historical data; inferencing is the deployment phase where the model predicts on new inputs.

---

### Question 5
**A model performs very well on training data but poorly on new, unseen test data. What problem does this indicate?**

- A) Underfitting
- B) High bias
- C) Overfitting
- D) Data imbalance

> ✅ **Answer: C** — When a model memorizes training data but fails to generalize, it is overfitting. The model has learned the noise in the training data rather than the underlying patterns.

---

### Question 6
**An AI hiring tool consistently ranks male candidates higher than equally qualified female candidates. Which AI concept does this illustrate?**

- A) Overfitting
- B) Underfitting
- C) Bias
- D) High variance

> ✅ **Answer: C** — This is AI bias, likely stemming from historical hiring data that reflected past gender imbalances. AWS SageMaker Clarify can help detect such bias.

---

### Question 7
**Which of the following is the MOST accurate description of the relationship between AI, Machine Learning, and Deep Learning?**

- A) They are three separate and unrelated fields
- B) Machine learning is a subset of deep learning, which is a subset of AI
- C) AI is a subset of machine learning, which is a subset of deep learning
- D) Deep learning is a subset of machine learning, which is a subset of AI

> ✅ **Answer: D** — The correct nesting is: Deep Learning ⊂ Machine Learning ⊂ AI.

---

### Question 8
**A company has millions of customer transaction records stored in a database with fields for date, amount, merchant, and location. What type of data is this?**

- A) Unstructured data
- B) Time-series and structured data
- C) Image data
- D) Semi-structured data

> ✅ **Answer: B** — Transaction records are structured (defined schema, tabular format) AND have a time dimension (date field), making them time-series data as well.

---

### Question 9
**Which of the following scenarios BEST illustrates Reinforcement Learning?**

- A) A model trained on labeled medical images to detect tumors
- B) A system that groups news articles into topics without predefined categories
- C) An AI agent that learns to play chess by playing millions of games and receiving win/loss feedback
- D) An NLP model that summarizes customer emails

> ✅ **Answer: C** — Reinforcement learning involves an agent learning through interaction with an environment using rewards/penalties. Game playing with win/loss feedback is the classic RL use case.

---

### Question 10
**What is the PRIMARY distinction between Deep Learning and traditional Machine Learning?**

- A) Deep learning requires labeled data; traditional ML does not
- B) Deep learning uses multi-layered neural networks to automatically learn feature representations; traditional ML often requires manual feature engineering
- C) Deep learning only works on image data; traditional ML works on all data types
- D) Deep learning is always more accurate than traditional ML

> ✅ **Answer: B** — The key differentiator is that deep learning automatically learns hierarchical feature representations through multiple layers, while traditional ML typically requires domain experts to engineer features manually.

---

*End of Task Statement 1.1 Study Notes*

> 💡 **Exam Tips:**
> - Know the nested relationship: **GenAI ⊂ Deep Learning ⊂ ML ⊂ AI**
> - Know when to use **batch vs. real-time** inference (look for latency requirements in scenarios)
> - Be able to identify **supervised vs. unsupervised vs. RL** from scenario descriptions
> - Understand **overfitting vs. underfitting** and their symptoms
> - Remember **AWS-specific services** that map to each concept (Rekognition → CV, Comprehend → NLP, Forecast → Time Series, SageMaker Clarify → Bias detection)