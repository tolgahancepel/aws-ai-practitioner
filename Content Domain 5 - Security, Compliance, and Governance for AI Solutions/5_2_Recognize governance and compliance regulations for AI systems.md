# AIF-C01 | Task 5.2: Governance and Compliance Regulations for AI Systems

---

## 1. AWS Services for Governance and Compliance

### AWS Config
- A **continuous configuration monitoring and compliance service** that records the configuration state of AWS resources over time.
- **Key capabilities**:
  - Records all configuration changes to AWS resources (S3 buckets, IAM policies, SageMaker endpoints, etc.).
  - Evaluates resources against **Config Rules** — predefined or custom compliance checks.
  - Provides a **configuration timeline** showing exactly when and how resources changed.
  - Triggers automated remediation when non-compliant resources are detected.
- **AI governance use cases**:
  - Verify S3 buckets storing training data have encryption enabled.
  - Detect IAM policies that grant overly broad Bedrock access.
  - Ensure SageMaker notebooks are deployed within a VPC.
  - Confirm KMS encryption is applied to SageMaker model artifacts.
  - Track configuration drift in ML infrastructure.

**Key Config Rules for AI systems:**
```
✅ s3-bucket-server-side-encryption-enabled
✅ sagemaker-notebook-instance-inside-vpc
✅ sagemaker-endpoint-config-kms-key-configured
✅ iam-no-inline-policy-check
✅ restricted-ssh (no open SSH on SageMaker instances)
```

> 💡 **Exam Tip**: **AWS Config** = continuous compliance monitoring and resource configuration history. If a question asks about detecting misconfigured AI infrastructure or proving compliance over time, Config is the answer.

---

### Amazon Inspector
- **Automated vulnerability management** service that continuously scans AWS workloads for software vulnerabilities and unintended network exposure.
- **What it scans**:
  - EC2 instances (OS and application vulnerabilities).
  - Amazon ECR container images (including SageMaker custom containers).
  - AWS Lambda functions.
- **AI use cases**:
  - Scan custom SageMaker training and inference containers for CVEs.
  - Detect outdated ML framework versions (TensorFlow, PyTorch) with known vulnerabilities.
  - Identify unintended network exposure of SageMaker instances.
- **Output**: Findings with severity scores (Critical, High, Medium, Low) and remediation guidance.

> 💡 **Exam Tip**: **Amazon Inspector** = automated **vulnerability scanning** for compute and containers. For SageMaker custom containers with ML framework vulnerabilities, Inspector is the tool.

---

### AWS Audit Manager
- Automates **evidence collection for compliance audits**, mapping AWS usage to specific compliance frameworks.
- **Key capabilities**:
  - Pre-built frameworks for common regulations: **HIPAA, GDPR, SOC 2, PCI DSS, NIST, FedRAMP**.
  - Continuously collects evidence from AWS services (Config, CloudTrail, Security Hub).
  - Organizes evidence into audit-ready reports for auditors and regulators.
  - Supports **custom frameworks** for organization-specific compliance requirements.
- **AI governance use cases**:
  - Automate evidence collection for AI model governance audits.
  - Map Bedrock and SageMaker controls to HIPAA or GDPR requirements.
  - Generate audit reports demonstrating responsible AI practices.
  - Track compliance posture for AI systems across the development lifecycle.

> 💡 **Exam Tip**: **AWS Audit Manager** = automated audit evidence collection and reporting. If a question mentions "audit," "compliance framework," or "demonstrating compliance to regulators," Audit Manager is the answer.

---

### AWS Artifact
- A **self-service portal** providing on-demand access to AWS's **compliance documentation and agreements**.
- **What it provides**:
  - **Compliance reports**: SOC 1/2/3, ISO 27001, PCI DSS, FedRAMP, HIPAA, GDPR reports about AWS infrastructure.
  - **AWS Agreements**: BAA (Business Associate Agreement for HIPAA), GDPR Data Processing Addendum.
  - Evidence that **AWS's infrastructure** meets compliance requirements (not the customer's applications).
- **AI governance use cases**:
  - Download AWS compliance reports to provide to auditors as evidence of infrastructure security.
  - Sign a HIPAA BAA before deploying AI systems that process patient data on AWS.
  - Provide regulators with proof that the underlying cloud platform is compliant.

