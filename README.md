# 🌱 Spec Kit

**Spec Kit** is a lightweight Custom Skill for Spec-Driven Development (SDD) designed for AI coding assistants like Claude (via Claude Code or Claude Desktop customizations).

By treating specifications as executable documentation, Spec Kit guides your AI agent through a predictable, high-quality development lifecycle using structured markdown templates.

---

## ⚡ Setup

To use Spec Kit as a custom agent skill:

1. **For Claude Code**:
   Copy or symlink this directory into your project's `.claude/skills/` directory:
   ```bash
   # From your project root
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
Establish your project's core principles, design guidelines, and tech constraints in `CONSTITUTION.md` at the project root.
```bash
/speckit.constitution
```

### 2. `/speckit.specify [feature_description]`
Describe the feature in natural language. The agent will:
- Auto-generate a feature number and short name (e.g., `specs/001-user-login/`).
- Switch to a feature-specific Git branch.
- Generate `spec.md` with prioritized user stories using Given-When-Then acceptance scenarios.
```bash
/speckit.specify "Create a drag-and-drop dashboard for photo albums"
```

### 3. `/speckit.plan`
The agent reads your specification, verifies compliance with `CONSTITUTION.md`, and designs a technical architecture:
- Generates `plan.md` outlining the code structures and dependencies.
- Generates `research.md`, `data-model.md`, `quickstart.md`, and interface `contracts/`.
```bash
/speckit.plan
```

### 4. `/speckit.tasks`
The agent breaks down the technical plan into a task checklist:
- Generates `tasks.md` grouped by user story (enabling incremental MVP verification).
- Defines parallel implementation opportunities.
```bash
/speckit.tasks
```

### 5. `/speckit.implement`
The agent begins executing the tasks in `tasks.md` sequentially, committing code incrementally, and checking off completed items.
```bash
/speckit.implement
```

---

## 🔍 Helper Commands

- `/speckit.clarify`: Use this before planning to prompt the agent to analyze the requirements and ask targeted clarifying questions.
- `/speckit.analyze`: Verify consistency and ensure all requirements map to technical plans and task items.
- `/speckit.checklist [focus]`: Create custom quality checklists (e.g., security, performance, SEO) under `specs/<NNN>-<short-name>/checklist-<focus>.md`.
- `/speckit.taskstoissues`: Convert the `tasks.md` file into formatted templates for GitHub Issues or other trackers.

---

## 📂 Repository Layout

```text
spec-kit/
├── SKILL.md                 # Anthropic Custom Skill definition and instructions
├── README.md                # Easy-to-follow guide (this file)
├── LICENSE                  # MIT License
├── .gitignore               # Exclusions
└── templates/               # Structured templates used by the skill
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
