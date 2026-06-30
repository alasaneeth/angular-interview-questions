# Azure DevOps — MNC Standard Interview Questions & Answers

*CI/CD · Pipelines · Environments · Git Flow · CD Deploy*

## Section 1: Azure DevOps Basics

### Q1. What is Azure DevOps?

Azure DevOps is a Microsoft cloud platform that provides tools for software development teams. It includes Boards (project management), Repos (Git repositories), Pipelines (CI/CD), Test Plans (manual testing), and Artifacts (package management). It supports the end-to-end DevOps lifecycle.

> 💡 **Tip:** MNC interviews expect you to mention all 5 services: Boards, Repos, Pipelines, Test Plans, Artifacts.

### Q2. What is the difference between Azure Repos and GitHub?

Both are Git-based version control systems. Azure Repos is fully integrated within the Azure DevOps ecosystem and is better for enterprises with tight Azure integration. GitHub is more popular in open-source and supports GitHub Actions. MNCs often use GitHub as the code repo and Azure DevOps for CI/CD pipelines.

> 💡 **Tip:** In interviews mention: "We used GitHub for source control and Azure DevOps for CI/CD pipeline management."

### Q3. What are Azure DevOps Artifacts used for?

Azure Artifacts is a package management service that lets teams create, host, and share packages (npm, NuGet, Maven, Python). MNCs use it for private internal packages that should not be published to public registries like npmjs.com.

> 💡 **Tip:** Example: "@company/ui-kit" internal package stored in Azure Artifacts — not public npm.

### Q4. What is Azure DevOps Test Plans?

Test Plans is a manual testing tool used by QA teams. It allows creating test cases, tracking test runs, progress reports, and exploratory testing sessions. QA engineers use Test Plans to approve the TEST environment before PROD deployment.

> 💡 **Tip:** Say: "Our QA team used Test Plans to verify features in the TEST environment before approving PROD release."

## Section 2: CI/CD Pipeline

### Q1. What is CI/CD? Explain with an example.

CI (Continuous Integration) automatically builds and tests code on every commit. CD (Continuous Delivery/Deployment) automatically deploys the tested code to environments.

Example: Developer pushes code → Azure Pipeline triggers → npm build runs → deploys to DEV → after approval → TEST → PROD.

> 💡 **Tip:** Always give a real project example from your experience in interviews.

### Q2. What is the difference between Continuous Delivery and Continuous Deployment?

**Continuous Delivery:** Code is automatically built and tested, but deployment to PROD requires manual approval.

**Continuous Deployment:** Every successful build is automatically deployed to PROD without manual intervention.

MNCs prefer Continuous Delivery for PROD to retain human control.

> 💡 **Tip:** MNC answer: "We used Continuous Delivery — DEV was automatic, but TEST and PROD required manual approval gates."

### Q3. What is a YAML pipeline in Azure DevOps?

A YAML pipeline defines the CI/CD process as code in a file called `azure-pipelines.yml` stored in the repository. It contains triggers, stages, jobs, and steps. Benefits: version controlled, reviewable via PR, reproducible across environments.

> 💡 **Tip:** YAML pipeline = Pipeline as Code. Always mention it is stored in the repo alongside application code.

### Q4. Explain the stages in your Azure Pipeline.

- **Stage 1 - CI:** npm install, npm run build, publish artifacts
- **Stage 2 - DEV:** Auto deploy when develop branch is pushed
- **Stage 3 - TEST:** Deploy when main branch is pushed, requires manual approval
- **Stage 4 - PROD:** Deploys after TEST approval, requires second manual approval

> 💡 **Tip:** Draw this flow in interviews: CI → DEV → TEST (approve) → PROD (approve).

### Q5. What is a Service Connection in Azure DevOps?

A Service Connection is a secure link between Azure DevOps and external services like GitHub, Azure, AWS, Docker Hub. It stores credentials securely so pipelines can access external resources without hardcoding passwords. Example: a GitHub service connection allows a pipeline to pull code from GitHub.

> 💡 **Tip:** Always say: "We stored all credentials in Service Connections — never hardcoded in YAML."

### Q6. What triggers an Azure Pipeline automatically?