**Artifact vs. Audit Manager:**
| Service | Purpose |
|---|---|
| **AWS Artifact** | Access AWS's own compliance reports and agreements |
| **AWS Audit Manager** | Collect and organize evidence about YOUR AWS usage for audits |

> 💡 **Exam Tip**: **AWS Artifact** = download AWS's compliance certificates and sign agreements. **Audit Manager** = collect evidence about your own resources. They are complementary, not the same.

---

### AWS CloudTrail
- Records a **complete, tamper-evident audit log of all API activity** across AWS accounts.
- **What it captures**:
  - Who made a request (IAM user, role, service).
  - What action was taken (API call).
  - What resource was affected.
  - When it happened (timestamp).
  - Where it came from (IP address, region).
- **AI governance use cases**:
  - Audit all Amazon Bedrock API calls — who invoked which models and when.
  - Track access to sensitive training data in S3.
  - Detect unauthorized changes to SageMaker model endpoints.
  - Investigate security incidents involving AI systems.
  - Demonstrate access audit trail for regulatory compliance.
- **CloudTrail Lake**: Enables SQL-based querying of CloudTrail logs for compliance investigation.

> 💡 **Exam Tip**: **CloudTrail** = the **audit trail** for all AWS API activity. It is the foundational service for security investigation, compliance auditing, and forensics in AI systems. "Who did what, when, and where" → CloudTrail.

---

### AWS Trusted Advisor
- An automated **best practices advisory service** that analyzes your AWS environment and provides recommendations across five categories:
  - **Cost Optimization**
  - **Performance**
  - **Security**
  - **Fault Tolerance**
  - **Service Limits**
- **AI governance use cases**:
  - Identify S3 buckets with public access (training data exposure risk).
  - Flag IAM users with excessive permissions.
  - Alert on SageMaker service limit approaching (training job quotas).
  - Detect underutilized resources in ML infrastructure (cost optimization).
- **Access levels**: Basic/Developer (limited checks); Business/Enterprise (full checks + AWS Support API).

> 💡 **Exam Tip**: **Trusted Advisor** = automated best-practice recommendations across security, cost, performance, and limits. It's advisory — it identifies issues but doesn't automatically fix them (unlike Config remediation).

---

### Governance Services Summary

| Service | Primary Function | Key AI Use Case |
|---|---|---|
| **AWS Config** | Continuous resource compliance monitoring | Detect misconfigured AI infrastructure |
| **Amazon Inspector** | Vulnerability scanning | Scan ML containers for CVEs |
| **AWS Audit Manager** | Automated audit evidence collection | Map AI controls to compliance frameworks |
| **AWS Artifact** | Download AWS compliance reports/agreements | HIPAA BAA, SOC 2 reports for auditors |
| **AWS CloudTrail** | API audit logging | Track all Bedrock/SageMaker API calls |
| **AWS Trusted Advisor** | Best practice recommendations | Identify security and cost issues in AI infra |

---

## 2. Data Governance Strategies

Data governance for AI systems ensures that data used in training, inference, and outputs is **managed responsibly, securely, and in compliance with regulations** throughout its entire lifecycle.

---

### Data Lifecycle Management
- Define and enforce **policies for each stage** of data's life within AI systems.

**AI data lifecycle stages:**

```
[Collection] → [Ingestion] → [Storage] → [Processing/Training]
     ↓
[Inference Use] → [Output Logging] → [Archival] → [Deletion]
```

**Lifecycle governance actions:**
- **Collection**: Document sources, verify licensing, assess for PII.
- **Ingestion**: Validate quality, apply transformations, tag with metadata.
- **Storage**: Encrypt, apply access controls, enable versioning.
- **Processing**: Track transformations for lineage; apply privacy-enhancing techniques.
- **Training**: Record dataset versions and configurations used.
- **Inference**: Log inputs/outputs with appropriate PII protections.
- **Archival**: Move aging data to cost-effective storage (S3 Glacier) with retention policies.
- **Deletion**: Securely delete data per retention schedules and right-to-erasure requests (GDPR).

**AWS tools**: S3 Lifecycle policies (automated tiering and deletion), AWS Backup, S3 Intelligent-Tiering.

---

### Logging
- **Comprehensive logging** is the foundation of AI governance — you cannot govern what you cannot see.
- **What to log in AI systems**:

