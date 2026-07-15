---
name: spec-kit
description: "Guides Spec-Driven Development (SDD) — from constitution and specification through planning, task breakdown, implementation, and quality validation."
user-invocable: true
disable-model-invocation: false
---

# Spec-Driven Development (SDD) Custom Skill

This skill guides and automates Spec-Driven Development (SDD) — a workflow where specifications serve as executable sources of truth that generate implementation plans, task lists, and code.

## Core SDD Workflow

The standard sequence is:
1. **Constitution** (Project initialization, once)
2. **Specify** (Define feature requirements, per feature)
3. **Plan** (Design technical architecture, per feature)
4. **Tasks** (Break plan into actionable steps, per feature)
5. **Implement** (Execute tasks and write code, per feature)

---

## Commands & Workflows

When the user invokes any of the commands below, follow these precise execution instructions.

### 📜 `/speckit.constitution`
**Purpose**: Define project-wide governance and engineering principles in `CONSTITUTION.md` at the project root.
**Instructions**:
1. Copy `templates/constitution-template.md` to `CONSTITUTION.md` at the project root.
2. Interactively help the user define core engineering principles, testing gates, and technology constraints.
3. Replace placeholders with finalized guidelines.

---

### 📝 `/speckit.specify [feature_description]`
**Purpose**: Document the feature's natural language requirements.
**Instructions**:
1. Generate a concise short name (2-4 words, hyphenated, e.g., `user-authentication`) from the user description.
2. Determine the next feature number (e.g., `001`, `002`) by scanning directories in `specs/`. If no `specs/` directory exists, default to `001`.
3. Create the directory `specs/<NNN>-<short-name>/` (e.g., `specs/001-user-authentication/`).
4. Copy `templates/spec-template.md` to `specs/<NNN>-<short-name>/spec.md`.
5. Populate the file with:
   - The user's input description.
   - Testable, prioritized user stories (P1, P2, P3...) with Given-When-Then acceptance scenarios.
   - Identified edge cases, functional requirements, entity diagrams, and assumptions.
6. If in a Git repository:
   - Create a branch named `<NNN>-<short-name>`.
   - Commit `specs/<NNN>-<short-name>/spec.md` with a descriptive commit message.

---

### 🗺️ `/speckit.plan`
**Purpose**: Design a technical implementation plan for the active feature.
**Instructions**:
1. Read the specification file `specs/<NNN>-<short-name>/spec.md`.
2. Perform a **Constitution Check**: Check the specification against `CONSTITUTION.md`. If there are potential violations, flag them and discuss them with the user.
3. Copy `templates/plan-template.md` to `specs/<NNN>-<short-name>/plan.md`.
4. Populate `specs/<NNN>-<short-name>/plan.md` with the technical approach, file layout decisions, and dependencies.
5. Create supporting files in `specs/<NNN>-<short-name>/`:
   - `research.md`: Log of technology trade-offs, architecture decisions, and libraries.
   - `data-model.md`: Entity-relationship definitions, database schemas, or state shape.
   - `quickstart.md`: High-level guide defining step-by-step setup and validation scenarios.
   - `contracts/`: A folder containing API specifications (OpenAPI, protobufs) or interface definitions.

---

### 📋 `/speckit.tasks`
**Purpose**: Break the technical plan down into an actionable task checklist.
**Instructions**:
1. Read the feature specification (`spec.md`), plan (`plan.md`), and any schema files (`data-model.md`, `contracts/`).
2. Copy `templates/tasks-template.md` to `specs/<NNN>-<short-name>/tasks.md`.
3. Generate detailed, concrete tasks matching the project's exact file layout and technology stack.
4. **Organize tasks by User Story** (US1, US2, etc.) to ensure that completing a phase yields an independently functional and testable slice of the MVP.
5. Include explicit file paths and use the tag `[P]` for tasks that can be implemented in parallel.

---

### 🛠️ `/speckit.implement`
**Purpose**: Execute the generated tasks to build the feature.
**Instructions**:
1. Read `specs/<NNN>-<short-name>/tasks.md`.
2. Execute tasks sequentially or in parallel, prioritizing P1 user stories first.
3. If the project's constitution or specification requires tests, follow a test-first approach: write tests, verify they fail, then implement to pass them.
4. Mark tasks as complete (`[x]`) in `tasks.md` as you make progress and commit changes incrementally.

---

### 🔍 `/speckit.clarify`
**Purpose**: Ask the user clarifying questions about requirements before planning.
**Instructions**:
1. Analyze the feature specification or description.
2. Identify ambiguous requirements, missing edge cases, or undefined workflows.
3. Present a clear, concise bulleted list of questions to resolve before starting on `plan.md`.

---

### 📊 `/speckit.analyze`
**Purpose**: Check for consistency across all feature artifacts.
**Instructions**:
1. Scan `spec.md`, `plan.md`, and `tasks.md` for discrepancies.
2. Verify that:
   - All functional requirements in `spec.md` have a technical approach in `plan.md`.
   - All components in `plan.md` have corresponding implementation tasks in `tasks.md`.
   - No task contradicts the project's `CONSTITUTION.md`.
3. Output a consistency report flagging any gaps or contradictions.

---

### ✅ `/speckit.checklist [focus]`
**Purpose**: Generate a targeted validation checklist.
**Instructions**:
1. Copy `templates/checklist-template.md` to `specs/<NNN>-<short-name>/checklist-<focus>.md`.
2. Fill it with concrete verification checks tailored to the requested focus (e.g., security, performance, accessibility, SEO, or API endpoints).

---

### 🎫 `/speckit.taskstoissues`
**Purpose**: Convert task lists into tracker-ready formats.
**Instructions**:
1. Read `specs/<NNN>-<short-name>/tasks.md`.
2. Reformat the task list into GitHub Issue markdown templates or structured JSON suitable for uploading to project management tracking systems.
