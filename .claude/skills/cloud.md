---
name: cloud
description: Apply cloud infrastructure standards for AWS and GCP. Use when provisioning resources, designing infrastructure, reviewing IAM policies, or working with any cloud service. All infrastructure must use Terraform — invoke this skill whenever cloud resources or IaC are involved.
---

# Cloud

## Universal Principles
- **IaC mandatory**: never provision resources manually in production — always Terraform
- Infrastructure changes go through code review like any other code
- Terraform state stored remotely (S3 + DynamoDB lock for AWS / GCS for GCP)
- Separate state files per environment (dev / staging / prod)
- `terraform plan` output must be reviewed before `terraform apply`
- No hardcoded credentials in Terraform files

## Terraform Standards
- Modules for reusable infrastructure patterns
- Variables with descriptions and types always defined
- Tag/label all resources (see tagging below)
- Use `.tfvars` per environment — never commit sensitive `.tfvars`
- Pin provider versions in `required_providers`
- Include cost estimate in PRs for infra changes when possible

## Terraform in CI/CD (Automation)
- `terraform fmt` and `terraform validate` on every PR
- `terraform plan` output posted as PR comment
- `terraform apply` only via CD pipeline — never locally in production

## Tagging / Labeling (mandatory on all resources)
```
project    = "[project-name]"
env        = "dev | staging | prod"
owner      = "[team or person]"
managed_by = "terraform"
```

## IAM & Permissions
- Principle of least privilege — always
- Never use root/owner accounts for application workloads
- Service accounts / roles scoped to specific resources and actions
- MFA mandatory for human accounts in production

## Secrets Management
- AWS: Secrets Manager or Parameter Store (SSM)
- GCP: Secret Manager
- Applications fetch secrets at runtime, not at deploy time

## Observability
- Centralized logging mandatory
- Metrics and alerts configured for critical resources
- Budget alerts configured before going to production

---

## AWS Specifics
- VPC with private subnets for application workloads
- Security groups: no `0.0.0.0/0` on sensitive ports
- S3 buckets: block public access by default
- RDS: enable automated backups and encryption at rest

## GCP Specifics
- Use separate projects per environment for isolation
- BigQuery: partition and cluster tables, define expiration policies
- GCS buckets: uniform bucket-level access, no ACLs
- Workload Identity for service-to-service auth (avoid service account keys)
