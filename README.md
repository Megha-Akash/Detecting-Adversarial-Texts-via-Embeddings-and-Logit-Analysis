# Detecting Adversarial Texts via Embeddings and Logit Analysis

A Trustworthy Machine Learning project exploring the detection of adversarial attacks in large language models by analyzing embedding-space similarity and shifts in logit distribution. This method aims to identify subtle perturbations introduced by attacks like TextFooler that fool models while preserving text fluency.

---

## Table of Contents

- [Overview](#overview)
- [Related Work](#related-work)
- [Proposed Method](#proposed-method)
- [Experimental Setup](#experimental-setup)
- [Results](#results)


---

## Overview

Adversarial attacks pose a critical threat to the robustness of NLP systems. This project presents an adversarial detection approach using token-level embedding similarity and logit difference analysis. It evaluates detection effectiveness against the TextFooler attack using a fine-tuned DistilBERT model on the SST-2 sentiment dataset.

---

## Related Work

- **TextFooler** – Replaces important words with synonyms to mislead model predictions while maintaining semantic similarity (Jin et al., 2019).


---

## Proposed Method

1. **Adversarial Data Generation**  
   - Use TextFooler to generate adversarial examples from the SST-2 dataset.
   - Equal split of clean and perturbed texts for balanced training.

2. **Model Training**  
   - Fine-tune DistilBERT on combined dataset.
   - Train for 3 epochs with batch size 8 and learning rate 2e-5.

3. **Adversarial Detection**  
   - **Logit Difference**: Compare logits of clean vs perturbed versions.
   - **Embedding Similarity**: Use cosine similarity on token embeddings.

4. **Hyperparameter Tuning**  
   - Grid search for optimal logit thresholds (0.1–0.5) and embedding similarity thresholds (0.7–0.9).
   - Evaluate with Accuracy, F1-Score, AUC, and ASR.

---

## Experimental Setup

- **Dataset**: SST-2 from HuggingFace `datasets` library
- **Attack**: TextFooler from TextAttack library
- **Model**: DistilBERT
- **Training**:
  - Tokenization and padding to 512 tokens
  - Trainer API for model fine-tuning

- **Evaluation Metrics**:
  - Accuracy
  - F1-Score (0.6960)
  - AUC (0.5030)
  - ASR (61.27%)

---

## Results

| Detection Method                | Logit Threshold | Embed Threshold | Accuracy | F1-Score | AUC    | ASR (%) |
|--------------------------------|------------------|------------------|----------|----------|--------|---------|
| Embedding & Logit Analysis     | 0.1              | 0.7              | 0.548    | 0.6960   | 0.5030 | 61.27   |

- Moderate success in detecting adversarial inputs.
- High ASR indicates adversarial examples still evade detection.
- Embedding similarity and logit shifts alone may not be sufficient for robust detection.

---
