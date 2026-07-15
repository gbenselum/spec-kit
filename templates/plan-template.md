# DevOps Implementation Plan: [INFRASTRUCTURE OR PIPELINE FEATURE]

**Branch**: `[###-feature-name]` | **Date**: [DATE] | **Spec**: [link to specs/###-feature-name/spec.md]

**Input**: Infrastructure specification from `/specs/[###-feature-name]/spec.md`

**Note**: This template is filled in during the planning phase. See `SKILL.md` for the full execution workflow.

## Summary
[Extract from feature spec: primary infrastructure/CI/CD requirement + technical architecture choices]

## Technical Context
<!--
  ACTION REQUIRED: Replace the content in this section with the cloud/infra details.
-->

**Cloud Provider(s) & Region**: [e.g., AWS us-east-1, GCP us-central1, Multi-Cloud or N/A]

**Infrastructure as Code (IaC)**: [e.g., Terraform 1.6+, Pulumi v3, CloudFormation, Ansible]

**CI/CD Pipeline Platform**: [e.g., GitHub Actions, GitLab CI, Jenkins, ArgoCD]

**Observability & Monitoring**: [e.g., CloudWatch, Prometheus/Grafana, Datadog]

**Security & Compliance Scanners**: [e.g., tfsec, checkov, tflint, trivy]

**Target Environments**: [e.g., dev, staging, prod]

**Estimated Monthly Cost (approx.)**: [e.g., $120/mo dev, $450/mo prod or NEEDS CLARIFICATION]

**Disaster Recovery Strategy**: [e.g., Daily automated snapshots, Multi-Region failover, or N/A]

---

## Constitution Check
*GATE: Must pass before Phase 0 research. Re-check after Phase 1 topology design.*

[Provide evidence of compliance with project's CONSTITUTION.md: e.g., standard library tools check, region isolation check, IAM checks]

---

## Infrastructure & Pipeline Structure

### Documentation (this feature)
```text
specs/[###-feature]/
├── plan.md              # Technical implementation plan (this file)
├── research.md          # Technology trade-offs, pricing, and IAM matrices
├── topology.md          # Networking, VPC subnets, and security group diagrams/layout
├── quickstart.md        # Local terraform validation, vars config, deploy & destroy guide
└── contracts/           # Environment variable maps, secrets declarations, Policy-as-Code rules
```

### Source Code (repository root)
<!--
  ACTION REQUIRED: Replace the tree below with the concrete IaC and Pipeline layout.
-->

```text
# [REMOVE IF UNUSED] Option 1: Terraform multi-environment layout
terraform/
├── modules/
│   ├── vpc/             # VPC network layout
│   │   ├── main.tf, variables.tf, outputs.tf
│   ├── compute/         # ECS, EC2, or EKS modules
│   └── database/        # RDS, Aurora, or DynamoDB modules
└── environments/
    ├── dev/             # Dev environment configuration
    │   ├── main.tf (calls modules), backend.tf (remote state), terraform.tfvars
    └── prod/            # Prod environment configuration
        └── main.tf, backend.tf, terraform.tfvars

.github/workflows/
├── deploy-dev.yml       # Dev deployment pipeline
└── deploy-prod.yml      # Staging & Production promotion pipeline

# [REMOVE IF UNUSED] Option 2: Kubernetes Helm Chart structure
k8s/
├── base/                # Kustomize base templates
│   ├── deployment.yaml, service.yaml, ingress.yaml
├── overlays/
│   ├── dev/             # Dev patches
│   └── prod/            # Prod patches
└── charts/
    └── [chart-name]/    # Helm chart for application packaging

.gitlab-ci.yml           # GitLab CI pipeline configuration
```

**Structure Decision**: [Document the selected IaC/Pipeline structure and reference the paths captured above]

---

## Complexity Tracking
> **Fill ONLY if Constitution Check has violations that must be justified**

| Violation | Why Needed | Simpler Alternative Rejected Because |
|-----------|------------|-------------------------------------|
| [e.g., Multi-region VPC peering] | [e.g., compliance requirement] | [e.g., VPN tunnel rejected due to latency bounds] |
