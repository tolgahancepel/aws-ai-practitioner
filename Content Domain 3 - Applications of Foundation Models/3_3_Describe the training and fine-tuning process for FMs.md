# AIF-C01 | Task 3.3: Training and Fine-Tuning Process for Foundation Models (FMs)

---

## 1. Key Elements of Training a Foundation Model

### Pre-Training
- The **initial, large-scale training phase** where a model learns general knowledge and language understanding from massive datasets.
- The model is exposed to **billions or trillions of tokens** of text (books, websites, code, articles, etc.).
- The model learns to **predict the next token** (or reconstruct masked tokens) — this is called self-supervised learning.
- **Output**: A general-purpose FM with broad capabilities but no task-specific optimization.
- **Cost**: Extremely high — millions of dollars in compute, weeks/months of training time.
- **Who does it**: Large AI labs and cloud providers (AWS, Anthropic, Meta, etc.).

**What the model learns during pre-training:**
- Grammar, syntax, and semantics of language
- World knowledge (facts, relationships, concepts)
- Reasoning patterns
- Code, math, and logic structures

---

### Fine-Tuning
- Further training of a **pre-trained FM on a smaller, task-specific dataset** to specialize its behavior.
- The model's weights are **updated** (unlike RAG or prompting, which don't change weights).
- Requires **labeled examples** of the desired input-output behavior.
- **Output**: A model adapted for a specific task, domain, or style.
- **Cost**: Moderate — much less than pre-training, but requires compute and labeled data.

**Types of fine-tuning covered in next section.**

---

### Continuous Pre-Training
- Also called **domain-adaptive pre-training**.
- Continues the pre-training process on a **domain-specific unlabeled corpus** after the initial pre-training.
- The model learns new domain vocabulary, concepts, and patterns **without needing labeled data**.
- **Use cases**:
  - Medical: train on clinical notes, research papers
  - Legal: train on case law, contracts
  - Financial: train on SEC filings, market reports
  - Code: train on proprietary codebases
- **Cost**: High — similar to pre-training but on a smaller, focused dataset.
- **Difference from fine-tuning**: Uses unlabeled data; updates domain knowledge rather than task behavior.

> 💡 **Exam Tip**: Continuous pre-training = update the model's **knowledge** with unlabeled domain data. Fine-tuning = update the model's **behavior** with labeled task data.

---

### Distillation (Knowledge Distillation)
- The process of training a **smaller "student" model** to mimic the behavior of a **larger "teacher" model**.
- The student learns from the teacher's output probabilities (soft labels) rather than just ground-truth labels.
- **Goal**: Compress a large model into a smaller, faster, cheaper model that retains most of the capability.
- **Benefits**:
  - Lower inference cost and latency
  - Smaller memory footprint
  - Easier to deploy on edge devices
- **Tradeoff**: Some capability loss compared to the full teacher model.
- **Example**: Distilling a 70B parameter model into a 7B model that behaves similarly for specific tasks.

> 💡 **Exam Tip**: Distillation = **shrink a big model into a small one** while preserving performance. It's about efficiency and deployment cost reduction.

---

### Training Phases Summary

| Phase | Data Type | Data Size | Cost | Output |
|---|---|---|---|---|
| **Pre-Training** | Unlabeled (self-supervised) | Billions/trillions of tokens | Extremely High | General-purpose FM |
| **Continuous Pre-Training** | Unlabeled domain-specific | Millions–billions of tokens | High | Domain-knowledgeable FM |
| **Fine-Tuning** | Labeled task-specific | Hundreds–thousands of examples | Medium | Task/domain-specialized FM |
| **Distillation** | Teacher model outputs | Varies | Medium | Smaller, efficient model |

---

## 2. Methods for Fine-Tuning a Foundation Model

### Instruction Tuning
- Fine-tunes the model on **instruction-response pairs** to teach it to follow natural language instructions.
- Training data format: `{"instruction": "Summarize this text", "response": "..."}`
- Makes the model better at **understanding and following user commands**.
- Most modern chat models (e.g., Claude, GPT, Llama-Instruct) are instruction-tuned on top of a base model.
- **Variants**:
  - **Supervised Fine-Tuning (SFT)**: Train on human-written instruction-response examples.
  - **RLHF** (covered in Section 3): Refine further using human preference feedback.

> 💡 **Exam Tip**: Instruction tuning is why models can follow commands like "Summarize," "Translate," or "Write code for..." rather than just predicting the next word.

---