Triggers include: Branch trigger (push to main/develop), PR trigger (when a Pull Request is created), Schedule trigger (cron-based, e.g., nightly builds), and Resource trigger (when another pipeline completes). In a typical project, push to develop triggers the DEV stage and push to main triggers TEST+PROD.

> 💡 **Tip:** YAML example: `trigger: branches: include: [main, develop]`

### Q7. What are Pipeline Artifacts?

Pipeline Artifacts are files produced by one stage that can be passed to subsequent stages. In a React app, the build output (`dist/` folder) is published as an artifact after the CI stage, then downloaded and deployed in the DEV/TEST/PROD stages. This avoids rebuilding the app multiple times.

> 💡 **Tip:** Key point: "Build once, deploy many times" — the same artifact goes to DEV, TEST, and PROD.

## Section 3: Environments & Approvals

### Q1. What are Environments in Azure DevOps?

Environments represent deployment targets like DEV, TEST, and PROD. They track deployment history, provide approval gates, and record which version is running where. Environments help teams know exactly what code is in each stage and who approved each deployment.

> 💡 **Tip:** MNC answer: "We had 3 environments: DEV for developer testing, TEST for QA verification, PROD for end users."

### Q2. How do you configure Manual Approvals in Azure DevOps?

Go to Environments → Select environment (TEST/PROD) → Approvals and checks → Add Approval → Add approvers. When the pipeline reaches that stage, it pauses and sends a notification to approvers. The pipeline proceeds only after approval. A timeout can be set (e.g., 30 days).

> 💡 **Tip:** Say: "TEST required QA lead approval. PROD required both QA lead and Project Manager approval."

### Q3. What branch strategy do you follow in an MNC?

GitFlow: `main` branch for production code, `develop` branch for integration, `feature/*` branches for new features, `fix/*` for bug fixes, `hotfix/*` for production emergency fixes. Feature branches merge to develop first, then develop merges to main after QA approval.

> 💡 **Tip:** Never say you commit directly to main. Always mention PR-based merging with code review.

### Q4. What happens when a hotfix is needed in PROD?

Create a hotfix branch from `main` (not develop). Fix the bug, test locally, raise a PR to main. After approval, merge to main — the pipeline triggers → TEST approval → PROD approval → live. Then back-merge the hotfix to develop to keep branches in sync.

> 💡 **Tip:** `hotfix/*` branches from main, not develop — this is the key MNC standard answer.

## Section 4: CD — Deployment

### Q1. How do you deploy a React app using Azure DevOps CD?

Build the React app using `npm run build` (outputs `dist/` folder). Publish `dist/` as a pipeline artifact. In the CD stage, download the artifact. Deploy to Azure Static Web Apps using the `AzureStaticWebApp` task with an API token stored in pipeline variables. Each environment (DEV/TEST/PROD) has its own Static Web App resource.

> 💡 **Tip:** Azure Static Web Apps free tier supports 3 environments perfectly for DEV/TEST/PROD.

### Q2. What is Azure Static Web Apps?

Azure Static Web Apps is a hosting service optimized for static files (HTML, CSS, JS) and SPAs like React, Vue, Angular. It provides free SSL, custom domains, global CDN, and GitHub/Azure DevOps integration. The free tier supports unlimited bandwidth and custom domains.

> 💡 **Tip:** Perfect for React apps — no server needed, just static files deployment.

### Q3. How do you store secrets in an Azure DevOps Pipeline?

Never hardcode secrets in YAML. Use: Pipeline Variables (Settings → Variables → mark as secret), Variable Groups (Library → Variable Groups — shared across pipelines), or Azure Key Vault integration (most secure — secrets stored in Key Vault, pipeline reads at runtime).

> 💡 **Tip:** MNC answer: "We used Azure Key Vault linked Variable Groups for all secrets like API keys and deployment tokens."

### Q4. What is the difference between Pipeline Variables and Variable Groups?

**Pipeline Variables:** Specific to one pipeline, defined in pipeline settings or YAML.

**Variable Groups:** Defined in Library, can be shared across multiple pipelines.

**Key Vault Variable Groups:** Automatically syncs secrets from Azure Key Vault. MNCs prefer Variable Groups for shared secrets.

> 💡 **Tip:** Interview tip: "Variable Groups allow us to update a secret in one place and all pipelines pick it up automatically."

