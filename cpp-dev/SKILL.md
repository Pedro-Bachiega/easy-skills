---
name: cpp-development-router
description: Route and execute C++ development tasks by selecting the minimal required specialty modules based on task type, domain, and risk. Use for professional C++ work including core development, DLLs, interop, performance, and authorized instrumentation.
---

## Purpose

Route C++ development tasks to the correct specialty modules and ensure execution follows professional, production-grade standards with minimal context loading.

---

## When to use

Use when:

* Implementing or modifying C++ code
* Designing system architecture or modules
* Working with DLLs, ABI, or packaging
* Building interop layers (FFI, Kotlin/native, C API)
* Debugging, profiling, or optimizing
* Writing tests or improving quality
* Performing authorized instrumentation or runtime work

---

## When NOT to use

Do NOT use when:

* Working purely in non-C++ domains
* Performing high-level planning without implementation
* Doing unrelated scripting or tooling tasks

---

## Inputs

* Task description (required)
* Relevant code or modules (optional but recommended)
* Constraints:

  * platform
  * compiler/toolchain
  * performance requirements
  * ABI stability requirements

---

## Outputs

Depending on task, must produce:

* Implementation or changes
* Architecture decisions (if applicable)
* Safety and correctness guarantees
* Required tests
* Build/packaging adjustments (if needed)
* Validation steps

---

## Process

### Step 1 — Classify Task

Analyze task and classify into domains:

* Core language / logic
* Architecture / modules
* Memory / lifetime
* Concurrency
* Performance
* Build / packaging
* DLL / ABI
* Interop (FFI / Kotlin / C API)
* Debugging / diagnostics
* Instrumentation (authorized only)
* Testing / quality
* Security

---

### Step 2 — Select Minimal Specialties

#### Core Engineering

* `architecture.md` → system design, boundaries
* `modules.md` → module structure and dependencies
* `language.md` → modern C++ usage
* `memory.md` → ownership, RAII, lifetimes
* `errors.md` → error handling
* `concurrency.md` → threading and sync
* `performance.md` → optimization and profiling

#### Build & Packaging

* `build.md` → build system (CMake-first)
* `packaging.md` → artifacts and distribution
* `dll.md` → shared library design and ABI

#### Interop

* `ffi.md` → foreign function boundaries
* `kotlin-interop.md` → Kotlin/native integration
* `c-api.md` → stable C ABI façade

#### Instrumentation & Runtime (Restricted)

* `hooks.md` → authorized hooks/extensions
* `injection.md` → authorized runtime loading
* `debugging.md` → diagnostics and crash analysis

#### Quality

* `testing.md` → test strategy and coverage
* `api-design.md` → public API design
* `logging.md` → logging and telemetry
* `security.md` → secure coding

---

### Step 3 — Apply Routing Rules

Load only what is required:

* DLL work
  → `dll.md`, `c-api.md`, `build.md`, `testing.md`

* Kotlin interop
  → `kotlin-interop.md`, `ffi.md`, `c-api.md`, `dll.md`

* Memory/lifetime issue
  → `memory.md`, `debugging.md`, `testing.md`

* Performance issue
  → `performance.md`, `concurrency.md`, `debugging.md`

* Architecture change
  → `architecture.md`, `modules.md`, `api-design.md`

* Build/system issue
  → `build.md`, `packaging.md`, `debugging.md`

* Authorized instrumentation
  → `hooks.md`, `security.md`, `testing.md`, `debugging.md`

---

### Step 4 — Execute Task

Follow deterministic workflow:

1. Understand requirements and constraints
2. Identify risks (ABI, memory, concurrency, performance)
3. Apply selected specialty rules
4. Implement or modify code
5. Ensure correctness (compile-time + runtime reasoning)
6. Add or update tests
7. Validate build and integration points

---

### Step 5 — Validate

Ensure:

* No undefined behavior introduced
* Ownership and lifetimes are correct
* ABI is stable (if applicable)
* Thread safety is maintained
* Performance constraints are respected
* Tests cover critical paths
* Build remains reproducible

---

## Constraints

Must:

* Load minimal specialties only
* Prefer RAII and deterministic ownership
* Maintain ABI stability when required
* Keep interop boundaries explicit and safe

Must NOT:

* Introduce undefined behavior
* Leak memory or resources
* Break ABI unintentionally
* Add hidden global state
* Use unsafe runtime manipulation outside authorized scope

---

## Security & Instrumentation Restrictions

Disallowed:

* stealth persistence
* evasion techniques
* credential access or bypass
* unauthorized process manipulation
* abuse-oriented hooking/injection

Allowed ONLY if explicitly authorized:

* internal tooling
* owned software
* debugging environments
* lab/testing scenarios
* observability/instrumentation

---

## Acceptance Criteria

Task is complete only if:

* Correct specialties were selected (minimal set)
* Implementation compiles and is logically correct
* Memory and lifetime rules are respected
* Concurrency (if present) is safe
* ABI/contracts are preserved or intentionally updated
* Tests are added or updated where required
* Build and integration are validated

---

## Key Principle

> Load only the knowledge required to safely and correctly complete the task.
