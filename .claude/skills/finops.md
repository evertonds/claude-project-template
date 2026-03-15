---
name: finops
description: Avoid cost surprises and build cost-awareness into infrastructure decisions. Use when provisioning cloud resources, reviewing infrastructure changes, or evaluating architecture options. Invoke when the user mentions cloud costs, resource sizing, billing, or is about to apply Terraform changes in production.
---

# FinOps

## Principles
- Cost is a non-functional requirement — treat it like performance or security
- Every new cloud resource must have an estimated monthly cost
- Budget alerts configured before going to production
- Tag all resources (project, env, owner) — enables cost attribution

## Before Provisioning Resources
- Estimate monthly cost using the cloud provider's pricing calculator
- Choose the right service tier for the workload — don't over-provision
- Consider reserved instances / committed use for stable workloads

## AWS Cost Controls
- Set AWS Budgets alerts (80% and 100% of budget)
- Lambda: tune memory — it directly affects cost and performance
- RDS: stop non-prod instances outside business hours
- Avoid NAT Gateway overuse — expensive for high egress workloads
- CloudWatch Logs: set retention policies — default is forever

## GCP Cost Controls
- Set billing alerts and budget notifications per project
- BigQuery: always preview query cost before running on large tables
- Cloud Run: set concurrency and max instances to avoid runaway scaling
- GCS: use appropriate storage class (Standard vs Nearline vs Coldline)

## Terraform Cost Hygiene
- Tag every resource via Terraform (enforced in modules)
- Include cost estimate in PR description for infra changes
- Destroy non-production environments when not in use

## Regular Review
- Monthly: review cost breakdown by project/env/service
- Identify idle resources: unattached volumes, stopped instances, unused IPs
- Right-size after 30 days of production data
