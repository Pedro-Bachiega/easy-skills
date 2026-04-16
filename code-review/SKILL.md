---
name: code-review-router
description: Route and execute pull request reviews by selecting only the minimal required review specialties based on changed files, language, and risk profile. Use for any PR review across Kotlin Multiplatform, C++, or mixed interop projects.
---

## Purpose

Route PR reviews to the correct specialty subsets and execute a structured review with minimal context usage.

---

## When to use

Use when:

* Reviewing any pull request
* Multiple languages or domains may be involved
* Context optimization is required
* Review must follow structured severity + output rules

---

## When NOT to use

Do NOT use when:

* Performing implementation instead of review
* Writing new code from scratch
* Doing exploratory analysis without a PR context

---

## Inputs

* PR diff (required)
* Changed file list (required)
* Optional:

  * PR description
  * linked issues
  * architecture context

---

## Outputs

Must produce:

1. Summary
2. Approval status or risk posture
3. Findings by severity (`blocker`, `high`, `medium`, `low`, `note`)
4. Required changes
5. Suggested improvements
6. Scope-specific checks performed
7. Missing tests / validation gaps
8. Routing note (which specialties were used and why)

---

## Process

### Step 1 — Always Load Base Context

Load:

* `review-process.md`
* `review-checklist.md`

---

### Step 2 — Detect Domains

Inspect:

* file extensions
* directories/modules
* API surface changes
* runtime / boundary-sensitive code

Classify into one or more:

* Kotlin / KMP
* C++
* UI (Compose)
* Architecture / API
* Testing
* Security-sensitive
* Performance-sensitive
* Build / packaging
* Interop (FFI / JNI / native)

---

### Step 3 — Apply Risk Routing

Use `risk-routing.md` logic:

Trigger additional specialties if:

* ABI / binary boundary changes → `dll-review.md`, `memory-review.md`
* Cross-language calls → `ffi-review.md`, `interop-review.md`
* State / UI logic → `state-review.md`, `compose-review.md`
* Public API changes → `api-review.md`
* Concurrency / performance paths → `performance-review.md`
* Security or trust boundary → `security-review.md`
* Runtime instrumentation → `runtime-review.md`

---

### Step 4 — Load Minimal Specialty Set

#### Kotlin / KMP

* `kotlin-review.md`
* `kmp-review.md` (if multiplatform)
* `compose-review.md` (if UI)
* `state-review.md` (if state/event logic)

#### C++

* `cpp-review.md`
* `memory-review.md` (if ownership/lifetime relevant)
* `dll-review.md` (if shared libs / ABI)
* `ffi-review.md` (if foreign boundary)
* `interop-review.md` (if Kotlin/native)
* `runtime-review.md` (if instrumentation)
* `build-review.md` (if build/package changes)

#### Cross-cutting (load only if needed)

* `architecture-review.md`
* `api-review.md`
* `testing-review.md`
* `security-review.md`
* `performance-review.md`

---

### Step 5 — Execute Review

Follow `review-process.md`:

1. Understand intent of change
2. Identify risk areas
3. Run checklist (`review-checklist.md`)
4. Apply specialty rules
5. Classify findings by severity
6. Validate tests and coverage
7. Evaluate correctness, safety, and maintainability

---

### Step 6 — Enforce Constraints

Must:

* Minimize loaded specialties
* Avoid irrelevant domains
* Focus on correctness, safety, and clarity
* Respect security restrictions

Must NOT:

* Review outside authorized scope
* Assume intent not present in PR
* Approve with unresolved `blocker` issues

---

## Constraints

* Do not load all specialties by default
* Do not mix Kotlin and C++ reviews unless PR requires it
* Runtime instrumentation reviews must remain:

  * authorized
  * internal
  * defensive or diagnostic

Disallowed:

* unauthorized access patterns
* stealth/evasive modifications
* credential or security bypass logic

---

## Acceptance Criteria

A review is complete only if:

* Correct specialties were selected (minimal set)
* All high-risk areas were analyzed
* Findings are clearly categorized by severity
* Required changes are explicitly actionable
* Missing tests are identified
* Output format is fully respected
* Routing note explains domain coverage

---

## Routing Examples

### KMP Business Logic

Load:

* base
* `kotlin-review.md`
* `kmp-review.md`
* `architecture-review.md`
* `testing-review.md`

---

### Compose UI

Load:

* base
* `kotlin-review.md`
* `compose-review.md`
* `state-review.md`
* `testing-review.md`

---

### C++ DLL

Load:

* base
* `cpp-review.md`
* `dll-review.md`
* `memory-review.md`
* `api-review.md`
* `testing-review.md`
* `build-review.md`

---

### Kotlin ↔ Native Interop

Load:

* base
* `kotlin-review.md`
* `cpp-review.md`
* `ffi-review.md`
* `interop-review.md`
* `dll-review.md`
* `testing-review.md`

---

### Runtime Instrumentation (Authorized)

Load:

* base
* `cpp-review.md`
* `runtime-review.md`
* `security-review.md`
* `testing-review.md`

---

## Key Principle

> Load the minimum required context to produce a complete and correct review.
