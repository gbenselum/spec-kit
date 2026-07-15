# 🌱 Spec Kit: DevOps & SRE Edition

**Spec Kit** is a lightweight Custom Skill for Spec-Driven Development (SDD) designed for AI coding assistants like Claude (via Claude Code or Claude Desktop customizations), focused entirely on **Infrastructure as Code (IaC), CI/CD pipelines, SRE observability, and cloud security architecture**.

Instead of writing application code directly, Spec Kit guides your agent through a structured design and validation workflow to build reliable, secure, and compliant cloud foundations.

---

## ⚡ Setup

To use Spec Kit as a custom agent skill:

1. **For Claude Code**:
   Symlink this directory into your project's `.claude/skills/` folder:
   ```bash
   # Run from your project root
   mkdir -p .claude/skills/
   ln -s /path/to/spec-kit .claude/skills/spec-kit
   ```
2. **For IDE Agent Frameworks**:
   Add this repository path to your workspace customization root (e.g., `.agents/` directory).

Once loaded, Claude will automatically discover the `SKILL.md` file and understand all Spec Kit commands.

---

## 🛠️ How to Use

Invoke the following slash commands in your chat with the agent:

### 1. `/speckit.constitution`
Establish your project's cloud standards, cost limits, and security constraints in `CONSTITUTION.md` at the project root.
```bash
/speckit.constitution
```

### 2. `/speckit.specify [infrastructure_description]`
Describe the infrastructure or pipeline requirements. The agent will:
- Auto-generate a feature number and short name (e.g., `specs/001-vpc-setup/`).
- Create a feature-specific Git branch.
- Generate `spec.md` detailing operational journeys, security rules, and SLO/SLI metrics.
```bash
/speckit.specify "Set up an AWS ECS cluster on Fargate with a private database and secure public load balancer"
```

### 3. `/speckit.plan`
The agent reads your spec, checks compliance against your `CONSTITUTION.md` rules, and designs the architecture:
- Generates `plan.md` outlining resources, modules, and inputs.
- Generates `research.md` (cost estimations and IAM matrices), `topology.md` (subnets and traffic rules), and `quickstart.md` (deploy/destroy validation).
```bash
/speckit.plan
```

### 4. `/speckit.tasks`
The agent maps your plan into concrete provisioning and configuration tasks:
- Generates `tasks.md` grouped by component scope (VPC, IAM, Database, ECS, CI/CD, Alerting) to allow incremental deployment and testing.
```bash
/speckit.tasks
```

### 5. `/speckit.implement`
The agent begins executing the tasks in `tasks.md` sequentially, writing IaC modules or pipeline YAML configs, running static checks (e.g., `tflint`, `checkov`, `tfsec`), and checking off completed items.
```bash
/speckit.implement
```

---

## 🔍 SRE & Helper Commands

- `/speckit.clarify`: Prompt the agent to ask targeted clarifying questions about backup policies, sizing, secrets, and alerting before planning.
- `/speckit.analyze`: Audit plan documents for security gaps (plaintext secrets, open ports) and cost limits before deployment.
- `/speckit.checklist [focus]`: Generate validation checklists (e.g., `secops` security reviews, `cost` optimizations, `dr` disaster recovery runs) under `specs/<NNN>-<short-name>/checklist-<focus>.md`.
- `/speckit.taskstoissues`: Convert your `tasks.md` checkboxes into cards formatted for Jira or GitHub issues.

---

## 📂 Repository Layout

```text
spec-kit/
├── SKILL.md                 # Anthropic Custom Skill definition (DevOps/SRE edition)
├── README.md                # Easy-to-follow guide (this file)
├── demo.md                  # Detailed ECS & Terraform walkthrough
├── LICENSE                  # MIT License
├── .gitignore               # System exclusions
└── templates/               # Structured DevOps templates used by the skill
    ├── spec-template.md
    ├── plan-template.md
    ├── tasks-template.md
    ├── checklist-template.md
    └── constitution-template.md
```

---

## 📄 License & Attribution

This project is a streamlined Custom Skill adaptation of the original [GitHub Spec Kit](https://github.com/github/spec-kit).

The original work is Copyright © GitHub, Inc. and is licensed under the MIT License. See the [LICENSE](LICENSE) file for the full license text.
