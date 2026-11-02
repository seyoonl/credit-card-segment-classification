# Credit Card Customer Segment Classification

*Supervised classification of customer segments using gradient-boosting models and a multi-stage pipeline.*

**Team project** · **LIKELION Data Analytics Bootcamp (Final Project)**

> This educational project used the dataset from DACON's **Credit Card Customer Segment Classification AI Competition**. The team developed and evaluated models independently as part of the bootcamp; **no submission was made to the official competition**.

## Overview

The project aimed to predict five predefined customer segments (A–E) from anonymized credit card customer data and to explore how customer attributes and spending behavior differ across segments.

A major challenge was the substantial class imbalance: **Segment E accounted for approximately 80%** of the data, while Segments A and B were extremely rare. We compared several classifiers, experimented with a multi-stage classification pipeline, and examined the trade-offs between overall performance and minority-class recognition.

## Dataset

The provided data included customer membership, credit, transaction, billing, balance, channel, marketing, and performance-related information.

- **Target:** customer segment (A, B, C, D, or E)
- **Main challenge:** severe class imbalance and high-dimensional tabular features
- **Source:** DACON competition dataset

The original competition data is not redistributed in this repository.

## Project Workflow

| Stage | Team work |
| --- | --- |
| Data exploration | Inspected target distribution and customer-level features |
| Preprocessing | Addressed missing values, constant features, and categorical variables |
| Feature selection | Explored correlation-based filtering and variance inflation factor (VIF) |
| Baseline models | Compared LightGBM, XGBoost, and CatBoost |
| Pipeline design | Experimented with two-stage and three-stage CatBoost-based classification |
| Optimization | Used Optuna for hyperparameter tuning and explored class weighting |
| Interpretation | Reviewed confusion matrices, feature importance, segment-level EDA, and possible marketing applications |

## Model Evaluation

The following results are **validation Micro F1 scores reported in the team presentation**, not official DACON leaderboard scores.

| Approach | Validation Micro F1 |
| --- | ---: |
| LightGBM | 0.8432 |
| XGBoost | 0.8700 |
| CatBoost | 0.8711 |
| Three-stage CatBoost pipeline + hyperparameter tuning | **0.8939** |
| Three-stage pipeline + tuning + class weighting | 0.8885 |

The weighted model slightly reduced Micro F1 compared with the tuned pipeline, but improved recognition of some minority segments. The team ultimately discussed this trade-off in terms of the potential importance of identifying less frequent customer groups.

**Interpretation note:** For a single-label multiclass problem, Micro F1 is equivalent to overall accuracy. Because Segment E dominates the dataset, Micro F1 alone is insufficient to assess minority-class performance; class-specific precision/recall and Macro F1 are important complementary measures.

## Key Takeaways

- Severe class imbalance made overall performance and minority-class recognition different objectives.
- Multi-stage classification and hyperparameter tuning provided opportunities to improve model performance, but introduced additional complexity and possible error propagation.
- Class weighting shifted the balance between different segments rather than improving every class simultaneously.
- Feature-level EDA suggested differences in customer tenure, card usage, and spending patterns, providing hypotheses for segment-specific marketing strategies.

The marketing suggestions are exploratory interpretations of the available features, **not verified descriptions of customers' income or creditworthiness**.

## Limitations

- Correlation- and VIF-based feature selection may have removed useful features for tree-based models.
- A hierarchical pipeline can propagate earlier classification errors to subsequent stages.
- Minority classes were extremely small, making robust evaluation especially important.
- The source code and complete experimental environment are not included at this stage, so the reported results are not independently reproducible from this repository alone.

## Project Materials

- [Final presentation (PDF)](docs/presentation.pdf)

## Code Availability

This repository currently documents the project methodology and results. The original working code is not published here. The project was completed collaboratively by a four-person team during the LIKELION Data Analytics Bootcamp.
