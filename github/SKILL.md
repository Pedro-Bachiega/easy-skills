---
name: github
description: GitHub workflow for the Tibia workspace. Use when creating branches, opening PRs, addressing review, pushing fixes, or merging work after review and tests are clean.
---

# GitHub Workflow

Use this skill for branch, PR, review, and merge flow.
Keep the scope tight.

## Workflow

1. Create a focused branch.
2. Push only the files needed for the epic.
3. Open the PR when the branch is ready for review.
4. Apply review fixes on the same branch.
5. Merge only after review is clean and tests pass.
6. Close or clean up stale branches when done.

## Rules

- Do not mix unrelated epics in one PR.
- Do not mark work done before merge.
- Prefer concise PR bodies that explain scope and tests.
- Keep review feedback separate from implementation.

## Handoff

Include:

- branch name
- PR URL
- tests run
- merge status
