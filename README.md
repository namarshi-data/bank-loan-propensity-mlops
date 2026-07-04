# Banking Loan Propensity Analytics & MLOps Deployment

End-to-end banking analytics project using machine learning to identify high-propensity personal loan customers, explain model results, and package the solution with API and MLOps-ready deployment templates.

## Recruiter Summary

This project demonstrates how predictive analytics can support personal loan campaign planning in a retail banking environment.

| Area | Evidence |
|---|---|
| Business problem | Prioritize customers most likely to accept a personal loan offer |
| Analytics task | Binary classification and customer propensity scoring |
| Champion model | Gradient Boosting classifier |
| Threshold strategy | Tuned threshold of 0.49 to balance recall and campaign efficiency |
| Holdout result | 94 of 96 actual loan customers identified |
| Business trade-off | 5 false positives and 2 false negatives |
| Deployment readiness | Flask API, Docker, Kubernetes templates, Terraform template, CI workflow |
| Governance awareness | Leakage review, fairness testing, drift monitoring, privacy review, and production sign-off noted |

The project is designed for banking analytics, finance data analyst, machine learning analyst, and data science-adjacent roles where candidates are expected to connect modelling results to business decisions.

---

## Business Problem

Retail banks need to prioritize customers who are most likely to respond to loan campaigns. Broad campaigns can increase marketing costs, reduce customer experience, and waste sales capacity by targeting customers with low likelihood of conversion.

This project answers:

* Which customers are most likely to accept a personal loan offer?
* Which customer attributes are most associated with loan propensity?
* Which model provides the best balance between customer capture and campaign efficiency?
* How can the model be packaged for repeatable API-based scoring?

---

## Key Results

The final champion model is a Gradient Boosting classifier with a tuned classification threshold. It was selected because it provided the strongest balance between identifying likely loan customers and controlling unnecessary campaign outreach.

| Metric          | Result |
| --------------- | -----: |
| ROC-AUC         | 99.91% |
| Precision       | 94.95% |
| Recall          | 97.92% |
| F1 Score        | 96.41% |
| False Positives |      5 |
| False Negatives |      2 |

> **Model risk note:** The high ROC-AUC reflects this portfolio dataset and holdout split. Before any real banking use, the model would require leakage review, out-of-time validation, fairness testing, drift monitoring, privacy review, and model-risk approval.

### Business Interpretation

In the holdout set, the model correctly identified **94 of 96 actual loan customers** and missed only **2**. It incorrectly targeted **5 non-loan customers**.

From a banking campaign perspective, this model supports targeted outreach by helping marketing teams prioritize customers with stronger loan acceptance probability while keeping unnecessary contact volume low.

---

## Business Value

Retail banks often run personal loan campaigns across large customer bases. A broad campaign may waste marketing spend, overload sales teams, and create poor customer experience by contacting customers with low likelihood of conversion.

This model supports a more targeted campaign strategy by ranking customers based on estimated loan acceptance probability.

Potential business benefits:

- Prioritize high-propensity customers for outreach
- Reduce unnecessary customer contact
- Improve sales team focus
- Support campaign segmentation
- Connect model metrics to campaign cost and missed opportunity
- Provide repeatable API-based scoring for future campaign files

---

## Project Workflow

```text
Raw customer data
        ↓
Data cleaning and preprocessing
        ↓
EDA and statistical analysis
        ↓
Feature engineering
        ↓
Train-test split
        ↓
Model training and evaluation
        ↓
Threshold tuning
        ↓
Champion model selection
        ↓
Model governance review
        ↓
Flask prediction API
        ↓
Docker / Kubernetes / Terraform templates
        ↓
CI validation with GitHub Actions
```

---

## Visual Outputs

### Project Workflow

![Project Workflow](screenshots/project_workflow.png)

### Architecture

![Architecture](screenshots/architecture.png)

### Model Comparison

![Model Comparison](screenshots/model_comparison.png)

### Feature Importance

![Feature Importance](screenshots/feature_importance.png)

---

## Model Deployment Summary

The trained Gradient Boosting model is packaged for repeatable customer-level scoring through a lightweight Flask API. The deployment layer is designed to show how the model could be used by a banking analytics or marketing team to score new customer records and return a loan-propensity prediction.

The deployment setup includes:

