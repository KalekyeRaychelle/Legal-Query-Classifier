# Legal-Query-Classifier
This project implements a transformer-based legal text classification system using RoBERTa to map user legal queries to one of 19 Kenyan Acts. The model was developed as part of the early architecture design for Uhaki, an AI-powered legal chatbot.
Here’s a clean, professional README you can use for your repository:

---

# Uhaki Legal Act Classifier

## Overview

Uhaki Legal Act Classifier is a transformer-based legal text classification system designed to map user legal queries to one of 19 Kenyan Acts.

The model was developed as part of the early architectural design of Uhaki, an AI-powered legal assistant focused on providing structured legal guidance.

This system reduces the search space in legal question answering by first identifying the most relevant governing Act before downstream answer retrieval or generation.

---

## Problem Statement

Legal queries are often open-ended and unstructured. Before generating or retrieving a legal response, the system must determine which statutory Act governs the issue.

Given a user query:

> "My landlord has refused to refund my deposit after I moved out."

The model predicts the most relevant Act from a predefined set of 19 Kenyan Acts.

This classification step improves:

* Precision in legal information retrieval
* System modularity
* Downstream response quality

---

## Model Architecture

The classifier is built using a fine-tuned version of
RoBERTa, originally introduced by
Meta and accessed via
Hugging Face Transformers.

* Base model: roberta-base
* Task: Multi-class classification (19 classes)
* Loss Function: CrossEntropyLoss
* Optimizer: AdamW
* Evaluation Metrics: Accuracy, Precision, Recall, F1-score

---

## Dataset

The dataset consists of labeled legal queries mapped to their corresponding Kenyan Acts.

Each sample contains:

* Input: Legal question (natural language)
* Label: Act category (1 of 19)

Example format:

| Text                                           | Label                  |
| ---------------------------------------------- | ---------------------- |
| "What are my rights during arrest?"            | Criminal Procedure Act |
| "Can my employer terminate me without notice?" | Employment Act         |

Text preprocessing includes:

* Tokenization using RoBERTa tokenizer
* Attention masking
* Label encoding

---

## Training

Training pipeline includes:

* Dataset loading
* Tokenization
* Model initialization
* Training loop
* Validation evaluation
* Model checkpoint saving

---

## Inference

To run inference:

```
python src/inference.py --text "My landlord has refused to return my deposit."
```

Example output:

```
Predicted Act: Landlord and Tenant Act
Confidence: 0.91
```

---

## Results

The model achieves strong multi-class classification performance across 19 Acts.

Evaluation metrics include:

* Overall accuracy -86.7%
* Macro F1-score-86.8%
* Confusion matrix analysis -
  <img width="878" height="611" alt="image" src="https://github.com/user-attachments/assets/9186c93a-f8b0-4a3a-9a4a-19777622bd1b" />

* Per-class performance breakdown

---

## Design Rationale

This classifier was designed as a modular component within a larger legal AI system.

Instead of directly generating answers, the architecture:

1. Classifies the query into a governing Act.
2. Narrows the retrieval scope.
3. Enables structured legal reasoning.

This modular design improves interpretability, maintainability, and scalability.

---

## Future Improvements

* Hierarchical legal classification
* Multi-label classification for overlapping legal domains
* Domain-adaptive pretraining on Kenyan legal corpora
* Integration with retrieval-based or RAG systems
* API deployment using FastAPI or Flask

