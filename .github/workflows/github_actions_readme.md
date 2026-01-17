# 🚀 Flask Application CI/CD with GitHub Actions

## 📌 Overview
This repository demonstrates a **CI/CD pipeline** for a Python Flask application using **GitHub Actions**.  
The workflow automates:
- Installing dependencies
- Running unit tests
- Building the application
- Deploying to **staging** and **production** environments

---

## 🛠️ Branching Strategy
- **main** → Production-ready code  
- **staging** → Testing and staging environment  

---

## ⚙️ Workflow File
The pipeline is defined in `.github/workflows/ci-cd.yml`.

### Jobs
1. **Install Dependencies**  
   - Sets up Python  
   - Installs required packages (`requirements.txt`)  
   - Ensures `pytest` is installed  

2. **Run Tests**  
   - Executes the test suite with `pytest`  
   - Uses a MongoDB service container for database-related tests  
   - Fails fast if tests do not pass  

3. **Build**  
   - Prepares the Flask application for deployment  

4. **Deploy to Staging**  
   - Triggered on push to the `staging` branch  
   - Deploys the app to a staging environment  

5. **Deploy to Production**  
   - Triggered when a **release** is created  
   - Deploys the app to production  

---

## 🔑 Environment Secrets
Sensitive information is stored in **GitHub Secrets**.  
Examples:
- `MONGO_URI` → MongoDB connection string  
- `DEPLOY_KEY` → Deployment key for servers  
- `API_TOKEN` → Token for cloud provider or container registry  

Secrets are referenced in the workflow as:
```yaml
env:
  MONGO_URI: ${{ secrets.MONGO_URI }}
