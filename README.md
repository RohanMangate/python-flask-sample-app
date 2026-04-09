# python-flask-sample-app

## Jenkins CI/CD Pipeline for Flask Application

### Overview
This project demonstrates a complete CI/CD pipeline using Jenkins for a Python Flask application. The pipeline automates dependency installation, testing, and deployment.

### Tools Used
- AWS EC2 (Ubuntu 24.04)
- Jenkins
- GitHub
- Python 3
- Flask
- Pytest

### Pipeline Stages
1. **Build**
   - Creates a Python virtual environment
   - Installs dependencies using `requirements.txt`

2. **Test**
   - Runs unit tests using `pytest`

3. **Deploy**
   - Starts the Flask application using Python

### Jenkinsfile
The pipeline is defined using a declarative Jenkinsfile located in the root of the repository.

### How It Works
- Code is pulled from the GitHub `main` branch
- Jenkins automatically builds, tests, and deploys the application
- Pipeline execution status is visible in Jenkins UI

### Notes
Virtual environments are used to comply with Python package management restrictions on modern Ubuntu systems (PEP 668).
