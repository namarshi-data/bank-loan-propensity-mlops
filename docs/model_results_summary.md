# Model Results Summary

## Project Context

This project predicts which retail banking customers are most likely to accept a personal loan offer. The goal is to support targeted campaign planning by ranking customers according to estimated loan acceptance probability.

The model is framed as a **marketing and campaign prioritization solution**, not as a credit decisioning model.

---

## Dataset Overview

| Item | Value |
|---|---:|
| Initial records | 5,000 |
| Final cleaned records | 4,980 |
| Holdout actual loan customers | 96 |
| Target variable | `LoanOnCard` |
| Problem type | Binary classification |
| Business use case | Personal loan propensity prediction |

---

## Model Development Summary

The modelling process compared several baseline and candidate models, including:

- Dummy Classifier
- Logistic Regression
- Weighted Logistic Regression
- Naive Bayes
- Support Vector Machine
- Decision Tree
- Random Forest
- Gradient Boosting
- Resampling-based experiments

The champion model was selected using both statistical performance and business interpretation.

---

## Champion Model

| Item | Value |
|---|---|
| Champion model | Gradient Boosting classifier |
| Selected threshold | 0.49 |
| Selection logic | Balance likely-customer capture with campaign efficiency |

---

## Holdout Performance

| Metric | Result |
|---|---:|
| ROC-AUC | 99.91% |
| Precision | 94.95% |
| Recall | 97.92% |
| F1 Score | 96.41% |
| True Positives | 94 |
| False Positives | 5 |
| False Negatives | 2 |
| Actual Positives | 96 |

---

## Confusion Matrix Interpretation

| Error Type | Meaning | Business Impact |
|---|---|---|
| True Positive | Customer predicted as high-propensity and accepted the loan | Correctly prioritized campaign opportunity |
| False Positive | Customer predicted as high-propensity but did not accept the loan | Extra campaign outreach cost |
| False Negative | Customer predicted as low-propensity but accepted the loan | Missed conversion opportunity |
| True Negative | Customer predicted as low-propensity and did not accept the loan | Correctly avoided unnecessary outreach |

The model correctly identified **94 of 96 actual loan customers** and missed only **2**. It incorrectly targeted **5 non-loan customers**.

---

## Business Interpretation

For a personal loan marketing campaign, recall and precision should be interpreted through a business lens.

- High recall helps reduce missed revenue opportunities.
- Strong precision helps avoid overloading campaign teams with low-propensity customers.
- False positives represent additional outreach cost.
- False negatives represent customers who may have accepted an offer but were not prioritized.

The selected model supports a targeted outreach strategy by prioritizing customers with stronger loan acceptance probability while keeping unnecessary contact volume low.

---

## Feature Importance Summary

The strongest model drivers were related to customer value, banking relationship strength, internal scoring, and spending behaviour.

| Rank | Feature | Business Interpretation |
|---:|---|---|
| 1 | HighestSpend | Higher transaction value may indicate stronger borrowing potential |
| 2 | Level | Relationship tier or customer segment may indicate product fit |
| 3 | HiddenScore | Internal score may capture customer quality or engagement signals |
| 4 | MonthlyAverageSpend | Spending behaviour may indicate financial activity and product need |
| 5 | FixedDepositAccount | Existing banking relationship may indicate product cross-sell opportunity |

### Governance Note

Feature importance should be used for model understanding, not as automatic customer-facing explanation. In production, features such as `HiddenScore` would require lineage and leakage review.

---

## Why Threshold Tuning Matters

The default threshold is not always the best business threshold. In this project, the threshold was tuned to improve the balance between:

- Capturing likely loan customers
- Reducing unnecessary outreach
- Supporting a campaign strategy that can be implemented by business teams

A banking analytics project should connect model metrics to operational decisions rather than reporting accuracy alone.

---

## Model Risk and Limitations

The high ROC-AUC should be interpreted carefully. It reflects this portfolio dataset and holdout split, not guaranteed real-world production performance.

Before real banking use, the model would require:

- Leakage review
- Out-of-time validation
- Fairness and bias testing
- Privacy and consent review
- Data quality monitoring
- Model drift monitoring
- Independent validation
- Business owner approval
- Model risk governance sign-off

---

## Summary

The Gradient Boosting champion model achieved strong holdout performance and translated model output into a practical campaign prioritization workflow. The project demonstrates data cleaning, feature engineering, model comparison, threshold tuning, business error interpretation, and governance awareness for a retail banking analytics use case.