| Log Type | What to Capture | AWS Service |
|---|---|---|
| **API activity logs** | All Bedrock/SageMaker API calls | AWS CloudTrail |
| **Model invocation logs** | Prompts, responses, model IDs, latency | Amazon Bedrock invocation logging → S3/CloudWatch |
| **Data access logs** | Who accessed which training data | S3 Server Access Logs, CloudTrail |
| **Application logs** | AI application errors, usage patterns | Amazon CloudWatch Logs |
| **Model monitoring logs** | Inference inputs/outputs for drift detection | SageMaker Model Monitor |
| **Security logs** | Threat detection findings, vulnerability scans | GuardDuty, Inspector, Security Hub |

**Bedrock model invocation logging:**
- Enable in Bedrock console to log all prompts and responses to S3 or CloudWatch.
- Critical for compliance auditing, debugging, and bias monitoring.
- Must balance logging detail with PII privacy protections.

---

### Data Residency
- **Definition**: Ensuring that data is **stored and processed within specific geographic boundaries** as required by regulations.
- **Why it matters**: GDPR (EU), data sovereignty laws, government/defense requirements.
- **AWS implementation**:
  - Data in an AWS region **stays in that region** unless explicitly transferred.
  - Choose Bedrock and SageMaker regions that align with data residency requirements.
  - Use **AWS Config rules** to detect data being replicated to non-compliant regions.
  - **AWS Control Tower data residency guardrails**: Prevent resource creation outside approved regions.
- **Cross-region inference tradeoff**: Bedrock's cross-region inference improves availability but may conflict with data residency requirements — understand and configure explicitly.

---

### Monitoring and Observation
- Continuously monitor AI system behavior to detect **quality degradation, bias drift, security threats, and compliance violations**.

**Monitoring layers for AI systems:**

| Layer | What to Monitor | AWS Tool |
|---|---|---|
| **Infrastructure** | CPU, GPU, memory, latency, errors | Amazon CloudWatch |
| **Model quality** | Accuracy, drift, bias metrics | SageMaker Model Monitor, Clarify |
| **Data quality** | Input distribution shifts, schema changes | SageMaker Data Quality Monitor |
| **Security** | Unauthorized access, anomalous API calls | GuardDuty, CloudTrail, Security Hub |
| **Cost** | Token usage, training job spend | AWS Cost Explorer, Budgets |
| **Application** | Error rates, response times, user feedback | CloudWatch, X-Ray |

**Observability vs. Monitoring:**
- **Monitoring**: Watching known metrics and alerting on threshold breaches.
- **Observability**: Deeper insight into system behavior — logs, metrics, and traces — enabling diagnosis of unknown failures.
- **AWS X-Ray**: Distributed tracing for AI application request flows.

---

### Data Retention
- **Definition**: Policies that define **how long data is kept** before being archived or deleted.
- **Why it matters for AI**:
  - Regulatory requirements mandate minimum retention (e.g., financial records 7 years).
  - GDPR right to erasure requires deletion of personal data on request.
  - Long retention of training data supports model auditing and reproducibility.
  - Excessive retention increases storage cost and privacy risk.

**Retention policy elements:**
- Minimum retention period (regulatory minimum).
- Maximum retention period (privacy/cost limitation).
- Archival policy (when to move to Glacier vs. active storage).
- Deletion procedure (secure erasure vs. standard delete).
- Legal hold: Suspend deletion when data is subject to litigation.

**AWS tools**: S3 Lifecycle policies, S3 Object Lock (WORM for legal hold), AWS Backup retention policies.

---

### Data Governance Strategy Summary

| Strategy | Key Action | AWS Tool |
|---|---|---|
| **Data lifecycle** | Automate transitions and deletion | S3 Lifecycle, AWS Backup |
| **Logging** | Capture all AI system activity | CloudTrail, Bedrock invocation logs, CloudWatch |
| **Data residency** | Restrict to compliant regions | Control Tower guardrails, Config rules |
| **Monitoring** | Detect drift, degradation, security threats | SageMaker Model Monitor, CloudWatch, GuardDuty |
| **Retention** | Define and enforce retention schedules | S3 Lifecycle, S3 Object Lock |

---

## 3. Processes to Follow Governance Protocols

