---
name: devops
description: Apply CI/CD, deployment, and environment management standards. Use when designing pipelines, configuring environments, planning deployments, or working with Terraform in CI/CD. Invoke when the user asks about automation, branching strategy, deploy process, or rollback procedures.
---

# DevOps

## Core Principles
- Everything as code: pipelines, infrastructure (Terraform), configuration
- No manual deployments in staging or production
- Every merge to main triggers the pipeline
- Fast feedback: pipelines should complete under 10 minutes ideally

## Environment Strategy
- **dev**: local or ephemeral — fast iteration, mocks allowed
- **staging**: mirrors production — integration and E2E tests run here
- **prod**: locked down, deployment requires passing pipeline + approval gate

## CI Pipeline (on every PR)
1. Lint & format check
2. Unit tests
3. Security scan (dependency audit, secret detection)
4. Build artifact
5. Report coverage

## CD Pipeline (on merge to main)
1. All CI steps
2. Integration tests
3. `terraform plan` (infra changes)
4. Deploy to staging → smoke tests
5. Manual approval gate → deploy to prod
6. Post-deploy health check

## Terraform in CI/CD
- `terraform fmt` and `terraform validate` on every PR
- `terraform plan` output posted as PR comment
- `terraform apply` only via CD pipeline — never locally in production

## Secrets in Pipelines
- Use CI/CD native secret stores (GitHub Actions Secrets, etc.)
- Reference secrets by name, never by value

## Rollback Strategy
- Every deployment must have a documented rollback path
- Database migrations must be backward-compatible during rollout window
- Feature flags for large features — decouple deploy from release

## Branching Strategy
- `main`: always deployable
- `feature/*`, `fix/*`, `chore/*`: short-lived branches
- PRs required for all merges to main
