---
name: github-workflow
description: Execute GitHub branch, pull request, review, and merge workflow for a single scoped task or epic. Use when creating branches, opening PRs, applying review fixes, and merging after validation.
---

## Purpose

Standardize GitHub workflow execution to ensure clean branches, focused PRs, and reliable merge readiness.

---

## When to use

Use when:

* Creating a new branch for a task or epic
* Opening or updating a pull request
* Addressing review feedback
* Preparing work for merge
* Finalizing and cleaning up branches

---

## When NOT to use

Do NOT use when:

* Writing or implementing code (use development skills instead)
* Reviewing code (use code-review skill)
* Planning tasks without execution

---

## Inputs

* Task or epic scope (required)
* Repository context (branching rules if any)
* Optional:

  * PR feedback
  * test results
  * CI status

---

## Outputs

Must produce:

* Branch name
* PR status (created / updated / ready / merged)
* Summary of changes
* Tests executed
* Merge status

---

## Process

### Step 1 — Create Branch

* Create a focused branch from the correct base
* Naming must reflect scope (feature/fix/refactor + descriptor)

---

### Step 2 — Scope Control

* Include only files required for the task
* Do not mix unrelated work
* Keep commits logically grouped

---

### Step 3 — Open PR

* Open PR when implementation is ready for review
* PR must include:

  * concise description of scope
  * what changed
  * how it was tested

---

### Step 4 — Address Review

* Apply all review feedback on the same branch
* Do not create new branches for fixes
* Keep fixes scoped to review comments

---

### Step 5 — Validate

Before merge:

* All review comments resolved
* Tests pass (local + CI if available)
* No regressions introduced
* Scope remains clean and focused

---

### Step 6 — Merge

* Merge only when:

  * review is clean
  * validation is complete
* Use correct merge strategy (project standard)

---

### Step 7 — Cleanup

* Delete or clean up stale branches
* Ensure repository remains clean

---

## Rules

Must:

* Keep PR scope minimal and focused
* Maintain clear separation between epics
* Ensure PR is reviewable and testable
* Keep PR description concise and informative

Must NOT:

* Mix unrelated work in a single PR
* Mark work complete before merge
* Ignore failing tests or unresolved review comments
* Blur implementation and review responsibilities

---

## Handoff

Always include:

* Branch name
* PR status or URL
* Tests executed
* Merge status

---

## Acceptance Criteria

Workflow is complete only if:

* Branch is correctly scoped and named
* PR is created or updated with clear description
* Review feedback is fully addressed
* Tests pass and validation is complete
* Merge is completed (or explicitly blocked with reason)
* Branch cleanup is performed if applicable

---

## Key Principle

> One branch, one scope, one clean merge.