| Component | Purpose |
|---|---|
| Flask API | Serves the trained model through a `/predict` endpoint |
| Sample request file | Provides an example customer-scoring payload |
| Dockerfile | Packages the API and dependencies into a container |
| Kubernetes manifests | Provides deployment and service templates for container orchestration |
| Terraform template | Provides an AWS ECR repository template for container image publishing |
| GitHub Actions CI | Validates Python files, runs tests, and checks Docker build readiness |

This repository is **structured for local and containerized deployment readiness**. It includes infrastructure templates for Docker, Kubernetes, Terraform, and CI validation, but it does **not** claim a live AWS, EKS, or Kubernetes production deployment.

---

## How to Run Locally

### 1. Create and activate environment

```bash
python -m venv .venv
```

Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

macOS/Linux:

```bash
source .venv/bin/activate
```

### 2. Install dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 3. Add raw data locally

Place the raw files here:

```text
data/raw/Data1.csv
data/raw/Data2.csv
```

Raw data is intentionally excluded from GitHub.

### 4. Run the full pipeline

```bash
python scripts/run_pipeline.py
```

### 5. Run the Flask API

```bash
python flask_app/app.py
```

Send a test prediction request:

```bash
curl -X POST http://localhost:5000/predict \
  -H "Content-Type: application/json" \
  -d @flask_app/sample_request.json
```

### 6. Optional: Run with Docker

```bash
docker build -f docker/Dockerfile -t bank-loan-propensity-api:latest .
docker run -p 5000:5000 bank-loan-propensity-api:latest
```

Detailed Kubernetes, Terraform, and CI instructions are available in `docs/deployment_guide.md`.

---

## Detailed Documentation

Additional technical documentation is available in the `docs/` folder:

- `docs/model_card.md`
- `docs/model_results_summary.md`
- `docs/deployment_guide.md`
- `docs/recruiter_review_notes.md`

---

## Tools & Skills Demonstrated

| Area | Tools / Methods | Skills Demonstrated |
|---|---|---|
| Data analysis | Python, Pandas, NumPy, SciPy | Data cleaning, preprocessing, EDA, statistical review, feature analysis |
| Machine learning | Scikit-Learn, Imbalanced-Learn, Gradient Boosting | Classification modelling, class imbalance handling, threshold tuning, model comparison |
| Model evaluation | Precision, recall, F1, ROC-AUC, confusion matrix | Business-focused model evaluation, false positive / false negative interpretation |
| Banking analytics | Loan propensity scoring, customer segmentation, campaign targeting | Marketing prioritization, customer-level analysis, campaign efficiency analysis |
| Model governance | Leakage review, fairness considerations, drift monitoring notes | Responsible model use, risk awareness, production-readiness thinking |
| API development | Flask, REST API, Joblib | Model serving, customer-level prediction endpoint, API contract testing |
| MLOps readiness | Docker, Kubernetes templates, Terraform template, GitHub Actions CI | Containerization, deployment templates, automated validation, repeatable pipeline execution |

---

## Target Roles This Project Supports

| Target Role | Why This Project Fits |
|---|---|
| Financial Data Analyst | Banking use case, customer-level analysis, business interpretation, campaign KPI thinking |
| Banking Analytics Analyst | Loan propensity modelling, segmentation, customer targeting, threshold strategy |
| Data Analyst | Data cleaning, EDA, statistical analysis, visualization, business insights |
| Machine Learning Analyst | Classification modelling, model comparison, threshold tuning, feature importance |
| Junior Data Scientist | End-to-end supervised learning workflow with business evaluation |
| Analytics Engineer / MLOps Analyst | Reusable pipeline, API, Docker, CI, deployment templates |

---

## Future Enhancements

- Add SQL-based data extraction and analytics layer
- Add Power BI dashboard for campaign monitoring
- Add MLflow experiment tracking and model registry workflow
- Add fairness, bias, and drift monitoring
- Add batch scoring for customer campaign files

---

## Important Notes

This project is a portfolio demonstration. It shows a professional end-to-end machine learning workflow and deployment-ready structure, but it does not represent an approved production banking model.

The repository intentionally excludes raw data, processed datasets, model artifacts, cloud credentials, Terraform state files, and generated outputs from version control.

The model is intended for campaign prioritization and analytical decision support, not automated credit approval, decline, or customer decisioning.

It is designed as a professional portfolio project for Canadian banking analytics, financial data analyst, data scientist, machine learning analyst, and MLOps-oriented roles.
