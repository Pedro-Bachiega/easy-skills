# Code Review Skill (Router)

This file is the entry point and router for code review.

Its purpose is to review pull requests with minimal context loading by selecting only the specialty files relevant to the PR.

This review skill is designed to support:
- Kotlin Multiplatform projects
- C++ projects
- mixed-language interop projects
- architecture reviews
- API reviews
- testing reviews
- security-sensitive boundary reviews
- DLL / FFI / runtime instrumentation reviews under authorized scope

---

## Core Principle

> Do not load the full review skill unless the PR truly spans many domains.
> Load only the review specialties required by the code being changed.

---

## Supported Review Targets

### Kotlin Multiplatform
Use this review skill for PRs involving:
- shared Kotlin logic
- source set boundaries
- Compose UI structure
- module organization
- platform integrations
- KMP architecture
- KMP performance and state management

### C++
Use this review skill for PRs involving:
- modern C++ code
- memory/lifetime correctness
- DLL/shared library APIs
- C ABI or FFI boundaries
- Kotlin/native interop
- testing, build, packaging, diagnostics
- authorized runtime instrumentation or hook-related internal tooling

---

## Review Routing Map

### Global Review Rules
- @review-process.md → review method, severity model, output format
- @review-checklist.md → universal checklist for all PRs
- @risk-routing.md → choose which specialties to load

### Architecture & Design
- @architecture-review.md → boundaries, layering, coupling, module concerns
- @api-review.md → API quality, stability, misuse resistance
- @testing-review.md → adequacy of tests and risk coverage
- @security-review.md → unsafe patterns, trust boundaries, misuse risk
- @performance-review.md → performance-sensitive changes

### Kotlin / KMP Reviews
- @kotlin-review.md → Kotlin language and general code quality
- @kmp-review.md → source sets, multiplatform boundaries, shared vs platform correctness
- @compose-review.md → Compose UI review
- @state-review.md → state and event-flow review for Kotlin presentation layers

### C++ Reviews
- @cpp-review.md → modern C++ correctness and maintainability
- @memory-review.md → ownership, RAII, binary-boundary lifetime safety
- @dll-review.md → DLL/shared library export and ABI review
- @ffi-review.md → foreign function boundary review
- @interop-review.md → Kotlin/native boundary review
- @runtime-review.md → controlled review of authorized hooking/instrumentation/runtime-loading code
- @build-review.md → build system and packaging review

---

## Review Output Contract

Every review should produce:

1. Summary
2. Approval status or risk posture
3. Findings by severity
4. Required changes
5. Suggested improvements
6. Scope-specific checks performed
7. Missing tests / missing validation
8. Final routing note describing which review specialties were used

---

## Severity Levels

Use these levels consistently:

- `blocker` → must be fixed before merge
- `high` → serious correctness, security, ABI, data loss, or stability issue
- `medium` → substantial maintainability, design, or test gap
- `low` → cleanup, style, readability, or minor consistency issue
- `note` → observation, optional guidance, or future improvement

---

## Review Restrictions

This review skill does not endorse:
- unauthorized access
- covert tampering
- stealth or evasive behavior
- abuse-oriented runtime modification
- credential theft or bypass behavior
- unsafe deployment of instrumentation outside authorized environments

Any review of hooks, runtime loading, or similar mechanisms must remain constrained to:
- owned software
- authorized internal tooling
- explicit assessment environments
- defensive, diagnostic, compatibility, or lab contexts

---

## Minimal Context Loading Examples

### Example 1: KMP shared business logic PR
Load:
- `review-process.md`
- `review-checklist.md`
- `kotlin-review.md`
- `kmp-review.md`
- `architecture-review.md`
- `testing-review.md`

Do not load:
- `compose-review.md`
- `dll-review.md`
- `ffi-review.md`

### Example 2: Compose screen PR
Load:
- `review-process.md`
- `review-checklist.md`
- `kotlin-review.md`
- `compose-review.md`
- `state-review.md`
- `testing-review.md`

### Example 3: DLL export PR in C++
Load:
- `review-process.md`
- `review-checklist.md`
- `cpp-review.md`
- `dll-review.md`
- `api-review.md`
- `memory-review.md`
- `testing-review.md`
- `build-review.md`

### Example 4: Kotlin calling native library PR
Load:
- `review-process.md`
- `review-checklist.md`
- `kotlin-review.md`
- `cpp-review.md`
- `ffi-review.md`
- `interop-review.md`
- `dll-review.md`
- `testing-review.md`

### Example 5: Authorized runtime instrumentation PR
Load:
- `review-process.md`
- `review-checklist.md`
- `cpp-review.md`
- `runtime-review.md`
- `security-review.md`
- `testing-review.md`
- `debugging or build review context if relevant`

---

## Default Routing Rule

Always load:
- `review-process.md`
- `review-checklist.md`

Then add only the narrow specialties needed by the changed files and risks.

Do not load all Kotlin and C++ review specialties by default.
