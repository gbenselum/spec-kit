---
description: "Task list template for DevOps and Infrastructure deployment"
---

# Tasks: [DEVOPS FEATURE NAME]

**Input**: Design documents from `/specs/[###-feature-name]/`

**Prerequisites**: plan.md (required), spec.md (required for journeys), research.md, topology.md, contracts/

**Tests**: Tests are OPTIONAL - only include if explicitly requested in the specification (e.g. running static security scanners, policy validations, or Terratests).

**Organization**: Tasks are grouped by Operational Journey or Scope to enable independent deployment, testing, and validation of each component.

## Format: `[ID] [P?] [Journey] Description`

- **[P]**: Can run in parallel (different files/modules, no dependencies)
- **[Journey]**: Which operational journey or component this task belongs to (e.g., US1: VPC, US2: IAM/RDS, US3: Compute/ECS, US4: CI/CD Pipeline)
- Include exact file/directory paths in descriptions

## Path Conventions
- **Terraform/IaC**: `terraform/environments/dev/`, `terraform/modules/vpc/`
- **Kubernetes**: `k8s/base/`, `k8s/overlays/dev/`
- **CI/CD**: `.github/workflows/`, `.gitlab-ci.yml`

<!--
  ============================================================================
  IMPORTANT: The tasks below are SAMPLE TASKS for illustration purposes only.

  Replace these sample tasks with actual, concrete tasks based on:
  - Operational journeys from spec.md
  - Infrastructure context from plan.md
  - Network diagrams from topology.md
  - Config inputs from contracts/

  Tasks MUST be organized by operational journey or component scope.
  DO NOT keep these sample tasks in the generated tasks.md file.
  ============================================================================
-->

## Phase 1: Setup (Backend & Providers)

**Purpose**: Remote state initialization and provider configuration

- [ ] T001 Initialize remote state storage backend (e.g. S3 bucket/DynamoDB table for state locks)
- [ ] T002 Configure cloud providers and region variables in `terraform/environments/dev/main.tf`
- [ ] T003 [P] Setup local environment variable files for development secrets management

---

## Phase 2: Foundational (Base Networking & IAM)

**Purpose**: Base VPC network structure and IAM policies. MUST be complete before services can be provisioned.

**⚠️ CRITICAL**: No service provisioning can begin until this phase is complete and verified.

- [ ] T004 Implement VPC with public/private subnets and route tables in `terraform/modules/vpc/`
- [ ] T005 [P] Create NAT Gateways for secure outbound internet from private subnets
- [ ] T006 [P] Provision base IAM execution roles and least-privilege instance profile policies
- [ ] T007 [P] Configure security group templates for cross-subnet traffic rules

**Checkpoint**: Foundation ready - base network and IAM profiles are verified. Service provisioning can now begin in parallel.

---

## Phase 3: Operational Journey 1 - Compute & Database (Priority: P1) 🎯 MVP

**Goal**: Provision the baseline running infrastructure (e.g. database and cluster)

**Independent Verification**: [Describe how to verify this compute block works on its own]

### Verification Tests (OPTIONAL - only if tests requested)
- [ ] T008 [P] [US1] Write Checkov/tfsec static scan tests for compute modules
- [ ] T009 [US1] Write baseline Terratest for verifying VPC-RDS connection block

### Provisioning Implementation
- [ ] T010 [P] [US1] Provision RDS PostgreSQL database instance in `terraform/modules/database/`
- [ ] T011 [P] [US1] Provision ECS cluster with Fargate launch configurations in `terraform/modules/compute/`
- [ ] T012 [US1] Deploy load balancer and listener routing rules for app container traffic
- [ ] T013 [US1] Link RDS secret keys to Secrets Manager

**Checkpoint**: At this point, the baseline compute and database resources should be fully provisioned and connectable.

---

## Phase 4: Operational Journey 2 - CI/CD Pipeline (Priority: P2)

**Goal**: Configure automated deployment workflows

**Independent Verification**: [Describe how to verify pipeline triggers]

### Pipeline Implementation
- [ ] T014 Configure repository secrets mapping in cloud provider credentials manager
- [ ] T015 [P] Implement build and test job workflow steps in `.github/workflows/deploy-dev.yml`
- [ ] T016 Implement container compilation and ECR push job steps
- [ ] T017 [P] Implement ECS task definition updates and automated rollout checks
- [ ] T018 [US2] Add linter, fmt, and checkov static validation checks to PR pull request workflows

**Checkpoint**: Staging pipeline should be fully functional. Pushing to dev branch auto-deploys to staging.

---

## Phase 5: Operational Journey 3 - SRE Observability & Monitoring (Priority: P3)

**Goal**: Set up logging, metrics, and alerting

**Independent Verification**: [Describe how to test triggering an alert]

### SRE Implementation
- [ ] T019 Configure CPU/Memory utilization alert alarms for the cluster container services
- [ ] T020 [P] Set up CloudWatch Log groups with retention policies and error-pattern metrics
- [ ] T021 Set up database health-check monitoring alerts and route to Slack/PagerDuty

---

## Phase N: Polish & Security Hardening

**Purpose**: Cleanup, cost auditing, policy verification

- [ ] TXXX Run tflint and checkov cleanups across all directories
- [ ] TXXX [P] Verify cost-tags are applied to all cloud resources
- [ ] TXXX Run quickstart.md validation (deployment followed by automated teardown verify)
- [ ] TXXX Commit remote state lock states

---

## Dependencies & Execution Order

### Phase Dependencies
- **Setup (Phase 1)**: No dependencies - can start immediately
- **Foundational (Phase 2)**: Depends on Setup - BLOCKS service compute/database provisioning
- **Journeys (Phase 3+)**: Depend on Foundational completion
  - Computes and Pipelines can proceed in parallel (if staffed)
  - Or sequentially (VPC -> Compute -> CI/CD -> SRE alerts)
- **Polish (Final Phase)**: Depends on all resources being fully deployed

### Within Each Journey
- Static code linters and checks run first
- Base modules before integration modules
- Deployments before monitoring alerting setup
- Automated teardown verification before final push
