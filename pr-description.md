# :rocket: Refactor CI/CD: Split workflows, improve automation and safety

## Summary

This PR restructures the CI/CD pipeline for clarity, automation, and reliability:

- **Splits the workflow into two files:**
  - `.github/workflows/ci.yml` for all build, lint, test, and E2E logic.
  - `.github/workflows/deploy.yml` for deployment to EC2, triggered only after CI passes.
- **Removes** the old `.github/workflows/deploy-to-ec2.yml`.
- **Unifies** all npm commands to use `--prefix` for both backend and frontend for consistency.
- **Adds error management and notification placeholders** for deployment success/failure.
- **Ensures deploy runs only after CI passes** using `workflow_run`.
- **Automates post-deploy server configuration** (including NGINX reverse proxy setup) as part of the deployment process.

---

## Details

- **ci.yml**
  - Runs all backend and frontend checks, builds, and E2E tests on the same runner.
  - Uses `--prefix` for npm commands for both backend and frontend.
- **deploy.yml**
  - Triggered by `workflow_run` on successful completion of the CI workflow.
  - Deploys the app to EC2.
  - Includes error management and notification placeholders.
  - Automates post-deploy server configuration (e.g., NGINX).
- **Removed**: Old monolithic workflow file.

---

## How to test

1. Open a PR to `main`.
2. Ensure the CI workflow runs and passes.
3. On CI success, the deploy workflow will trigger automatically.
4. Check that the application is deployed and accessible via the EC2 instance.

---

## Checklist

- [x] CI workflow passes
- [x] Deploy workflow triggers only after CI passes
- [x] Old workflow file removed
- [x] NPM commands unified with `--prefix`
- [x] Error management and notification placeholders present

---

**Closes:** #<issue-number-if-applicable> 