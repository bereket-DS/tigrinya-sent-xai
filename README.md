# TigrinyaSent-XAI

**Interpretable Sentiment Analysis for Tigrinya Social Media Text**

TigrinyaSent-XAI is a research project for developing and evaluating **interpretable sentiment analysis models for Tigrinya text**.

The project focuses not only on predicting whether a Tigrinya text is positive or negative, but also on explaining **why** a model makes a particular prediction. The goal is to investigate transformer-based sentiment classification together with token-level attribution, feature importance, and counterfactual explanations.

---

## Research Motivation

Tigrinya is a relatively low-resource language in Natural Language Processing (NLP). Compared with high-resource languages such as English, there are fewer publicly available datasets, pretrained models, linguistic resources, and evaluation tools.

Sentiment analysis for Tigrinya is particularly challenging because real-world social media text can contain:

* Spelling variations
* Informal language
* Long and noisy sentences
* Code-switching
* Sarcasm and irony
* Strong emotional expressions
* Political and social discussions
* Morphological variation
* Repeated characters and punctuation
* Informal abbreviations and social-media conventions

A classification model may achieve good accuracy while still being difficult to understand. Therefore, this project investigates **interpretable sentiment analysis**, where model predictions are accompanied by explanations identifying the words or phrases that contributed to the prediction.

---

## Project Objectives

The main objectives are:

1. Develop a baseline sentiment classification model for Tigrinya.
2. Fine-tune a transformer-based model for Tigrinya sentiment classification.
3. Compare traditional machine-learning and transformer-based approaches.
4. Generate human-readable explanations for model predictions.
5. Identify important words and phrases contributing to sentiment predictions.
6. Investigate counterfactual explanations.
7. Perform detailed error analysis on difficult Tigrinya texts.
8. Evaluate the faithfulness and stability of generated explanations.

---

## Dataset

The dataset contains two columns:

| Column     | Description                         |
| ---------- | ----------------------------------- |
| `sentence` | Tigrinya text                       |
| `label`    | Binary sentiment label (`0` or `1`) |

Example:

```text
sentence,label
"..." ,0
"..." ,1
```

The exact meaning of `0` and `1` will be verified during the dataset exploration stage rather than assumed beforehand.

### Important

The original dataset will be preserved in its original form.

```text
data/
└── raw/
    └── tigrinya_sentiment.csv
```

Processed datasets will be stored separately.

---

## Methodology

The project will follow several stages.

### 1. Dataset Exploration

The first stage will examine:

* Dataset size
* Missing values
* Duplicate sentences
* Label distribution
* Sentence length
* Character and token statistics
* Class imbalance
* Spelling variation
* Noisy text
* Long social-media comments
* Difficult and ambiguous examples

### 2. Data Preprocessing

Depending on the characteristics of the dataset, preprocessing may include:

* Removing unwanted artifacts
* Normalizing whitespace
* Handling duplicated samples
* Handling URLs and mentions
* Handling excessive punctuation
* Preserving meaningful Tigrinya characters
* Tokenization

Preprocessing will be carefully evaluated because aggressive normalization can remove information important for sentiment classification.

### 3. Baseline Model

A traditional machine-learning baseline will be developed using:

```text
TF-IDF
   ↓
Logistic Regression
   ↓
Sentiment Prediction
```

The baseline provides a useful reference point and has an additional advantage: its feature weights can provide a relatively simple form of interpretability.

### 4. Transformer Model

A Tigrinya-capable transformer model will be investigated for the main classification system.

Potential models include:

* TiRoBERTa
* XLM-RoBERTa
* Other Tigrinya-capable pretrained language models

The final model selection will be based on experimental evaluation rather than assuming that one model is automatically superior.

The general architecture is:

```text
Tigrinya Text
      ↓
Tokenizer
      ↓
Transformer Encoder
      ↓
Classification Head
      ↓
Positive / Negative
```

---

# Explainability