### Policies
- **AI governance policies** define the rules and standards for how AI systems are developed, deployed, and monitored within an organization.
- **Types of AI governance policies**:
  - **Acceptable Use Policy**: What use cases AI can/cannot be applied to.
  - **Data Use Policy**: What data can be used for training and inference.
  - **Model Approval Policy**: What gates a model must pass before production deployment.
  - **Incident Response Policy**: How to respond to AI-related failures, harms, or breaches.
  - **Vendor/Third-Party Policy**: Requirements for external FM providers (data handling, compliance).
  - **Human Oversight Policy**: When human review is required for AI decisions.
- Policies should be **written, versioned, approved, and communicated** to all stakeholders.

---

### Review Cadence
- AI governance requires **regular structured reviews** — not just at deployment, but throughout the lifecycle.

**Recommended review schedule:**

| Review Type | Frequency | What to Review |
|---|---|---|
| **Model performance review** | Monthly / Quarterly | Accuracy, drift, bias metrics from Model Monitor |
| **Security review** | Quarterly | IAM permissions, vulnerability scan results, threat findings |
| **Compliance audit** | Annually (or per regulation cycle) | Audit Manager evidence, compliance posture |
| **Data quality review** | After each dataset update | Completeness, bias, PII exposure |
| **Incident post-mortem** | After each incident | Root cause, remediation, policy updates |
| **Model card update** | After each model version change | Reflect new training data, performance metrics, limitations |
| **Policy review** | Annually | Ensure policies reflect current regulations and business needs |

---

### Review Strategies

**Pre-deployment model review gates:**
```
[Development] → [Bias/Fairness Evaluation (Clarify)]
              → [Security Review (Inspector, IAM Audit)]
              → [Performance Benchmarking (Bedrock Model Evaluation)]
              → [Model Card Completion]
              → [Governance Approval]
              → [Production Deployment]
```

**Review approaches:**
- **Red team reviews**: Adversarial testing of model safety and robustness before deployment.
- **Peer review**: Independent review of model design, training data, and evaluation results.
- **Automated gate checks**: CI/CD pipeline checks that fail if bias metrics exceed thresholds.
- **Stakeholder review**: Business, legal, and compliance teams review high-risk AI deployments.
- **Third-party audit**: External auditors validate governance controls for regulated industries.

---

### Governance Frameworks

#### AWS Generative AI Security Scoping Matrix
- An AWS framework for **determining the appropriate security and compliance scope** for GenAI use cases based on where and how the AI operates.
- Helps organizations categorize their GenAI usage across a spectrum of risk and control.

**Scoping dimensions:**
- **Data sensitivity**: Public, internal, confidential, regulated (PII, PHI, financial).
- **Model location**: AWS-managed (Bedrock), self-hosted (SageMaker), third-party API.
- **Use case risk**: Low-risk (internal productivity) vs. high-risk (automated decisions affecting individuals).
- **User base**: Internal employees, business partners, general public.

**How it works:**
- Map each GenAI application to the matrix.
- The quadrant determines which security controls, compliance frameworks, and governance processes are required.
- Higher data sensitivity + higher risk = more stringent controls required.

**Example mappings:**

| Use Case | Data Sensitivity | Risk Level | Required Controls |
|---|---|---|---|
| Internal chatbot using public FAQs | Low | Low | Basic IAM, logging |
| Customer-facing support bot | Medium | Medium | Guardrails, PII protection, monitoring |
| Healthcare diagnostic AI using patient data | High | High | HIPAA controls, human oversight, full audit trail |
| Automated loan decision system | High | High | Fairness audits, explainability, regulatory compliance |

---

#### Other Governance Frameworks
- **NIST AI RMF (Risk Management Framework)**: A framework for identifying, assessing, and managing AI risks across four functions: Govern, Map, Measure, Manage.
- **EU AI Act**: EU regulation classifying AI systems by risk level (prohibited, high-risk, limited-risk, minimal-risk) and imposing requirements accordingly.
- **ISO/IEC 42001**: International standard for AI management systems.
- **OECD AI Principles**: International guidelines for responsible, trustworthy AI.

---

### Transparency Standards
- Organizations should be **open with stakeholders** about their AI systems' capabilities, limitations, and use.
- **Transparency practices**:
  - Disclose to users when they are interacting with an AI (not a human).
  - Publish Model Cards for deployed models.
  - Document training data sources and known limitations.
  - Provide explanations for consequential AI decisions.
  - Report on AI system performance and incidents periodically.
  - Make acceptable use policies and terms of AI service publicly accessible.