### Domain Adaptation
- Fine-tuning a model to **specialize in a specific field or industry** using domain-specific labeled data.
- The model learns domain-specific terminology, norms, and reasoning patterns.
- **Examples**:
  - A general LLM → fine-tuned on medical records → medical assistant model
  - A general LLM → fine-tuned on legal documents → legal contract analyzer
  - A general LLM → fine-tuned on customer support logs → customer service bot

**Difference from continuous pre-training:**
- Domain adaptation (fine-tuning) uses **labeled** data and optimizes for a specific **task**.
- Continuous pre-training uses **unlabeled** data and updates **domain knowledge** broadly.

---

### Transfer Learning
- The broader concept underlying all fine-tuning: **reuse knowledge learned in one context and apply it to a new context**.
- Pre-training captures general knowledge → transfer it to a specific task via fine-tuning.
- Enables high performance with **much less data** than training from scratch.
- The pre-trained model's weights serve as a powerful starting point (vs. random initialization).
- **Why it works**: The FM has already learned general language structure, so fine-tuning only needs to teach task-specific behavior.

```
Pre-trained FM (general knowledge)
        │
        ▼  Transfer Learning
Fine-Tuned Model (task-specific behavior)
```

> 💡 **Exam Tip**: Transfer learning is the **foundational concept** behind why fine-tuning works efficiently. It explains why you don't need millions of labeled examples — the model already has a strong base.

---

### Parameter-Efficient Fine-Tuning (PEFT)
- Fine-tuning approaches that update **only a small subset of model parameters** rather than all weights.
- Dramatically reduces compute cost and storage requirements.
- **LoRA (Low-Rank Adaptation)**: Adds small trainable matrices to existing layers; only these are updated.
- **Adapters**: Insert small trainable modules between existing layers.
- **Benefits**: Faster training, lower cost, less risk of catastrophic forgetting, multiple fine-tuned versions from one base model.

---

### Fine-Tuning Methods Summary

| Method | What It Teaches | Data Type | Key Benefit |
|---|---|---|---|
| **Instruction Tuning** | How to follow instructions | Labeled instruction-response pairs | Improves instruction-following |
| **Domain Adaptation** | Domain-specific knowledge + behavior | Labeled domain examples | Specializes for an industry |
| **Transfer Learning** | (Underlying concept) Reuse general knowledge | Any labeled data | Efficient learning from less data |
| **Continuous Pre-Training** | Domain vocabulary and concepts | Unlabeled domain corpus | Expands domain knowledge |
| **PEFT / LoRA** | Task-specific behavior | Labeled data | Low cost, efficient fine-tuning |

---

## 3. Preparing Data for Fine-Tuning

Data quality is **the most critical factor** in fine-tuning success. Garbage in = garbage out.

### Data Curation
- The process of **selecting, cleaning, and organizing** data for fine-tuning.
- Steps include:
  - **Filtering**: Remove low-quality, irrelevant, or duplicate records.
  - **Deduplication**: Prevent the model from overfitting on repeated examples.
  - **Format standardization**: Ensure consistent structure (e.g., all examples in `instruction/response` format).
  - **Noise removal**: Remove HTML tags, formatting artifacts, encoding errors.
  - **Sensitive data removal**: Strip PII, credentials, confidential information.

---

### Data Governance
- Policies and processes that ensure data used for training is **legal, ethical, and compliant**.
- Key governance concerns:
  - **Licensing**: Do you have rights to use the data for training?
  - **Privacy compliance**: GDPR, HIPAA — avoid training on regulated personal data.
  - **Bias auditing**: Check that data doesn't systematically over/under-represent groups.
  - **Data lineage**: Track where data came from for auditability.
  - **Access control**: Restrict who can view or modify training datasets.

---

### Data Size
- **More data generally = better performance**, but diminishing returns apply.
- Fine-tuning typically needs **hundreds to thousands** of high-quality examples (vs. billions for pre-training).
- **Quality > Quantity**: 500 well-crafted examples often outperform 5,000 noisy ones.
- Minimum viable dataset size depends on:
  - Task complexity
  - How different the task is from the base model's pre-training
  - Desired accuracy level

---

### Data Labeling
- **Supervised fine-tuning requires labeled data** — each input must have a correct expected output.
- **Labeling approaches**:
  - **Human annotation**: Most accurate but expensive and slow (e.g., Amazon SageMaker Ground Truth).
  - **Expert annotation**: Domain experts label specialized data (medical, legal).
  - **Programmatic/automated labeling**: Rules or weaker models generate labels (faster, less accurate).
  - **LLM-assisted labeling**: Use a strong LLM to generate initial labels, then humans verify.
- **Label quality** directly determines model quality — inconsistent labels = inconsistent model behavior.

