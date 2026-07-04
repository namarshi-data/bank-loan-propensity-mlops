# Model Card: Banking Loan Propensity Analytics

## Model Overview

This model predicts the probability that a retail banking customer will accept a personal loan offer. It is designed as a **campaign prioritization and analytical decision-support model**, not as an automated credit approval, decline, pricing, or eligibility model.

| Item | Description |
|---|---|
| Project | Banking Loan Propensity Analytics & MLOps Deployment |
| Business use case | Personal loan campaign prioritization |
| Model type | Binary classification |
| Target variable | `LoanOnCard` |
| Champion model | Gradient Boosting classifier |
| Classification threshold | 0.49 |
| Primary users | Banking analytics, marketing analytics, campaign strategy, data science teams |
| Intended output | Loan acceptance probability and high/low propensity label |

---

## Intended Use

The model is intended to support marketing and analytics teams by ranking customers based on estimated likelihood of accepting a personal loan offer. The output can help prioritize outreach for customers with higher predicted propensity.

Appropriate uses:

- Campaign targeting and prioritization
- Customer-level propensity scoring
- Marketing list segmentation
- Sales outreach planning
- Analytical comparison of customer segments
- Portfolio-level campaign planning

---

## Out-of-Scope Use

This model should **not** be used as-is for real banking production decisions.

It is not intended for:

- Automated loan approval or decline
- Credit eligibility decisions
- Pricing, limit setting, or underwriting decisions
- Customer-facing explanations
- Regulatory reporting
- Production use without independent validation and approval

---

## Dataset Summary

| Item | Value |
|---|---:|
| Initial records | 5,000 |
| Final cleaned records | 4,980 |
| Holdout actual loan customers | 96 |
| Problem type | Binary classification |
| Business use case | Personal loan propensity prediction |

Raw data, processed datasets, and model artifacts are intentionally excluded from version control.

---

## Model Performance Summary

| Metric | Holdout Result |
|---|---:|
| ROC-AUC | 99.91% |
| Precision | 94.95% |
| Recall | 97.92% |
| F1 Score | 96.41% |
| True Positives | 94 |
| False Positives | 5 |
| False Negatives | 2 |
| Actual Positives | 96 |

### Business Interpretation

The model identified **94 of 96 actual loan customers** in the holdout set. It missed **2 actual loan customers** and incorrectly targeted **5 non-loan customers**.

For a loan marketing campaign, this trade-off supports targeted outreach while limiting unnecessary customer contact.

---

## Threshold Strategy

The champion model uses a tuned threshold of **0.49** instead of relying only on the default 0.50 threshold.

The threshold was selected to balance:

- Capturing likely loan customers
- Reducing missed conversion opportunities
- Controlling unnecessary campaign outreach
- Supporting practical campaign execution

---

## Key Model Drivers

The strongest model drivers were related to customer value, spending behaviour, internal scoring, and existing banking relationships.

| Rank | Feature |
|---:|---|
| 1 | HighestSpend |
| 2 | Level |
| 3 | HiddenScore |
| 4 | MonthlyAverageSpend |
| 5 | FixedDepositAccount |

### Governance Note on `HiddenScore`

`HiddenScore` is treated as an internal customer scoring attribute available before campaign decisioning. In a real banking environment, this field would require lineage review to confirm that it does not leak the target outcome or encode restricted/proxy information.

---

## Validation and Governance Considerations

Because this is a banking analytics use case, the model should be evaluated beyond accuracy alone.

Key validation considerations:

- Precision, recall, F1, and ROC-AUC review
- Confusion matrix interpretation
- False positive and false negative business impact
- Class imbalance awareness
- Threshold tuning documentation
- Feature importance interpretation
- Reproducible train-test workflow
- API prediction contract validation

---

## Model Risk Notes

The high ROC-AUC reflects this portfolio dataset and holdout split. Before real banking use, the model would require additional controls and independent review.

Required production controls would include:

- Leakage review
- Out-of-time validation
- Fairness and bias testing
- Privacy and consent review
- Data quality monitoring
- Model drift monitoring
- Periodic recalibration or retraining
- Business owner sign-off
- Model risk approval

---

## Monitoring Recommendations

If implemented in a real banking environment, the model should be monitored for:

| Monitoring Area | Example Checks |
|---|---|
| Data quality | Missing fields, invalid values, schema changes |
| Score stability | Shift in predicted probability distribution |
| Model drift | Feature distribution changes over time |
| Business performance | Campaign response rate by score band |
| Threshold performance | Precision, recall, false positives, false negatives |
| Fairness | Segment-level outcome and error-rate review |
| Operational use | Review of how scores are used by business teams |

---

## Responsible Use Statement

This project is a portfolio demonstration of a banking analytics and MLOps workflow. It is intended to show technical, analytical, and governance awareness. It does not represent an approved production banking model and should not be used for real customer decisioning without formal validation, controls, and approval.