Interpretability is a central component of this project.

The project will investigate several explanation methods.

## SHAP

SHAP will be investigated to estimate the contribution of input features to a prediction.

Example conceptual output:

```text
Prediction: Negative

ተጸሊኡ      █████████
ኣይፈትዎን   ███████
ጽቡቕ        ░░░
```

The actual visualization and methodology will depend on the selected model.

## LIME

LIME will be investigated as a local explanation method that approximates the model's behavior around an individual prediction.

## Integrated Gradients

Integrated Gradients will be investigated for transformer-based models to estimate token-level contribution.

## Token-Level Attribution

For each sentence, the system will aim to identify tokens or phrases that strongly influence the predicted sentiment.

Example:

```text
Input:
"... Tigrinya sentence ..."

Prediction:
Negative

Important tokens:
[important token 1]
[important token 2]
[important token 3]
```

---

# Counterfactual Explanations

The project will also investigate counterfactual explanations.

A counterfactual explanation asks:

> What minimal change to the input could cause the model to change its prediction?

Conceptually:

```text
Original sentence
       ↓
Prediction: Negative
       ↓
Modify sentiment-bearing phrase
       ↓
Counterfactual sentence
       ↓
Prediction: Positive
```

This can provide a more intuitive explanation of model behavior than feature importance alone.

---

# Explanation Evaluation

Explanations will not be evaluated only by visual inspection.

Possible evaluation dimensions include:

### Faithfulness

Does the explanation accurately represent the behavior of the model?

### Comprehensiveness

Does removing important tokens significantly affect the prediction?

### Sufficiency

Can the identified important tokens preserve the model's prediction?

### Stability

Does the explanation remain reasonably consistent when the input is slightly modified?

### Sparsity

Can the model explain a prediction using a small and meaningful subset of the input?

These metrics will be selected and implemented as the research progresses.

---

# Evaluation Metrics

The classification models will be evaluated using:

* Accuracy
* Precision
* Recall
* F1-score
* Macro F1
* Confusion matrix

For potentially imbalanced data, **Macro F1** will receive particular attention.

Additional metrics may be introduced depending on the final experimental design.

---

# Error Analysis

A detailed error analysis will be performed to understand where the models fail.

Examples of areas of interest include:

* Sarcasm
* Irony
* Negation
* Mixed sentiment
* Long sentences
* Informal language
* Morphological variation
* Spelling variation
* Ambiguous expressions
* Social and political language
* Out-of-domain text

The goal is not only to report model performance but also to understand **why the model succeeds or fails**.

---

# Project Structure

```text
tigrinya-sent-xai/
│
├── README.md
├── LICENSE
├── .gitignore
├── requirements.txt
├── pyproject.toml
│
├── configs/
│   ├── baseline.yaml
│   └── transformer.yaml
│
├── data/
│   ├── raw/
│   │   └── tigrinya_sentiment.csv
│   ├── processed/
│   │   ├── train.csv
│   │   ├── validation.csv
│   │   └── test.csv
│   └── README.md
│
├── notebooks/
│   ├── 01_dataset_exploration.ipynb
│   ├── 02_baseline_tfidf.ipynb
│   ├── 03_transformer_training.ipynb
│   ├── 04_model_evaluation.ipynb
│   └── 05_interpretability_analysis.ipynb
│
├── src/
│   ├── data/
│   ├── models/
│   ├── training/
│   ├── evaluation/
│   ├── explainability/
│   ├── counterfactual/
│   └── utils/
│
├── models/
│   ├── baseline/
│   └── transformer/
│
├── explanations/
│   ├── shap/
│   ├── lime/
│   ├── integrated_gradients/
│   └── counterfactuals/
│
├── results/
│   ├── metrics/
│   ├── predictions/
│   ├── error_analysis/
│   └── figures/
│
└── tests/
```

---

# Environment Setup

This project uses a Python virtual environment.

Create the environment:

