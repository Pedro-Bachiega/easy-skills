# Workspace Explorer Skill

This file is the entry point for read-only repository exploration.

Use it when the task is to map the codebase, locate relevant files, or identify constraints before implementation or review.

## Core Principle

> Read only the minimum needed to answer the question.

---

## Exploration Routing

- Repository layout, file locations, and feature mapping -> inspect the relevant workspace area first
- Kotlin Multiplatform feature discovery -> then load `kotlin-multiplatform-dev/README.md`
- Native C++ discovery -> then load `cpp-dev/README.md`
- Review and regression discovery -> then load `code-review/README.md`

---

## Output Contract

Return:

1. concise file map
2. relevant constraints
3. likely dependencies
4. risks or open questions
5. next best skill to load

---

## Rules

- do not edit files
- do not load unrelated skill trees
- do not speculate when file evidence is available
- keep answers short and actionable

---

## Minimal Loading Guide

Start with:

- `AGENTS.md`
- `.codex/skills/router.md`

Then load only the specialist skill needed for the exploration target.
