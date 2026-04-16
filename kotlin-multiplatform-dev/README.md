# Kotlin Multiplatform Skill (Router)

This file acts as the entry point and router for the Kotlin Multiplatform skill system.

Each concern is isolated into its own markdown file so we can minimize context size, improve clarity, and let each domain evolve independently.

## Core Principle

> Every file must do one thing well and assume nothing outside its scope.

---

## Skill Routing Map

### Core Architecture

* `core/architecture.md` -> global rules, layering, boundaries
* `core/modules.md` -> module structure and dependency graph
* `core/common.md` -> shared code rules (`commonMain`)

### Business Logic

* `business/domain.md` -> domain models and rules
* `business/usecases.md` -> application and business use cases
* `business/state.md` -> shared state management

### Infrastructure

* `data/network.md` -> networking layer
* `data/storage.md` -> persistence layer
* `data/serialization.md` -> data formats and parsing

### Platform Targets

* `platform/android.md` -> Android-specific implementation
* `platform/jvm.md` -> JVM, desktop, or server implementation
* `platform/ios.md` -> iOS integration and interop

### Platform Abstractions

* `platform/expect-actual.md` -> expect/actual strategy
* `platform/platform-services.md` -> permissions, sensors, and OS APIs

### Quality

* `quality/testing.md` -> test coverage, validation, and regression safety
* `quality/security.md` -> trust boundaries, unsafe inputs, and misuse risk

### UI (separate system)

* `ui/compose-ui.md` -> Compose UI rules, loaded separately when working on UI

---

## Rules for All Specialties

1. No file should exceed its responsibility.
2. No file should redefine rules from another file.
3. Prefer referencing over duplication.
4. Shared logic always lives in common code unless impossible.
5. UI is always a consumer, never a source of business logic.

---

## Execution Strategy

When working on a task:

1. Start from this file.
2. Identify the relevant specialties.
3. Load only those files.
4. Never load the entire system unless absolutely necessary.

---

## Explicit Exclusion

Compose UI rules are not defined here.

They must be implemented in:

* `ui/compose-ui.md`
