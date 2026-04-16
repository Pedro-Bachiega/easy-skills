---
name: kotlin-multiplatform-router
description: Route and execute Kotlin Multiplatform development tasks by selecting the minimal required specialties across shared logic, platform targets, infrastructure, and quality. Use for KMP architecture, business logic, and cross-platform implementation.
---

## Purpose

Coordinate Kotlin Multiplatform development by routing tasks to the correct specialty modules while enforcing clean architecture, shared logic discipline, and minimal context usage.

---

## When to use

Use when:

* Implementing or modifying KMP shared or platform code
* Designing module structure or architecture
* Working on domain, use cases, or state management
* Implementing networking, storage, or serialization
* Handling platform-specific integrations (Android, JVM, iOS)
* Defining expect/actual abstractions
* Writing tests or improving quality/security

---

## When NOT to use

Do NOT use when:

* Working exclusively on UI (use Compose UI skill)
* Performing code review (use code-review skill)
* Working outside Kotlin Multiplatform context

---

## Inputs

* Task description (required)
* Relevant modules or files (optional)
* Constraints:

  * target platforms
  * architecture requirements
  * performance or lifecycle constraints

---

## Outputs

Depending on task, must produce:

* Implementation or changes
* Architecture/module decisions (if applicable)
* Platform abstraction strategy (if needed)
* Tests and validation steps
* Integration points across targets

---

## Process

### Step 1 — Classify Task

Determine involved domains:

* Core architecture
* Business logic (domain / use cases / state)
* Infrastructure (network / storage / serialization)
* Platform-specific implementation
* Platform abstraction (expect/actual)
* Testing / quality
* Security

---

### Step 2 — Select Minimal Specialties

#### Core Architecture

* `core/architecture.md` → boundaries and layering
* `core/modules.md` → module structure
* `core/common.md` → shared (`commonMain`) rules

#### Business Logic

* `business/domain.md` → domain models and invariants
* `business/usecases.md` → application logic
* `business/state.md` → shared state management

#### Infrastructure

* `data/network.md` → networking layer
* `data/storage.md` → persistence
* `data/serialization.md` → formats and parsing

#### Platform Targets

* `platform/android.md` → Android implementation
* `platform/jvm.md` → JVM/desktop/server
* `platform/ios.md` → iOS integration

#### Platform Abstractions

* `platform/expect-actual.md` → abstraction strategy
* `platform/platform-services.md` → OS-level APIs

#### Quality

* `quality/testing.md` → testing strategy
* `quality/security.md` → trust boundaries and safety

---

### Step 3 — Apply Routing Rules

Load only required specialties:

* Shared business logic
  → `core/common.md`, `business/domain.md`, `business/usecases.md`

* State management
  → `business/state.md`, `core/common.md`

* Networking
  → `data/network.md`, `data/serialization.md`, `quality/testing.md`

* Persistence
  → `data/storage.md`, `data/serialization.md`

* Platform feature (Android/iOS/JVM)
  → corresponding platform file + `expect-actual.md` (if shared API)

* Cross-platform abstraction
  → `platform/expect-actual.md`, `core/common.md`

* Security-sensitive logic
  → `quality/security.md`, plus relevant domain/infrastructure files

---

### Step 4 — Execute Task

Follow deterministic workflow:

1. Understand requirements and constraints
2. Identify shared vs platform-specific boundaries
3. Apply selected specialty rules
4. Implement logic in correct source set:

   * `commonMain` when possible
   * platform source sets only when required
5. Ensure separation:

   * business logic independent of platform
   * UI not involved
6. Add or update tests
7. Validate cross-platform behavior

---

### Step 5 — Validate

Ensure:

* Shared logic is correctly placed in `commonMain`
* Platform code exists only where required
* expect/actual contracts are consistent
* No business logic leaks into platform or UI layers
* Module dependencies are respected
* Tests cover critical paths
* Serialization/network/storage boundaries are safe

---

## Rules

Must:

* Keep files single-responsibility
* Prefer shared code over duplication
* Use platform code only when unavoidable
* Keep UI as a consumer only (no business logic)

Must NOT:

* Duplicate logic across source sets
* Introduce platform dependencies into `commonMain`
* Mix infrastructure with domain logic
* Leak business rules into UI or platform layers

---

## Constraints

* UI is explicitly excluded from this skill
* All platform abstractions must be explicit (expect/actual)
* Module boundaries must be preserved
* Cross-platform behavior must remain consistent

---

## Acceptance Criteria

Task is complete only if:

* Correct specialties were selected (minimal set)
* Shared vs platform boundaries are respected
* Business logic resides in shared code when possible
* Platform-specific code is isolated and justified
* Tests are added or updated
* Integration across targets is validated
* No architectural violations are introduced

---

## Explicit Exclusion

Compose UI is not handled here.

Use:

* `ui/compose-ui.md`

---

## Key Principle

> Shared when possible, platform when necessary, never mixed.
