# AIF-C01 | Task 3.4: Methods to Evaluate Foundation Model Performance

---

## 1. Approaches to Evaluate FM Performance

Evaluating FMs is more complex than evaluating traditional ML models because outputs are often **open-ended, subjective, and multi-dimensional**. A combination of automated metrics and human judgment is typically needed.

---

### Human Evaluation
- Humans assess model outputs directly — the **gold standard** for quality but expensive and slow.
- **Use cases**: Evaluating tone, helpfulness, creativity, safety, factual accuracy.
- **Common approaches**:
  - **Preference ranking**: Show raters two responses and ask which is better (used in RLHF).
  - **Likert scale rating**: Rate response quality on a scale (1–5) across dimensions.
  - **Pass/fail**: Does the response meet a specific criterion?
  - **Side-by-side comparison**: Compare baseline model vs. new model outputs.
- **Evaluation dimensions** for human raters:
  - Accuracy / factual correctness
  - Relevance to the prompt
  - Coherence and fluency
  - Helpfulness
  - Harmlessness / safety
  - Conciseness

**Pros:**
- Captures nuance, context, and subjective quality
- Detects subtle safety and alignment issues
- Most aligned with real user experience

**Cons:**
- Expensive and time-consuming
- Inconsistent between raters (inter-rater variability)
- Doesn't scale easily

> 💡 **Exam Tip**: Human evaluation is the **most accurate** but **least scalable** method. It is the basis of RLHF reward model training.

---

### Benchmark Datasets
- **Standardized datasets and tasks** used to measure FM capabilities consistently across models.
- Allow **apples-to-apples comparison** between different models or versions.
- Scores on benchmarks enable the community to track progress over time.

**Common Benchmark Categories:**

| Benchmark | What It Measures |
|---|---|
| **MMLU** (Massive Multitask Language Understanding) | Knowledge across 57 subjects (math, law, medicine, etc.) |
| **HellaSwag** | Commonsense reasoning and sentence completion |
| **HumanEval** | Code generation correctness |
| **TruthfulQA** | Tendency to generate truthful vs. false statements |
| **GSM8K** | Grade school math word problems (reasoning) |
| **MT-Bench** | Multi-turn conversation quality |
| **BIG-Bench** | Diverse tasks beyond standard NLP benchmarks |

**Pros:**
- Reproducible and objective
- Easy to compare models
- No human raters needed

**Cons:**
- Benchmarks can be "gamed" (models trained on benchmark data)
- May not reflect real-world task performance
- Static benchmarks become outdated

> 💡 **Exam Tip**: Benchmarks = **standardized, reproducible comparison** across models. Know that benchmark scores alone don't guarantee real-world task performance.

---

### Amazon Bedrock Model Evaluation
- AWS's **managed service** for evaluating FM performance within Amazon Bedrock.
- Allows you to compare models and evaluate custom fine-tuned versions.

**Two evaluation modes:**

| Mode | Description |
|---|---|
| **Automatic Evaluation** | Uses built-in metrics and benchmark datasets to score models programmatically without human involvement |
| **Human Evaluation** | Routes model outputs to human reviewers (internal team or AWS-managed workforce via Amazon Mechanical Turk) for quality rating |

**Key capabilities:**
- Define **custom evaluation tasks** aligned to your specific use case.
- Evaluate across multiple dimensions: accuracy, robustness, toxicity, helpfulness.
- Compare **multiple models side-by-side** to select the best one.
- Supports evaluation of **fine-tuned models** vs. base models.
- Generates evaluation reports for audit and governance.

**Evaluation job inputs:**
- A **prompt dataset** (the questions/tasks)
- Expected outputs (for automatic scoring) or human rater instructions

> 💡 **Exam Tip**: Amazon Bedrock Model Evaluation is the AWS-managed answer when a question asks how to **compare FMs** or **evaluate a fine-tuned model** within AWS. Know both automatic and human evaluation modes.

---

## 2. Key Metrics for FM Evaluation

### ROUGE (Recall-Oriented Understudy for Gisting Evaluation)
- Measures **text overlap** between a model's generated output and one or more reference (human-written) outputs.
- Primarily used for **summarization** and **translation** tasks.
- **Recall-oriented**: Focuses on how much of the reference text is captured in the generated output.

**ROUGE Variants:**

| Variant | What It Measures |
|---|---|
| **ROUGE-N** | N-gram overlap (ROUGE-1 = unigrams, ROUGE-2 = bigrams) |
| **ROUGE-L** | Longest Common Subsequence (LCS) — measures sentence-level structure similarity |
| **ROUGE-W** | Weighted LCS — gives more weight to consecutive matches |

**Formula concept (ROUGE-1 Recall):**
```
ROUGE-1 Recall = (# overlapping unigrams) / (# unigrams in reference)
```

**Example:**
- Reference: "The cat sat on the mat"
- Generated: "The cat sat near the mat"
- ROUGE-1: 5 of 6 reference words matched → ROUGE-1 Recall = 0.83

**Pros:** Simple, widely used, fast to compute.
**Cons:** Doesn't capture semantic similarity — a paraphrase with different words scores low even if the meaning is the same.

