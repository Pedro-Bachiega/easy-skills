---
name: workspace-explorer
description: Explore a repository in read-only mode to map structure, locate relevant files, and identify constraints before implementation or review. Use for codebase discovery and task scoping.
---

## Purpose

Provide a minimal, accurate understanding of the workspace by identifying only the files, constraints, and dependencies required to answer a question or prepare the next step.

---

## When to use

Use when:

* Mapping repository structure
* Locating files or features
* Understanding how a system is organized
* Identifying dependencies before implementation
* Scoping a task prior to development or review

---

## When NOT to use

Do NOT use when:

* Implementing or modifying code
* Performing code review
* Executing tasks beyond discovery

---

## Inputs

* Exploration question or goal (required)
* Optional:

  * feature name
  * file/module hints
  * target language or domain

---

## Outputs

Must produce:

1. Concise file map
2. Relevant constraints
3. Likely dependencies
4. Risks or open questions
5. Next best skill to load

---

## Process

### Step 1 — Minimal Entry Load

Start with:

* `AGENTS.md`
* `.codex/skills/router.md`

---

### Step 2 — Scope Discovery

Identify:

* target feature or system area
* relevant language/domain (Kotlin, C++, etc.)
* likely module or directory boundaries

---

### Step 3 — Targeted Exploration

Inspect only:

* directories directly related to the task
* key entry points (modules, APIs, configs)

Avoid:

* scanning entire repository
* loading unrelated systems

---

### Step 4 — Route to Specialist (if needed)

Only after initial discovery:

* Kotlin Multiplatform
  → `kotlin-multiplatform-dev/SKILLS.md`

* C++ / Native
  → `cpp-dev/SKILLS.md`

* Review / Regression
  → `code-review/SKILLS.md`

Load only if required to refine understanding.

---

### Step 5 — Synthesize Findings

Produce structured output:

* File map → relevant paths and structure
* Constraints → architectural, platform, or build limitations
* Dependencies → modules, services, or APIs involved
* Risks → unclear areas, missing info, or complexity
* Next step → exact skill to load next

---

## Rules

Must:

* Read only what is necessary
* Stay within exploration scope
* Base conclusions on file evidence
* Keep output concise and actionable

Must NOT:

* Modify or suggest modifying files
* Load unrelated skill trees
* Speculate without evidence
* Expand scope beyond the question

---

## Constraints

* Read-only operation only
* Minimal context loading enforced
* No cross-domain expansion unless required
* No duplication of other skill responsibilities

---

## Acceptance Criteria

Exploration is complete only if:

* Relevant files are clearly identified
* Structure is understandable from output
* Constraints and dependencies are explicit
* Risks or unknowns are surfaced
* A precise next skill is recommended

---

## Key Principle

> Discover just enough to act correctly—nothing more.
