# Flask Practice - GitHub Actions CI/CD

This repository demonstrates a CI/CD pipeline for a Flask application using GitHub Actions.

## Workflow

1. **CI (Continuous Integration)**  
   - Triggered on push to `main` or `staging` branches.  
   - Installs dependencies, runs tests, and builds the app.

2. **Deploy to Staging**  
   - Triggered on push to `staging` branch.  
   - Uses secret: `STAGING_API_KEY`.

3. **Deploy to Production**  
   - Triggered on GitHub release creation.  
   - Uses secret: `PROD_API_KEY`.

## Secrets

Add the following GitHub repository secrets under **Settings → Secrets → Actions**:

- `STAGING_API_KEY` → staging deployment key  
- `PROD_API_KEY` → production deployment key

## How to Trigger

- **CI:** Push to `main` or `staging`  
- **Staging Deploy:** Push to `staging`  
- **Production Deploy:** Create a release via **Releases → Draft a new release → Publish release**

