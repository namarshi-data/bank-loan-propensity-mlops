# Deployment Guide

## Deployment Scope

This project packages the trained loan propensity model for repeatable customer-level scoring through a Flask API. The deployment files are designed for **local and containerized execution readiness**.

This repository includes templates for:

- Flask API serving
- Docker containerization
- Kubernetes deployment and service manifests
- Terraform template for AWS ECR repository creation
- GitHub Actions CI validation

It does **not** claim a live AWS, EKS, Kubernetes, or production deployment unless separate deployment evidence is added.

---

## Prerequisites

Recommended local setup:

- Python 3.10+
- Git
- Docker Desktop, optional for containerized execution
- kubectl, optional for Kubernetes template testing
- Terraform, optional for infrastructure template testing
- AWS CLI, optional for AWS/ECR workflows

---

## Local Environment Setup

Create and activate a virtual environment:

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

Install dependencies:

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

---

## Raw Data Setup

Raw data is intentionally excluded from GitHub. Place the source files locally in:

```text
data/raw/Data1.csv
data/raw/Data2.csv
```

Do not commit raw datasets, processed datasets, model artifacts, credentials, or generated outputs.

---

## Run the Full Pipeline

Run the complete pipeline:

```bash
python scripts/run_pipeline.py
```

The pipeline performs:

```text
data cleaning and preprocessing
feature engineering
train-test split
model training
model evaluation
model artifact export
```

---

## Run the Flask API Locally

After training the model, start the API:

```bash
python flask_app/app.py
```

Send a test prediction request:

```bash
curl -X POST http://localhost:5000/predict \
  -H "Content-Type: application/json" \
  -d @flask_app/sample_request.json
```

Example response:

```json
{
  "success": true,
  "result": {
    "prediction": 1,
    "loan_acceptance_probability": 0.94,
    "propensity_label": "High Propensity",
    "classification_threshold": 0.49
  }
}
```

---

## API Endpoint

| Endpoint | Method | Purpose |
|---|---|---|
| `/predict` | POST | Scores one customer record and returns loan propensity output |

The API is intended to demonstrate repeatable model scoring and API contract design. It is not a production banking service.

---

## Docker Execution

Build the Docker image:

```bash
docker build -f docker/Dockerfile -t bank-loan-propensity-api:latest .
```

Run the container locally:

```bash
docker run -p 5000:5000 bank-loan-propensity-api:latest
```

Test the API:

```bash
curl -X POST http://localhost:5000/predict \
  -H "Content-Type: application/json" \
  -d @flask_app/sample_request.json
```

---

## Kubernetes Template

The Kubernetes manifests are included as deployment templates.

Apply the deployment and service:

```bash
kubectl apply -f kubernetes/deployment.yaml
kubectl apply -f kubernetes/service.yaml
kubectl get pods
kubectl get svc
```

Before applying in a real environment, update the container image name in:

```text
kubernetes/deployment.yaml
```

Kubernetes evidence should only be added after running the service in a real cluster.

---

## Terraform Template

The Terraform folder includes an AWS ECR repository template for publishing container images.

```bash
cd terraform
terraform init
terraform plan
terraform apply
```

AWS resources may create costs. Destroy test resources after use:

```bash
terraform destroy
```

Do not commit:

- Terraform state files
- AWS credentials
- Local environment variables
- Secrets
- Access keys

---

## GitHub Actions CI

The GitHub Actions workflow validates the project by:

- Installing dependencies
- Compiling Python files
- Running unit tests
- Checking Docker build readiness

Workflow path:

```text
.github/workflows/ci.yml
```

---

## Deployment Evidence Checklist

Only add deployment screenshots or claims when real execution evidence exists.

| Evidence Type | Required Before Claiming |
|---|---|
| Local API | Screenshot or terminal output showing Flask API running |
| API prediction | Successful `/predict` response using sample request |
| Docker | Successful build and container run output |
| Kubernetes | Pods and service running in a real cluster |
| Terraform | Successful `terraform plan` or `apply` output |
| CI | Passing GitHub Actions workflow badge or screenshot |
| Cloud deployment | Real endpoint, cloud logs, and cost-aware deployment notes |

---

## Portfolio Positioning

This deployment layer demonstrates MLOps readiness while staying honest about scope. The project is structured to show how an analytics model can be packaged, tested, containerized, and prepared for deployment without claiming unsupported production infrastructure.
