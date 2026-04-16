# Module Structure

This file defines the module strategy for a Kotlin Multiplatform professional project.

It establishes:
- a minimal but complete base module set
- strict separation of concerns
- scalability rules for future growth
- correct use of source sets vs modules

---

## Core Principle

> Modules define responsibilities.
> Source sets define platform differences.

---

## Mandatory Base Modules

Every project using this skill should start with the following modules:

### Core (Business & Logic)

- `:core:domain`
- `:core:usecases`
- `:core:state`

### Data & Infrastructure

- `:core:data` *(optional but recommended aggregator)*
- `:core:network`
- `:core:storage`

### UI

- `:ui:designsystem`
- `:ui:components`
- `:ui:screens`
- `:ui:navigation`

### Application (Platform-specific entrypoints)

- `:app:android`
- `:app:desktop` (or `:app:jvm`)
- `:app:ios`

---

## Responsibility of Each Base Module

### `:core:domain`
- business rules
- entities and value objects
- pure logic only

### `:core:usecases`
- orchestration of domain logic
- application-level actions

### `:core:state`
- UI-facing state models
- state holders and transformations

---

### `:core:network`
- API definitions
- HTTP abstractions
- request/response mapping

### `:core:storage`
- persistence interfaces
- caching strategies

### `:core:data`
- optional aggregation layer
- combines network + storage when needed
- repository implementations

---

### `:ui:designsystem`
- theme
- tokens (colors, spacing, typography)
- base UI primitives

### `:ui:components`
- reusable UI components
- no feature-specific logic

### `:ui:screens`
- feature screens
- screen composition

### `:ui:navigation`
- navigation graph
- route definitions

---

### `:app:*`
- platform entrypoints
- app startup
- dependency wiring
- host integration

---

## Platform Rule (Strict)

Platform-specific modules are NOT allowed except for application modules.

❌ Do NOT create:
- `:platform:android`
- `:platform:jvm`
- `:platform:ios`
- `:feature:foo:android`

✅ Instead:
- use `androidMain`, `jvmMain`, `iosMain` inside shared modules

---

## Source Set Strategy

Each shared module must use source sets for platform specialization:

```text
module/
└── src/
    ├── commonMain/
    ├── commonTest/
    ├── androidMain/
    ├── jvmMain/
    └── iosMain/
