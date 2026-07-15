---
name: spec-kit
description: "Guides Spec-Driven Development (SDD) for DevOps: Infrastructure as Code (IaC), CI/CD pipelines, SRE observability, and cloud security architecture."
user-invocable: true
disable-model-invocation: false
---

# Spec-Driven Development (SDD) Custom Skill: DevOps & SRE Edition

This skill guides and automates Spec-Driven Development (SDD) tailored specifically for infrastructure engineering, cloud architecture, CI/CD, SRE, and security operations. It uses structured specifications to generate IaC plan topologies, pipeline tasks, and resource implementation checklists.

## Core DevOps SDD Workflow

The standard sequence is:
1. **Constitution** (Cloud compliance, IaC, and deployment policies, once)
2. **Specify** (Define infrastructure, security, or pipeline requirements, per feature)
3. **Plan** (Design network topologies, IAM roles, cloud resources, and cost bounds, per feature)
4. **Tasks** (Break provisioning and pipeline setup into prioritized, testable tasks, per feature)
5. **Implement** (Execute tasks, validate with Policy-as-Code tools, and deploy, per feature)

---

## Commands & Workflows

When the user invokes any of the commands below, follow these precise execution instructions.

### 📜 `/speckit.constitution`
**Purpose**: Establish project-wide infrastructure compliance, cost controls, and deployment rules in `CONSTITUTION.md` at the project root.
**Instructions**:
1. Copy `templates/constitution-template.md` to `CONSTITUTION.md` at the project root.
2. Interactively help the SRE/DevOps engineer define:
   - Permitted cloud providers (AWS, GCP, Azure, etc.) and region constraints.
   - Mandatory IaC tooling (e.g., Terraform module requirements, state locks).
   - Compliance targets (SOC2, HIPAA, PCI-DSS) and network isolation rules.
   - Cost limits, scaling policies, and disaster recovery SLA targets (RTO/RPO).
3. Replace placeholders with finalized guidelines.

---

### 📝 `/speckit.specify [feature_description]`
**Purpose**: Document the requirements for a new cloud component, CI/CD pipeline, SRE monitoring suite, or security change.
**Instructions**:
1. Generate a concise, hyphenated short name (2-4 words, e.g., `ecs-fargate-ci`) from the description.
2. Determine the next feature number (e.g., `001`, `002`) by scanning directories in `specs/`. If no `specs/` directory exists, default to `001`.
3. Create the directory `specs/<NNN>-<short-name>/` (e.g., `specs/001-ecs-fargate-ci/`).
4. Copy `templates/spec-template.md` to `specs/<NNN>-<short-name>/spec.md`.
5. Populate the file with:
   - The user's input infrastructure description.
   - User Journeys / Operational Scenarios (P1: Primary pipeline/infra provisioning, P2: Alerting/autoscaling, P3: Disaster recovery).
   - High-level functional security/compliance requirements and scalability assumptions.
6. If in a Git repository:
   - Create a branch named `<NNN>-<short-name>`.
   - Commit `specs/<NNN>-<short-name>/spec.md` with a clear commit message.

---

### 🗺️ `/speckit.plan`
**Purpose**: Design a technical implementation plan for the active DevOps feature.
**Instructions**:
1. Read the specification file `specs/<NNN>-<short-name>/spec.md`.
2. Perform a **Constitution Check**: Check the specification against `CONSTITUTION.md` (e.g., verifying region restrictions, instance type limits, or SSL-only traffic rules). Flag any violations.
3. Copy `templates/plan-template.md` to `specs/<NNN>-<short-name>/plan.md`.
4. Populate `specs/<NNN>-<short-name>/plan.md` with the cloud resource tree, IAM policies, and variables structure.
5. Create supporting files in `specs/<NNN>-<short-name>/`:
   - `research.md`: Cloud service pricing tables, CLI syntax references, and IAM permission matrices.
   - `topology.md`: Network routing, subnet structures, firewall/security group ingress/egress layouts.
   - `quickstart.md`: Instructions defining step-by-step setup, terraform plan validation steps, variables config, and clean teardown checks.
   - `contracts/`: A folder containing environment variables maps, secret declarations, or Policy-as-Code rules.

---

### 📋 `/speckit.tasks`
**Purpose**: Break the infrastructure design plan down into a concrete, runnable task checklist.
**Instructions**:
1. Read the feature specification (`spec.md`), plan (`plan.md`), and any topology or config files (`topology.md`, `contracts/`).
2. Copy `templates/tasks-template.md` to `specs/<NNN>-<short-name>/tasks.md`.
3. Generate detailed, concrete tasks matching the exact IaC modules and pipeline files.
4. **Organize tasks by Environment / Scope** (e.g., US1: Setup/Base Networking, US2: Security Groups & IAM, US3: Provisioning Compute/DB, US4: CI/CD Workflows) to enable incremental provisioning and validation.
5. Include explicit file paths and use the tag `[P]` for tasks that can be written or provisioned in parallel.

---

### 🛠️ `/speckit.implement`
**Purpose**: Provision the resources and build the pipelines defined in the tasks.
**Instructions**:
1. Read `specs/<NNN>-<short-name>/tasks.md`.
2. Systematically write IaC modules or pipeline YAML configs.
3. Run linting and static security checkers (e.g., `tflint`, `tfsec`, `checkov`, `hadolint`) and write integration validation steps (e.g. `terratest` or pipeline dry runs).
4. Mark tasks as complete (`[x]`) in `tasks.md` and commit changes incrementally.

---

### 🔍 `/speckit.clarify`
**Purpose**: Resolve SRE/cloud ambiguities before planning.
**Instructions**:
1. Analyze the infrastructure specification or description.
2. Identify ambiguous sizing requirements, backup retention periods, IAM scope creeps, or alerting thresholds.
3. Present a clear, concise bulleted list of questions to resolve before starting on `plan.md`.

---

### 📊 `/speckit.analyze`
**Purpose**: Check for architectural compliance and security gaps.
**Instructions**:
1. Scan `spec.md`, `plan.md`, and `tasks.md` for discrepancies.
2. Verify that:
   - All network ingress rules are documented and locked down.
   - Cost estimates and budget limits are declared.
   - Secrets are managed via a secrets manager, not plaintext environment variables.
   - Disaster recovery scenarios correspond to task checks.
3. Output a compliance analysis report.

---

### ✅ `/speckit.checklist [focus]`
**Purpose**: Generate a targeted compliance or SRE checklist.
**Instructions**:
1. Copy `templates/checklist-template.md` to `specs/<NNN>-<short-name>/checklist-<focus>.md`.
2. Fill it with concrete validation checklist items tailored to the requested focus (e.g., `secops` security auditing, `cost` cost optimizations, `dr` disaster recovery exercises, or `observability` SLO/SLI alerts validation).

---

### 🎫 `/speckit.taskstoissues`
**Purpose**: Reformat tasks into ticketing system cards.
**Instructions**:
1. Read `specs/<NNN>-<short-name>/tasks.md`.
2. Reformat the task list into structured Markdown tickets or JSON formats ready to import into task managers like Jira.
