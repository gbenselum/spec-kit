# 🚀 Spec Kit: DevOps Custom Skill Demo

This demo walks through a step-by-step example of how to use the Spec Kit custom skill to plan and deploy cloud infrastructure and CI/CD pipelines.

We will walk through a common, realistic DevOps use case: **"Deploying a secure AWS ECS/Fargate Service with a private RDS Database, provisioned via Terraform, and deployed via GitHub Actions."**

---

## 🏗️ The DevOps Use Case: Secure ECS & RDS Stack

Our goal is to build:
1. **Networking**: A VPC with public subnets (for Application Load Balancers) and private subnets (for ECS tasks and RDS databases).
2. **Infrastructure**: ECS Fargate container service and an Aurora PostgreSQL database.
3. **Pipeline**: A GitHub Actions workflow that compiles a Docker image, pushes it to AWS ECR, and deploys it to ECS.
4. **SRE Alerting**: CloudWatch CPU/Memory alerts routed to Slack.

Here is how the Spec Kit custom skill automates and structures this engineering process:

---

### Step 1: `/speckit.constitution`
First, establish the cloud governance policies for the organization.

**You type in chat:**
```bash
/speckit.constitution
```

**The Agent executes:**
1. Copies `templates/constitution-template.md` to `CONSTITUTION.md` in the project root.
2. Interactively aligns with you on constraints (e.g., AWS provider, us-east-1 region, Terraform state locked in S3, least-privilege IAM rules, Checkov static scanning mandatory).
3. Produces the final `CONSTITUTION.md`.

*Snippet from the generated `CONSTITUTION.md`:*
```markdown
# Cloud Infrastructure Constitution

## Core Principles
### I. Remote State Lock
All Terraform deployments must store state in an S3 bucket with versioning enabled and lock state via a DynamoDB table.
### II. Security Baseline
Public ingress is restricted strictly to HTTPS (port 443) on the Application Load Balancers. Database subnets must not have route table entries to the Internet Gateway.
```

---

### Step 2: `/speckit.specify [infrastructure_description]`
Define the specific requirements for this ECS/RDS stack.

**You type in chat:**
```bash
/speckit.specify "AWS ECS cluster with public ALB, private ECS Fargate tasks, and a PostgreSQL RDS database with CI/CD deployment via GitHub Actions."
```

**The Agent executes:**
1. Generates the short name `ecs-rds-fargate`.
2. Scans `specs/` and determines this is feature `001`.
3. Creates the directory `specs/001-ecs-rds-fargate/`.
4. Copies `templates/spec-template.md` to `specs/001-ecs-rds-fargate/spec.md`.
5. Fills it out with operational journeys, security goals, cost limits, and SLOs.
6. Switches to a git branch named `001-ecs-rds-fargate` and commits the specification.

*Snippet from generated `specs/001-ecs-rds-fargate/spec.md`:*
```markdown
# Specification: ECS & RDS Stack

## Operational Journeys
### Operational Journey 1 - Provisioning VPC and RDS (Priority: P1)
As a systems engineer, I want to provision the networking and database modules so that ECS Fargate tasks can securely connect to PostgreSQL.
- **Acceptance Scenario**:
  - **Given** VPC subnets are created
  - **When** I run `terraform apply` on the database module
  - **Then** the RDS instance is created in the private database subnet group
```

---

### Step 3: `/speckit.plan`
Design the cloud architecture layouts and pipeline files.

**You type in chat:**
```bash
/speckit.plan
```

**The Agent executes:**
1. Reads `specs/001-ecs-rds-fargate/spec.md`.
2. Performs the **Constitution Check** (verifying that state lock and region bounds are respected).
3. Copies `templates/plan-template.md` to `specs/001-ecs-rds-fargate/plan.md`.
4. Generates:
   - `plan.md`: Declares the Terraform module hierarchy (vpc, compute, database).
   - `research.md`: Contains instance pricing calculations and IAM policy definitions.
   - `topology.md`: Diagrams subnets (10.0.1.0/24 public, 10.0.2.0/24 private), NAT gateways, and Security Group rules.
   - `quickstart.md`: Guides on initializing remote backend, running local dry-run `terraform plan`, and safe resource teardown.

---

### Step 4: `/speckit.tasks`
Map the architectural plan into concrete implementation tasks.

**You type in chat:**
```bash
/speckit.tasks
```

**The Agent executes:**
1. Copies `templates/tasks-template.md` to `specs/001-ecs-rds-fargate/tasks.md`.
2. Populates `tasks.md` with infrastructure tasks grouped by component scope to ensure incremental verification.

*Snippet from generated `specs/001-ecs-rds-fargate/tasks.md`:*
```markdown
# Tasks: ECS & RDS Stack

## Phase 1: Setup
- [ ] T001 Initialize S3 remote backend bucket in AWS Console
- [ ] T002 Configure AWS provider block in `terraform/environments/dev/main.tf`

## Phase 2: Foundational (Networking)
- [ ] T003 Provision VPC and subnets in `terraform/modules/vpc/`
- [ ] T004 Provision NAT Gateway and configure routing tables for private subnets

## Phase 3: Operational Journey 1 (ECS & RDS Compute)
- [ ] T005 [P] Provision private Aurora PostgreSQL database in `terraform/modules/database/`
- [ ] T006 [P] Provision ECS Cluster and Task Definitions in `terraform/modules/compute/`
```

---

### Step 5: `/speckit.implement`
Deploy the infrastructure and configure the workflows.

**You type in chat:**
```bash
/speckit.implement
```

**The Agent executes:**
1. Reads `tasks.md`.
2. Systematically writes the Terraform configurations (`main.tf`, `variables.tf`) and pipeline files (`.github/workflows/deploy.yml`).
3. Runs Checkov/tfsec static scans to catch open ports or unencrypted disks.
4. Deploys the modules in order: Base VPC -> IAM & RDS -> ECS & ALB -> CI/CD Actions -> Observability alerts.
5. Updates task progress in `tasks.md` and commits incrementally.

---

## 🔍 DevOps Helper Commands

- **`/speckit.clarify`**: Ask clarifying questions about sizing (e.g. RDS db.t4g vs db.r6g instance sizes), target retention times, or security compliance targets.
- **`/speckit.analyze`**: Run a consistency audit on your IaC files to ensure all resources mapped in your topology diagrams match your task checklists.
- **`/speckit.checklist secops`**: Generates a targeted security audit list (checking for plaintext secrets, IAM wildcards, or public subnets access leaks).
