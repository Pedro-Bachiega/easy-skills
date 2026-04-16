# Workspace Router

Use the smallest relevant skill first, then add specialist cards only if the task needs them.

## Routing

- Codebase discovery, file location lookup, and risk triage -> `project-explorer/README.md`
- Code review, PR feedback, regressions, and risk checks -> `code-review/README.md`
- Native C++ implementation, DLLs, runtime hooks, and interop -> `cpp-dev/README.md`
- Kotlin Multiplatform client work, shared logic, and Compose UI -> `kotlin-multiplatform-dev/README.md`
- GitHub branch, PR, and merge flow -> `github/SKILL.md`

## Shared Rules

- Keep changes isolated to the current epic.
- Do not mix unrelated epics in the same change.
- Code, test, review, fix, and merge before marking work done.
- Leave generated output, temp directories, and build folders out of PRs.
- Prefer small additive changes and reusable contracts over broad rewrites.

## Token Discipline

- Read only the relevant skill card.
- Prefer the shortest path that keeps the branch compiling.
- Reuse existing worktrees and branches instead of duplicating context.