> 💡 **Exam Tip**: **ROUGE = summarization evaluation**. It measures word overlap with a reference. High ROUGE = generated text is close to the reference text.

---

### BLEU (Bilingual Evaluation Understudy)
- Measures **precision of n-gram overlap** between generated text and reference text.
- Primarily used for **machine translation** evaluation.
- **Precision-oriented**: Focuses on how much of the generated output appears in the reference.

**Key characteristics:**
- Scores range from **0 to 1** (or 0 to 100%).
- Uses a **brevity penalty** to penalize overly short translations.
- Computes precision across multiple n-gram sizes (1-gram through 4-gram) and takes the geometric mean.

**BLEU vs. ROUGE:**

| Metric | Orientation | Primary Use | Measures |
|---|---|---|---|
| **BLEU** | Precision | Translation | How much of the generated text matches the reference |
| **ROUGE** | Recall | Summarization | How much of the reference is captured in generated text |

**Pros:** Fast, language-agnostic, standard for translation benchmarks.
**Cons:** Doesn't handle synonyms or paraphrases; poor correlation with human judgment on some tasks.

> 💡 **Exam Tip**: **BLEU = translation evaluation**. It is **precision-based** (vs. ROUGE which is **recall-based**). Both measure n-gram overlap but from opposite directions.

---

### BERTScore
- Uses **BERT embeddings** to measure **semantic similarity** between generated and reference text.
- Unlike ROUGE and BLEU, BERTScore captures **meaning**, not just exact word matches.
- Computes token-level cosine similarity between embeddings of generated and reference tokens.
- Returns **Precision, Recall, and F1** scores based on semantic similarity.

**Why BERTScore is better for semantic tasks:**
- "The automobile is red" vs. "The car is red" → BLEU/ROUGE score low (different words), BERTScore high (same meaning).

**Pros:** Semantic-aware, handles synonyms and paraphrases, correlates better with human judgment.
**Cons:** Computationally heavier than ROUGE/BLEU, requires a BERT model to compute.

> 💡 **Exam Tip**: **BERTScore = semantic similarity evaluation**. It's the most sophisticated of the three — use it when meaning matters more than exact word matches. The key differentiator is that it uses **embeddings**, not word overlap.

---

### Additional Metrics Worth Knowing

| Metric | Use Case | What It Measures |
|---|---|---|
| **Perplexity** | Language model quality | How well the model predicts a text sample; lower = better |
| **Accuracy / F1** | Classification tasks | Standard classification metrics |
| **Exact Match (EM)** | Q&A tasks | Whether generated answer exactly matches reference |
| **Toxicity Score** | Safety evaluation | Likelihood of harmful/offensive content |
| **Faithfulness** | RAG evaluation | Whether the response is grounded in retrieved context |
| **Answer Relevance** | RAG evaluation | Whether the response addresses the actual question |
| **METEOR** | Translation/summarization | Like BLEU but also considers synonyms and stemming |

---

### Metrics Summary

| Metric | Best For | Approach | Semantic-Aware? |
|---|---|---|---|
| **ROUGE** | Summarization | N-gram recall overlap | ❌ No |
| **BLEU** | Translation | N-gram precision overlap | ❌ No |
| **BERTScore** | Semantic similarity tasks | Embedding cosine similarity | ✅ Yes |
| **Perplexity** | General LM quality | Probability of text | ❌ No |
| **Exact Match** | Q&A | String comparison | ❌ No |
| **Faithfulness** | RAG pipelines | Grounding verification | ✅ Yes |

---

## 3. Evaluating Whether an FM Meets Business Objectives

Technical metrics alone don't tell you if a model is **delivering business value**. Business evaluation bridges the gap between model scores and real-world outcomes.

### Productivity
- **Question**: Is the model making users or teams more efficient?
- **Metrics**:
  - Time saved per task (e.g., drafting emails, writing code)
  - Number of tasks completed per hour with vs. without AI
  - Reduction in manual review time
  - Employee effort scores (how much work the AI offloads)
- **Example**: A coding assistant reduces average PR review time by 30% → productivity improvement validated.

---

### User Engagement
- **Question**: Are users actively using and trusting the AI feature?
- **Metrics**:
  - Daily/Monthly Active Users (DAU/MAU) of AI features
  - Session length and return rate
  - Thumbs up/down or star ratings on AI responses
  - Adoption rate (% of eligible users using the feature)
  - Abandonment rate (users who stop using the feature)
- **Example**: A chatbot with 80% positive ratings and growing DAU indicates strong user engagement.

---

### Task Completion / Task Accuracy
- **Question**: Does the model successfully complete the tasks it was built for?
- **Metrics**:
  - Task completion rate (% of requests successfully fulfilled)
  - Error rate / failure rate
  - Escalation rate (% of AI responses that required human intervention)
  - First-contact resolution rate (for customer service bots)
- **Example**: A support bot that resolves 70% of tickets without human escalation meets its task completion target.

---

### Other Business KPIs