```bash
python3 -m venv .venv
```

Activate it:

```bash
source .venv/bin/activate
```

Verify Python:

```bash
python --version
```

Upgrade pip:

```bash
python -m pip install --upgrade pip
```

Install project dependencies:

```bash
pip install -r requirements.txt
```

---

# Reproducibility

Experiments should be reproducible whenever possible.

The project will use:

* Fixed random seeds
* Version-controlled source code
* Versioned datasets
* Recorded model configurations
* Logged evaluation metrics
* Saved experiment results

Git will be used for source-code version control.

DVC may be used for dataset and model versioning.

MLflow may be used for experiment tracking and model management.

---

# Experiment Management

The planned workflow is:

```text
                    GitHub
                      │
                Source Code
                      │
                      ▼
Local Development ── Git
      │
      ├── Dataset ──────── DVC
      │
      ├── Experiments ──── MLflow
      │
      └── Models ───────── MLflow / DVC
                      │
                      ▼
                   DagsHub
```

The exact experiment-tracking workflow will be introduced after the initial model pipeline is working.

---

# Development Roadmap

## Phase 1 — Project Setup

* [x] Create project repository
* [ ] Create Python virtual environment
* [ ] Install dependencies
* [ ] Configure Git
* [ ] Add dataset
* [ ] Create initial project structure

## Phase 2 — Dataset Analysis

* [ ] Load dataset
* [ ] Verify columns
* [ ] Verify label mapping
* [ ] Check missing values
* [ ] Check duplicates
* [ ] Analyze class distribution
* [ ] Analyze sentence lengths
* [ ] Investigate linguistic and social-media noise

## Phase 3 — Baseline

* [ ] TF-IDF features
* [ ] Logistic Regression
* [ ] Train/validation/test split
* [ ] Evaluation
* [ ] Confusion matrix
* [ ] Baseline error analysis

## Phase 4 — Transformer

* [ ] Select pretrained model
* [ ] Prepare tokenizer
* [ ] Fine-tune model
* [ ] Evaluate model
* [ ] Compare against baseline

## Phase 5 — Explainability

* [ ] SHAP
* [ ] LIME
* [ ] Integrated Gradients
* [ ] Token attribution
* [ ] Explanation visualization

## Phase 6 — Counterfactuals

* [ ] Develop counterfactual generation
* [ ] Evaluate prediction changes
* [ ] Analyze minimal modifications

## Phase 7 — Research Evaluation

* [ ] Faithfulness evaluation
* [ ] Sufficiency evaluation
* [ ] Comprehensiveness evaluation
* [ ] Stability evaluation
* [ ] Explanation error analysis

## Phase 8 — MLOps

* [ ] DVC
* [ ] MLflow
* [ ] DagsHub
* [ ] Docker
* [ ] CI/CD
* [ ] Model serving API

---

# Research Questions

The project may investigate the following research questions:

### RQ1

How effectively can transformer-based models perform binary sentiment classification for Tigrinya social media text?

### RQ2

How do transformer-based models compare with traditional TF-IDF-based approaches for Tigrinya sentiment classification?

### RQ3

Which explanation methods provide the most faithful and stable explanations for Tigrinya sentiment predictions?

### RQ4

Can token-level and phrase-level explanations identify meaningful sentiment-bearing expressions in Tigrinya?

### RQ5

Can counterfactual explanations provide useful and interpretable evidence for sentiment predictions?

### RQ6

What linguistic and social-media phenomena are responsible for model errors?

---

# Current Status

**Project stage: Initial setup**

The project is currently focused on establishing the dataset, development environment, baseline pipeline, and reproducible research workflow.

Model performance and explanation results will be added after experiments are completed.

---

# License

This project is intended for research and educational purposes.

The license and dataset usage conditions will be specified according to the licensing terms of the source dataset.

---

# Author

**Bereket Weldemichael**

Tigrinya NLP / Machine Learning Research Project