### Q5. What is a Deployment Strategy in Azure DevOps?

- **runOnce:** Deploys once to all targets (simple apps)
- **Rolling:** Deploys to targets in batches, reduces downtime
- **Blue-Green:** Two identical environments, switch traffic after validation
- **Canary:** Deploy to a small % of users first, then gradually increase

MNCs use Blue-Green or Canary for zero-downtime PROD deployments.

> 💡 **Tip:** For interview: "We used runOnce for DEV/TEST and Blue-Green strategy for PROD to ensure zero downtime."

### Q6. How do you rollback a failed deployment in Azure DevOps?

Re-run a previous successful pipeline run (Pipelines → select run → Re-run). Or use `git revert` to undo commits and push — the pipeline auto-triggers with the reverted code. For Azure Static Web Apps, each deployment creates a snapshot — you can switch back via the Azure Portal. Always keep previous artifact versions.

> 💡 **Tip:** Key MNC answer: "We retained the last 5 successful pipeline artifacts for quick rollback if needed."

## Section 5: Advanced & Scenario Questions

### Q1. Your pipeline fails in TEST but works in DEV. How do you debug?

Check pipeline logs for the exact error (click failed job → view logs). Compare DEV and TEST environment variables — missing secrets are a common cause. Check if the TEST environment has different resource limits. Reproduce locally with TEST environment variables. Use pipeline diagnostic logging: `system.debug = true`.

> 💡 **Tip:** Always mention: "First check the logs, then compare environment variables between DEV and TEST."

### Q2. How do you prevent a developer from directly pushing to main?

In Azure DevOps Repos: Branch Policies → main branch → Require minimum reviewers (min 1-2), require linked work items, require PR comments resolved, build validation (CI must pass before merge), delete source branch after merge. For GitHub: Branch protection rules with similar settings.

> 💡 **Tip:** MNC standard: No direct push to main or develop. All changes via Pull Request with at least 1 reviewer.

### Q3. What is the purpose of "dependsOn" in a YAML pipeline?

`dependsOn` defines the execution order of stages. Example: DEV stage has `dependsOn: CI` — meaning DEV runs only after CI succeeds. PROD has `dependsOn: TEST` — PROD runs only after TEST succeeds. Without `dependsOn`, stages run in parallel.

> 💡 **Tip:** Draw the dependency chain: CI → DEV, CI → TEST (for main branch), TEST → PROD.

### Q4. How do you run a pipeline only for specific branches?

Use conditions in stages: `condition: and(succeeded(), eq(variables['Build.SourceBranch'], 'refs/heads/develop'))` for the DEV stage, and `condition: and(succeeded(), eq(variables['Build.SourceBranch'], 'refs/heads/main'))` for TEST and PROD stages. This ensures DEV deploys only for the develop branch and PROD only for main.

> 💡 **Tip:** This is exactly what's typically implemented — DEV skips on main push, TEST/PROD skip on develop push.

### Q5. What is the Conventional Commits standard?

Conventional Commits is a commit message format: `type(scope): description`. Types include: feat (new feature), fix (bug fix), chore (maintenance), refactor (code restructure), docs (documentation), test (tests), ci (CI/CD changes). Example: `feat(timer): add 4-7-8 phase animation`. Enables automated changelog generation.

> 💡 **Tip:** MNCs use this for automated versioning and changelog generation. Tools like semantic-release use commit types to auto-bump version numbers.

## Quick Reference: Azure DevOps Cheat Sheet

| Concept | Description | MNC Use |
|---|---|---|
| CI | Build + Test on every push | npm install + npm run build |
| CD | Auto deploy to environments | DEV auto, TEST/PROD manual approve |
| Service Connection | Secure external service link | GitHub, Azure connection |
| Environment | Deployment target with approvals | DEV, TEST, PROD |
| Variable Group | Shared secrets across pipelines | API keys, tokens |
| Artifact | Build output passed between stages | dist/ folder |
| Branch Policy | Protect main/develop branches | Require PR + reviewer |
| Approval Gate | Manual review before deploy | QA approves TEST, Lead approves PROD |
| YAML Pipeline | Pipeline as code in repo | azure-pipelines.yml |

---
*Prepared for MNC Interview Preparation · Azure DevOps CI/CD*