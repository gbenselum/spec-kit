# [PROJECT_NAME] DevOps Constitution
<!-- Example: Cloud Infrastructure Constitution, SRE & CI/CD Governance, etc. -->

## Core Principles

### [PRINCIPLE_1_NAME]
<!-- Example: I. Infrastructure as Code (IaC) Mandatory -->
[PRINCIPLE_1_DESCRIPTION]
<!-- Example: Every piece of cloud infrastructure must be declared as code using Terraform/OpenTofu; no manual modifications ("click-ops") in cloud consoles allowed -->

### [PRINCIPLE_2_NAME]
<!-- Example: II. Automated Testing & Static Analysis -->
[PRINCIPLE_2_DESCRIPTION]
<!-- Example: All IaC code must pass linting (tflint), format checking (fmt), and static security scans (tfsec/checkov) on every pull request before merging -->

### [PRINCIPLE_3_NAME]
<!-- Example: III. Principle of Least Privilege -->
[PRINCIPLE_3_DESCRIPTION]
<!-- Example: IAM policies, security groups, and service roles must declare the minimal permissions required. Star permissions (e.g., Action: "*") are strictly prohibited -->

### [PRINCIPLE_4_NAME]
<!-- Example: IV. Observability by Default -->
[PRINCIPLE_4_DESCRIPTION]
<!-- Example: Every provisioned service (compute, database, cache) must be configured with metrics scraping and alerting thresholds for critical SLO/SLI violations -->

### [PRINCIPLE_5_NAME]
<!-- Example: V. Cost Optimization & Budgeting -->
[PRINCIPLE_5_DESCRIPTION]
<!-- Example: Cloud resources must be tagged with environment, team, and feature IDs. Alerting budgets must be enabled for all non-production environments -->

## Infrastructure Constraints & Standards
<!-- Example: Supported cloud regions, instance families, sizing bounds, etc. -->

[INFRASTRUCTURE_CONSTRAINTS]
<!-- Example:
- Production runs exclusively in aws:us-east-1 and us-west-2.
- Multi-AZ deployment is mandatory for databases in production.
- Plaintext secrets must not be stored in repository; use AWS Secrets Manager or Vault.
-->

## Deployment & Pipeline Workflow
<!-- Example: CI/CD triggers, environment promotion gates, rollbacks, etc. -->

[DEPLOYMENT_WORKFLOW]
<!-- Example:
- All changes must deploy to staging/dev first.
- Production deployments require manual approval gates in the pipeline.
- Automated rollback must trigger if synthetic healthchecks fail post-deployment.
-->

## Governance & Compliance
<!-- Example: Review gates, compliance audits (SOC2/HIPAA), disaster recovery testing, etc. -->

[GOVERNANCE_RULES]
<!-- Example:
- Monthly disaster recovery simulations (chaos testing) must be performed.
- All logs must be retained in encrypted S3 buckets for 365 days.
-->

**Version**: [CONSTITUTION_VERSION] | **Ratified**: [RATIFICATION_DATE] | **Last Amended**: [LAST_AMENDED_DATE]
<!-- Example: Version: 1.0.0 | Ratified: 2026-07-15 | Last Amended: 2026-07-15 -->