| Objective | Business Metric |
|---|---|
| Cost reduction | Cost per interaction with AI vs. without |
| Revenue impact | Conversion rate improvement from AI recommendations |
| Customer satisfaction | NPS, CSAT scores comparing AI vs. non-AI interactions |
| Compliance | % of outputs flagged for policy violations |
| Latency / SLA | % of responses delivered within SLA threshold |

> 💡 **Exam Tip**: When a question asks about evaluating if an FM "meets business objectives," think beyond technical metrics. Map the use case to a **business KPI**: productivity = time saved, engagement = user adoption, task completion = success rate.

---

## 4. Evaluating Applications Built with FMs

Applications like RAG pipelines, agents, and multi-step workflows require evaluation beyond single model output quality.

---

### Evaluating RAG Applications
RAG introduces additional components (retrieval + generation) that must be evaluated independently and together.

| Dimension | What to Evaluate | Metric/Method |
|---|---|---|
| **Retrieval Quality** | Are the right chunks being retrieved? | Precision@K, Recall@K, MRR (Mean Reciprocal Rank) |
| **Faithfulness** | Is the generated answer grounded in retrieved context? | Human review, faithfulness score |
| **Answer Relevance** | Does the answer address the actual question? | LLM-as-judge, human review |
| **Context Relevance** | Is the retrieved context actually relevant to the question? | Embedding similarity, human review |
| **End-to-End Accuracy** | Is the final answer correct? | Exact match, human evaluation |

**Evaluation Frameworks for RAG:**
- **RAGAS**: Open-source framework specifically designed to evaluate RAG pipelines across faithfulness, answer relevance, context precision, and context recall.

---

### Evaluating Agent Applications
Agents are harder to evaluate because they take **multi-step actions** and the path to the answer matters as much as the final answer.

| Dimension | What to Evaluate | Method |
|---|---|---|
| **Task Completion** | Did the agent successfully complete the goal? | Pass/fail evaluation on test scenarios |
| **Step Accuracy** | Did the agent take correct intermediate steps? | Trace analysis, step-by-step human review |
| **Tool Use Correctness** | Did the agent call the right tools with the right parameters? | Tool call logging and validation |
| **Efficiency** | Did the agent complete the task in a reasonable number of steps? | Step count, latency measurement |
| **Hallucination in Actions** | Did the agent fabricate tool parameters or take unneeded actions? | Output monitoring, human review |
| **Safety** | Did the agent stay within allowed action boundaries? | Guardrail logs, policy compliance checks |

---

### Evaluating Workflows
- **End-to-end testing**: Run the complete workflow with known inputs and verify expected outputs.
- **Component-level evaluation**: Evaluate each FM call in the workflow independently.
- **Regression testing**: After model updates, verify the workflow still produces acceptable outputs.
- **A/B testing**: Deploy two versions of a workflow and compare user outcomes.
- **Monitoring in production**: Track drift, error rates, latency, and output quality over time using tools like Amazon CloudWatch and Amazon Bedrock model monitoring.

---

### LLM-as-a-Judge
- Use a **powerful LLM to evaluate the outputs** of another model.
- The judge model scores responses on dimensions like accuracy, helpfulness, and safety.
- Cheaper and faster than human evaluation at scale.
- **Risk**: The judge model can have its own biases.
- **Use case**: Automated evaluation of open-ended responses in RAG, agent, and chatbot applications.

---

## 5. Evaluation Strategy by Application Type

| Application | Key Evaluation Focus | Primary Tools/Methods |
|---|---|---|
| **Base FM selection** | Benchmark scores, task accuracy | Benchmark datasets, Bedrock Model Evaluation |
| **Fine-tuned model** | Task-specific accuracy, vs. base model | ROUGE/BLEU/BERTScore, human eval, Bedrock Model Evaluation |
| **RAG pipeline** | Retrieval quality + faithfulness + relevance | RAGAS, faithfulness score, human review |
| **Agent** | Task completion, step accuracy, safety | Trace analysis, pass/fail tests, guardrail logs |
| **Customer-facing chatbot** | User satisfaction, engagement, safety | CSAT, engagement metrics, toxicity scores |

---

## 6. Exam Tips Recap

- ✅ **ROUGE** = summarization, recall-based n-gram overlap.
- ✅ **BLEU** = translation, precision-based n-gram overlap.
- ✅ **BERTScore** = semantic similarity using embeddings — the only one of the three that is semantic-aware.
- ✅ **Human evaluation** = most accurate, least scalable. **Benchmarks** = scalable, reproducible, but may not reflect real-world performance.
- ✅ **Amazon Bedrock Model Evaluation** = AWS managed service for automatic and human-based FM evaluation.
- ✅ Business objectives: **productivity** = time saved, **engagement** = user adoption/ratings, **task completion** = success/escalation rate.
- ✅ **RAG evaluation** needs to cover both retrieval quality (right chunks?) and generation quality (faithful, relevant answer?).
- ✅ **Agent evaluation** must assess intermediate steps, not just the final answer.
- ✅ **LLM-as-a-judge** is a scalable alternative to human evaluation for open-ended outputs.
- ✅ BLEU is **precision**-oriented; ROUGE is **recall**-oriented — know the difference.