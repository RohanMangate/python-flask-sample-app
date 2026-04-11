# Jenkins CI/CD Pipeline for Flask Application

## Overview

This project demonstrates the implementation of Continuous Integration and Continuous Deployment (CI/CD) pipelines using both **Jenkins** and **GitHub Actions** for a Python Flask application. The pipelines automate dependency installation, testing, staging deployment, and production deployment.

---

## Technologies Used

- Python 3
- Flask
- Pytest
- Jenkins
- GitHub Actions
- AWS EC2 (Ubuntu)

---

## Repository Structure

```
python-flask-sample-app/
├── app.py
├── test_app.py
├── requirements.txt
├── Jenkinsfile
├── README.md
└── .github/
    └── workflows/
        └── flask-ci-cd.yml
```

---

## Jenkins CI/CD Pipeline

### Jenkins Setup

Jenkins is installed on an AWS EC2 instance running Ubuntu. Java and Python were configured on the Jenkins server to support pipeline execution.

### Pipeline Configuration

The Jenkins pipeline is defined using a `Jenkinsfile` stored in the root of the GitHub repository. Jenkins pulls the source code using Git SCM.

### Pipeline Stages

The Jenkins pipeline consists of the following stages:

| Stage    | Description                                                                 |
|----------|-----------------------------------------------------------------------------|
| **Build**  | Installs required Python dependencies using pip from `requirements.txt`.  |
| **Test**   | Executes unit tests using `pytest` to validate application functionality. |
| **Deploy** | Deploys the Flask application to a staging environment after successful test execution. |

### Triggers

The Jenkins pipeline uses SCM-based execution and is configured to build from the `main` branch. Poll SCM and webhook triggers were not enabled as they are optional and not mandatory for this assignment.

### Notifications

Post-build notifications are implemented using Jenkins pipeline `post` conditions. SMTP email configuration is documented but not enabled, as it is outside the scope of this assignment.

---

## GitHub Actions CI/CD Pipeline

### Workflow Configuration

The GitHub Actions workflow is defined in the file: .github/workflows/flask-ci-cd.yml


### Workflow Triggers

The workflow is triggered under the following conditions:

- **Push** to `main` branch (CI)
- **Push or merge** to `staging` branch (Staging Deployment)
- **Release creation** (Production Deployment)

### Workflow Jobs

1. Install Dependencies
2. Run Tests (`pytest`)
3. Build Application
4. Deploy to Staging
5. Deploy to Production

### Environment Secrets

The workflow references GitHub Secrets (`DEPLOY_KEY`, `API_TOKEN`) to demonstrate secure handling of sensitive values.

### Deployment Strategy

- **Staging Deployment** occurs when changes are pushed to the `staging` branch.
- **Production Deployment** occurs when a GitHub release tag (e.g., `v1.0.0`) is published.

---

## Notes

- Jenkins uses SCM-based pipeline execution.
- Poll SCM and GitHub webhooks were intentionally not enabled.
- SMTP email notifications are documented but not configured.
- GitHub Actions workflows executed successfully for CI, staging, and production deployments.