- **AWS transparency tools**: SageMaker Model Cards, Bedrock Model Cards (for AWS Titan models), AWS responsible AI documentation.

---

### Team Training Requirements
- Governance only works if **people understand and follow it**. Training is non-negotiable.

**AI governance training by role:**

| Role | Training Topics |
|---|---|
| **Developers / ML Engineers** | Secure coding for AI, prompt injection defense, data privacy, responsible AI practices |
| **Data Scientists** | Bias detection, fairness metrics, responsible data use, model documentation |
| **Product Managers** | AI ethics, acceptable use policies, regulatory requirements, risk assessment |
| **Security Teams** | AI-specific threat landscape, Bedrock/SageMaker security configurations |
| **Legal / Compliance** | AI regulations (EU AI Act, GDPR, sector-specific), IP considerations, liability |
| **Executives / Leadership** | AI governance strategy, risk tolerance, regulatory landscape, ethical principles |
| **All Staff** | AI acceptable use policy, data handling, reporting AI incidents |

**Training best practices:**
- **Role-based training**: Tailor content to job function — not everyone needs the same depth.
- **Regular cadence**: Annual refreshers + updates when regulations or policies change.
- **Scenario-based learning**: Use real-world examples of AI failures to make risks tangible.
- **Certification tracking**: Track completion and certifications in an LMS (Learning Management System).
- **Incident-driven updates**: Update training after AI incidents or near-misses.

---

## 4. Governance and Compliance Quick Reference

### Regulatory Landscape for AI

| Regulation | Scope | Key AI Requirements |
|---|---|---|
| **GDPR** (EU) | Personal data of EU residents | Right to explanation for automated decisions, data minimization, right to erasure |
| **EU AI Act** | AI systems in EU market | Risk classification, transparency, human oversight for high-risk AI |
| **HIPAA** (US) | Healthcare data | PHI protection, BAA required, audit logs |
| **CCPA** (California) | California consumer personal data | Right to know, delete, opt-out of AI-driven profiling |
| **SOC 2** | Service organizations | Trust service criteria: security, availability, confidentiality |
| **NIST AI RMF** | Voluntary US framework | Govern, Map, Measure, Manage AI risk |

---

### Governance Maturity Levels

```
Level 1: Ad Hoc
└── No formal policies; governance reactive to incidents

Level 2: Defined
└── Policies exist; applied inconsistently; manual processes

Level 3: Managed
└── Policies consistently applied; monitoring in place; regular reviews

Level 4: Optimized
└── Automated controls; continuous monitoring; governance drives decisions
    └── AWS tools enabling this level:
        Config (automated compliance) + Audit Manager (continuous evidence) +
        CloudTrail (full audit trail) + Model Monitor (continuous monitoring)
```

---

## 5. Exam Tips Recap

- ✅ **AWS Config** = continuous compliance monitoring; evaluates resources against rules; detects configuration drift.
- ✅ **Amazon Inspector** = automated vulnerability scanning for EC2, containers (SageMaker images), and Lambda.
- ✅ **AWS Audit Manager** = automated audit evidence collection mapped to compliance frameworks (HIPAA, SOC 2, GDPR).
- ✅ **AWS Artifact** = download AWS's compliance reports and sign agreements (HIPAA BAA). Not about your resources — about AWS's infrastructure.
- ✅ **AWS CloudTrail** = audit log of all API calls. Answer for "who did what, when" forensic questions.
- ✅ **Trusted Advisor** = best-practice recommendations across security, cost, performance, and limits. Advisory only.
- ✅ **Data residency** = keep data in specific regions. Control Tower guardrails + Config rules enforce this.
- ✅ **Generative AI Security Scoping Matrix** = AWS framework for determining required security controls based on data sensitivity and use case risk.
- ✅ **Logging** for AI: CloudTrail (API activity) + Bedrock invocation logs (prompts/responses) + SageMaker Model Monitor (inference data).
- ✅ **Governance requires policies + reviews + frameworks + transparency + training** — all five components are testable.
- ✅ Know the difference: **Artifact** (AWS's reports) vs. **Audit Manager** (your resources' evidence) vs. **Config** (your resources' compliance).
- ✅ **NIST AI RMF** = Govern, Map, Measure, Manage. **EU AI Act** = risk-based classification of AI systems.