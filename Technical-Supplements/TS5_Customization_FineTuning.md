# Technical Supplement 5 — Customization & Fine-Tuning Frameworks
### Version 1.1 — November 2025
---

**Purpose & Scope  **
This supplement provides a strategic overview and implementation
frameworks for customizing LMMs—from prompt-tuning to RAG and
fine-tuning. It focuses on governance-based methods for adapting models
to specialized domains without compromising accountability.

**Audience:** AI Engineers, System Architects, Managers  
**Prerequisites:** Understanding of prompting fundamentals (C.G.A.F.R.)
and organizational AI governance principles.  
**Outcome:** A decision framework for selecting customization strategies
and implementation checklists for deploying reliable RAG systems and
governed fine-tuning processes.

**Key Objectives:**

- Provide a strategic decision framework for selecting the right
  customization strategy (from prompting to fine-tuning).

- Deliver practical implementation checklists for deploying reliable RAG
  systems.

- Standardize governed fine-tuning processes to ensure reproducibility,
  auditability, and ethical compliance.

Developed by Russell Nida

© 2025 Russell Nida. Released under CC BY-NC-SA 4.0 for educational use.

# Contents

[1. Understanding the Spectrum of Customization
[1](#understanding-the-spectrum-of-customization)](#understanding-the-spectrum-of-customization)

[2. When to Customize vs. When to Re-Prompt
[2](#when-to-customize-vs.-when-to-re-prompt)](#when-to-customize-vs.-when-to-re-prompt)

[3. Retrieval-Augmented Generation (RAG)
[2](#retrieval-augmented-generation-rag)](#retrieval-augmented-generation-rag)

[4. Fine-Tuning and Domain Adaptation
[2](#fine-tuning-and-domain-adaptation)](#fine-tuning-and-domain-adaptation)

[5. Organizational Custom Instructions
[3](#organizational-custom-instructions)](#organizational-custom-instructions)

[6. Governance & Validation Framework
[4](#governance-validation-framework)](#governance-validation-framework)

[7. Key Takeaway [4](#key-takeaway)](#key-takeaway)

[8. Implementation Checklist for RAG Infrastructure
[4](#implementation-checklist-for-rag-infrastructure)](#implementation-checklist-for-rag-infrastructure)

[8.1 RAG Architecture Overview
[4](#rag-architecture-overview)](#rag-architecture-overview)

[8.2 Implementation Checklist
[5](#implementation-checklist)](#implementation-checklist)

[8.3 Maintenance and Drift Control
[5](#maintenance-and-drift-control)](#maintenance-and-drift-control)

[8.4 Key Takeaway [5](#key-takeaway-1)](#key-takeaway-1)

[9. Fine-Tuning Dataset Specification Template
[6](#fine-tuning-dataset-specification-template)](#fine-tuning-dataset-specification-template)

[9.1 Dataset Composition
[6](#dataset-composition)](#dataset-composition)

[9.2 Quality Standards Checklist
[6](#quality-standards-checklist)](#quality-standards-checklist)

[9.3 Training Metadata Record
[7](#training-metadata-record)](#training-metadata-record)

[9.4 Post-Training Validation
[7](#post-training-validation)](#post-training-validation)

[9.5 Key Takeaway [7](#key-takeaway-2)](#key-takeaway-2)

**Purpose**

Provide a decision framework for organizations that want to move beyond
ad-hoc prompting into system-level model customization. This supplement
focuses on when, why, and how to shape an LMM's behavior through
configuration, retrieval, or training—while maintaining accountability,
auditability, and compliance.

# 1. Understanding the Spectrum of Customization

Each level of customization adds capability, but also responsibility and
risk.

| **Level** | **Method** | **Description** | **Governance Considerations** |
|----|----|----|----|
| **Prompt Engineering** | Advanced prompt frameworks (e.g., C.G.A.F.R., Technical Supplement 1) | User-level control over context and structure. | Low risk; manual oversight. |
| **System Instruction Tuning** | Adjusting persistent "rules" (e.g., custom GPT instructions or templates). | Organizational alignment of tone, boundaries, compliance cues. | Medium risk; needs policy review. |
| **Retrieval-Augmented Generation (RAG)** | Supplying curated knowledge bases or document stores for context retrieval. | Enables domain-specific expertise without retraining the model. | High value; moderate risk; requires data governance. |
| **Fine-Tuning / Domain Adaptation** | Updating model weights with new labeled data. | Maximum alignment with organizational language or tasks. | High cost, high risk; requires ML governance and validation. |

**Key Principle:** Always start with prompting → configuration →
retrieval → training. Each layer adds power and responsibility.

# 2. When to Customize vs. When to Re-Prompt

Use this framework to decide whether the challenge is prompt design,
context, or model behavior.

- **Frequency:** Is the same instruction used repeatedly across teams?

- **Complexity:** Does it require multi-step reasoning or context
  recall?

- **Consistency:** Are outputs audited or regulatory?

- **Performance:** Is the baseline model demonstrably inadequate?

**Rule of Thumb:** If the problem is communication, improve prompting.
If the problem is context or domain knowledge, use RAG. If the problem
is model behavior, consider fine-tuning.

# 3. Retrieval-Augmented Generation (RAG)

Separate data from model memory. RAG allows the LMM to retrieve
authoritative information from a trusted corpus before answering.

1.  Curate a verified, versioned document repository.

2.  Embed and index content using a semantic vector store.

3.  Connect the index to the LMM through a retrieval pipeline.

4.  Log all queries and retrieved documents for auditability.

**Caution:** RAG systems inherit the trustworthiness of their sources.
Maintain data lineage and access control; treat each retrieval as
evidence, not authority.

# 4. Fine-Tuning and Domain Adaptation

Adapt a base model to specific organizational tone, terminology, or
decision logic. Fine-tuning should only be pursued when other strategies
fail.

**Pre-Tuning Checklist**

- Demonstrated need (prompting/RAG insufficient).

- Ethical and security review.

- High-quality labeled training data.

- Defined success metrics and validation set.

- Rollback and monitoring plan.

**Fine-Tuning Workflow**

1.  Prepare dataset (clean, diverse, representative).

2.  Train with incremental updates—monitor loss and overfitting.

3.  Validate against unseen data and human benchmarks.

4.  Deploy with staged rollout and human-in-the-loop review.

5.  Continuously log outputs for drift and bias detection.

**Caution:** Fine-tuned models can 'overfit' to your specific data,
becoming less capable of generalizing to novel situations and
potentially 'forgetting' useful knowledge from their base training. They
amplify both strengths and biases present in your dataset. Govern them
like software releases—versioned, tested, and reversible.

# 5. Organizational Custom Instructions

Codify institutional knowledge and ethical boundaries into the model's
persistent system message.

| **Instruction Area** | **Example Guidance** |
|----|----|
| **Tone & Style** | Use formal, evidence-based language suitable for government technical reports. |
| **Boundaries** | Never speculate on unverified operational data. |
| **Compliance** | Always flag potential export-control content. |
| **Auditability** | Tag every generated section with source and confidence score. |

**Manager's Mindset:** Treat these as your operating manual for the
model—enforceable, reviewable, and updateable.

# 6. Governance & Validation Framework

- **Version Control:** Tag every configuration, RAG corpus, and
  fine-tune with date and reviewer.

- **Testing:** Maintain regression tests for prompt stability and
  factual accuracy.

- **Monitoring:** Continuously evaluate outputs for drift, bias, and
  policy compliance.

- **Fallback Plan:** Maintain a "known-good" baseline model for
  comparison and rollback.

**Key Principle:** Customization without governance is not
optimization—it's liability.

**Note:** For definitions of terms like vector store and overfitting,
see Supplement B - Glossary.

# 7. Key Takeaway

The goal is not to make the model "yours," but to make it a more
reliable and accountable representative of your organization's values,
evidence, and judgment.

# 8. Implementation Checklist for RAG Infrastructure

**Purpose**

Provide a practical engineering framework for securely deploying and
maintaining a Retrieval-Augmented Generation (RAG) system within an
enterprise environment.

## 8.1 RAG Architecture Overview

A RAG pipeline connects: **Knowledge Source → Indexing Layer → Retrieval
Logic → Generation Layer**.

**Key Principle:** Separate data governance from reasoning logic. Treat
retrieval as a controlled data feed, not as model memory.

## 8.2 Implementation Checklist

| **Stage** | **Key Actions** | **Validation / Governance** |
|----|----|----|
| **1 - Preparation** | Identify authoritative sources; define data ownership; sanitize sensitive info. | Legal and data-classification review complete. |
| **2 - Indexing** | Generate embeddings with a vetted model; store in a secure vector database (e.g., FAISS, Pinecone). | Check reproducibility and version control for embeddings. |
| **3 - Retrieval** | Implement similarity search (top-k) with relevance threshold tuning. | Verify precision/recall using validation queries. |
| **4 - Integration** | Configure LMM prompt template to include retrieved context under a "Context:" header. | Confirm that retrieved snippets appear verbatim, not paraphrased. |
| **5 - Monitoring** | Log retrieval queries, document IDs, and timestamps. | Audit log reviewed monthly; drift or bias triggers re-indexing. |
| **6 - Security** | Restrict access to index API and storage; encrypt in transit and at rest. | Perform annual penetration and data-leak tests. |

## 8.3 Maintenance and Drift Control

- Re-embed content whenever source documents are updated.

- Maintain an **Embedding Version Registry** with model + date.

- Run quarterly validation to detect stale or irrelevant retrievals.

- Purge orphaned or deprecated vectors to reduce bias accumulation.

**Caution:** An outdated or poisoned index silently corrupts reasoning.
Treat the index like production data—versioned, monitored, and owned.

## 8.4 Key Takeaway

Reliable RAG systems depend more on data discipline than model
sophistication. Success = trustworthy data × transparent retrieval ×
audited generation.

# 9. Fine-Tuning Dataset Specification Template

**Purpose**

Standardize how fine-tuning datasets are built, documented, and
validated to ensure reproducibility and ethical compliance.

## 9.1 Dataset Composition

| **Field** | **Description** | **Example** |
|----|----|----|
| **Dataset ID** | Unique versioned identifier | FIN-2025-Q2-V1 |
| **Source** | Origin of data | Internal customer-service transcripts |
| **Purpose** | Target behavior or skill | Tone alignment for policy summaries |
| **Data Volume** | Number of records / tokens | 4k samples ≈ 2M tokens |
| **Data Split** | Train / Validation / Test | 80 / 10 / 10 |
| **Label Schema** | Category or score structure | Sentiment = {Positive, Neutral, Negative} |
| **Anonymization Method** | Removal or masking process | Regex + NER filtering |
| **Reviewer / Owner** | Data custodian name | Compliance - J.Doe |

## 9.2 Quality Standards Checklist

| **Criterion** | **Required Practice** | **Verification** |
|----|----|----|
| **Accuracy** | Double-annotate 10% of samples; resolve disagreements. | ≥ 95% inter-annotator agreement. |
| **Balance** | Check class distribution for bias. | No class \< 10%. |
| **Security** | Ensure PII removal and secure storage. | Data-loss-prevention scan. |
| **Ethical Review** | Confirm consent and use policy alignment. | IRB / Legal sign-off. |
| **Versioning** | Commit dataset metadata to version control. | Tag: dataset-FIN-2025-Q2-V1. |

## 9.3 Training Metadata Record

| **Field**               | **Example**           |
|-------------------------|-----------------------|
| **Base Model Version**  | GPT-5-Base-2025-03    |
| **Training Data ID**    | FIN-2025-Q2-V1        |
| **Training Parameters** | LR = 1e-5; Epochs = 3 |
| **Validation Accuracy** | 92.4%                 |
| **Reviewer**            | ML Lead - A.Smith     |
| **Deployment Tag**      | PROD-FIN-V1-2025-06   |

## 9.4 Post-Training Validation

- Compare fine-tuned vs. base model on held-out tasks.

- Conduct bias and robustness tests on unseen inputs.

- Document qualitative differences (style, tone, risk).

- Maintain a rollback option to prior model version.

**Caution:** A fine-tune without reproducibility and validation is a
liability, not an asset.

## 9.5 Key Takeaway

A fine-tuned model is only as ethical and reliable as its dataset. Treat
datasets as living compliance documents—versioned, reviewed, and
auditable.

**End of Technical Supplement 5**

**Cross-Reference:** For related security and threat-modeling
frameworks, see Technical Supplement 6 - Security & Governance.

**© 2025 Guide to Using Large Multimodal Models v1.1 - Authorized for
Educational & Non-Commercial Use (CC BY-NC-SA 4.0).**
