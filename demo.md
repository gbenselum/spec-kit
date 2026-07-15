# 🚀 Spec Kit: Custom Skill Demo

This demo walks through a step-by-step example of how to use the Spec Kit custom skill to build a feature from scratch. 

We will use a playful, bogus feature: **"The Shakespearean Code Critic CLI"** — a CLI tool that parses code comments in your project, translates them into Shakespearean English, and rates the dramatic tension of your codebase on a scale of 1 to 10.

---

## 🎭 The Bogus Feature: Shakespearean Code Critic

Our goal is to build a CLI tool that:
1. Scans a file for code comments.
2. Translates those comments to Shakespearean English (e.g., `# TODO: Fix database leak` becomes `# Hark! Repair the leaking vessel of data!`).
3. Scores the codebase's drama level.

Here is how you use the Spec Kit custom skill to build it:

---

### Step 1: `/speckit.constitution`
Before creating any feature, establish the project's quality rules. 

**You type in chat:**
```bash
/speckit.constitution
```

**The Agent executes:**
1. Copies `templates/constitution-template.md` to `CONSTITUTION.md` in the project root.
2. Asks for constraints (e.g., Python 3.11, zero third-party translation APIs, standard library only).
3. Produces the final `CONSTITUTION.md`.

*Snippet from generated `CONSTITUTION.md`:*
```markdown
# Shakespearean Critic Constitution

## Core Principles
### I. Standard Library Only
To keep the application "light as a feather," no external translation packages (like spaCy or NLTK) may be used. Translation must be rule-based.
### II. Test-First Verification
All translation rules must have unit tests written and verified before the parser is built.
```

---

### Step 2: `/speckit.specify [description]`
Now, define the requirements for the critic CLI.

**You type in chat:**
```bash
/speckit.specify "Build a CLI that scans a Python file, extracts comments, converts them to Shakespearean phrasing, and outputs a drama rating from 1 to 10."
```

**The Agent executes:**
1. Generates the short name `shakespearean-critic`.
2. Scans `specs/` and determines this is feature `001`.
3. Creates the directory `specs/001-shakespearean-critic/`.
4. Copies `templates/spec-template.md` to `specs/001-shakespearean-critic/spec.md`.
5. Fills it out with testable user stories (P1: Parsing and translation, P2: Drama rating).
6. Creates and switches to a git branch named `001-shakespearean-critic`, then commits the spec.

*Snippet from generated `specs/001-shakespearean-critic/spec.md`:*
```markdown
# Feature Specification: Shakespearean Code Critic

**Feature Branch**: `001-shakespearean-critic`

## User Stories
### User Story 1 - Translate Comments (Priority: P1)
As a developer, I want to scan a Python file so that I can see my comments rewritten in dramatic Shakespearean prose.
- **Acceptance Scenario**: 
  - **Given** a file with `# TODO: fix authentication`
  - **When** the CLI runs with `--file auth.py`
  - **Then** the output contains `Hark! Mend the gates of authentication!`
```

---

### Step 3: `/speckit.plan`
Design the technical architecture and platform decisions.

**You type in chat:**
```bash
/speckit.plan
```

**The Agent executes:**
1. Reads `specs/001-shakespearean-critic/spec.md`.
2. Validates it against `CONSTITUTION.md` (verifying standard library compliance).
3. Copies `templates/plan-template.md` to `specs/001-shakespearean-critic/plan.md`.
4. Generates:
   - `plan.md`: Outlines a single-file Python structure.
   - `research.md`: Maps dictionary replacements for common words (e.g., "fix" -> "mend", "database" -> "vault").
   - `quickstart.md`: Provides sample commands and verification guidelines.

---

### Step 4: `/speckit.tasks`
Create the step-by-step checklist of tasks.

**You type in chat:**
```bash
/speckit.tasks
```

**The Agent executes:**
1. Copies `templates/tasks-template.md` to `specs/001-shakespearean-critic/tasks.md`.
2. Replaces sample tasks with concrete ones matching the single-file layout.

*Snippet from generated `specs/001-shakespearean-critic/tasks.md`:*
```markdown
# Tasks: Shakespearean Code Critic

## Phase 1: Setup
- [ ] T001 Initialize script file `src/critic.py`
- [ ] T002 Configure test framework in `tests/test_critic.py`

## Phase 2: Foundational
- [ ] T003 Implement basic regex-based comment parser in `src/critic.py`

## Phase 3: User Story 1 (Translation)
- [ ] T004 Write translation dictionary in `src/critic.py`
- [ ] T005 [P] Implement translation logic replacing modern words with Elizabethan equivalents
```

---

### Step 5: `/speckit.implement`
Build the code systematically.

**You type in chat:**
```bash
/speckit.implement
```

**The Agent executes:**
1. Reads `tasks.md`.
2. Executes tasks sequentially:
   - Creates the file structure.
   - Writes tests first.
   - Implements translation logic to pass the tests.
3. Checks off tasks (`[x]`) and commits changes incrementally.

---

## 💡 Quick Tips

- **Unsure about requirements?** Run `/speckit.clarify` before `/speckit.plan`. The agent will present a concise list of clarifying questions.
- **Want to audit your work?** Run `/speckit.analyze` at any point to verify that everything matches between your `spec.md`, `plan.md`, and code!