---

### Representativeness
- Training data must **represent the full range of real-world inputs** the model will encounter.
- **Risks of non-representative data**:
  - **Bias**: Model performs well on over-represented groups and poorly on under-represented ones.
  - **Distributional shift**: Model fails when deployed data differs from training data.
- **Best practices**:
  - Include diverse examples across demographics, languages, edge cases.
  - Balance classes (for classification tasks — avoid heavy class imbalance).
  - Include both easy and hard examples.
  - Mirror the real production distribution as closely as possible.

> 💡 **Exam Tip**: Non-representative data is one of the **primary causes of bias** in ML models. Always consider diversity and balance when preparing fine-tuning data.

---

### Reinforcement Learning from Human Feedback (RLHF)
- A technique to align a model's outputs with **human values and preferences**.
- Goes beyond supervised fine-tuning to optimize for what humans actually *prefer*, not just what's technically correct.

**RLHF Process (Step by Step):**

```
Step 1: Supervised Fine-Tuning (SFT)
├── Train model on high-quality instruction-response examples
└── Output: Initial fine-tuned model

Step 2: Train a Reward Model
├── Show human raters pairs of model outputs
├── Humans rank/prefer one output over another
└── Train a separate "reward model" to predict human preference scores

Step 3: Reinforcement Learning Optimization
├── Use the reward model as a feedback signal
├── Optimize the fine-tuned model using PPO (Proximal Policy Optimization)
└── Model learns to generate outputs that score higher on human preference

Output: Aligned model that produces helpful, harmless, honest responses
```

**Why RLHF matters:**
- Reduces harmful, biased, or misleading outputs.
- Makes models more helpful and aligned with human intent.
- Powers the alignment of models like Claude, ChatGPT, and Llama-Chat.

**RLHF Variants:**
- **RLAIF (RL from AI Feedback)**: Use an AI model instead of humans to provide preference feedback — cheaper and faster.
- **DPO (Direct Preference Optimization)**: A simpler alternative to RLHF that directly optimizes on human preference data without a separate reward model.

> 💡 **Exam Tip**: RLHF is the key technique for making models **safe, helpful, and aligned**. It uses **human preference rankings** (not just correct/incorrect labels) to improve the model. It is applied *after* initial supervised fine-tuning.

---

### Data Preparation Checklist

| Step | What to Do | Why It Matters |
|---|---|---|
| **Curation** | Filter, deduplicate, clean, standardize | Prevents noisy/inconsistent training |
| **Governance** | Check licensing, privacy, compliance | Legal and ethical use of data |
| **Sizing** | Aim for quality > quantity | Efficient and effective training |
| **Labeling** | Human or expert annotation | Supervised learning requires correct labels |
| **Representativeness** | Diverse, balanced, edge cases | Prevents bias and distributional shift |
| **RLHF** | Human preference ranking for alignment | Makes model helpful, harmless, honest |

---

## 4. AWS Services for Fine-Tuning

| Service | Role |
|---|---|
| **Amazon Bedrock** | Fine-tune supported FMs (Titan, Llama, etc.) via a managed interface — no infrastructure management |
| **Amazon SageMaker** | Full MLOps platform for custom fine-tuning workflows, including PEFT/LoRA |
| **Amazon SageMaker Ground Truth** | Managed data labeling service with human annotators |
| **AWS Data Exchange** | Source licensed third-party datasets for training/fine-tuning |
| **Amazon S3** | Store training datasets, model artifacts, and outputs |

---

## 5. Exam Tips Recap

- ✅ **Pre-training** = general knowledge from massive unlabeled data. **Fine-tuning** = task-specific behavior from labeled data.
- ✅ **Continuous pre-training** = domain knowledge update with **unlabeled** corpus (not the same as fine-tuning).
- ✅ **Distillation** = compress a large model into a smaller, faster one.
- ✅ **Instruction tuning** teaches the model to follow commands. It's the basis of all chat/assistant models.
- ✅ **Transfer learning** is the concept that makes fine-tuning efficient — pre-trained knowledge transfers to new tasks.
- ✅ **Data quality > data quantity** for fine-tuning. Curate, clean, and balance your dataset.
- ✅ **Non-representative data = biased model.** Always ensure diversity and balance.
- ✅ **RLHF** = human preference rankings → reward model → RL optimization → aligned model.
- ✅ **RLHF happens after SFT** — it's a refinement step, not a replacement for supervised fine-tuning.
- ✅ **Amazon Bedrock** manages fine-tuning infrastructure. **SageMaker Ground Truth** handles data labeling.