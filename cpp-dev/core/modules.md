# Module Structure

This file defines the code organization strategy for a scalable C++ project.

## Core Principle

> Modules separate responsibilities.
> Platform differences and compiler-specific details should not dominate module boundaries.

## Mandatory Base Modules

Every professional project should start with these base modules or their equivalent:

### Core
- `core/domain`
- `core/runtime`
- `core/utils`

### Interfaces
- `api/public`
- `api/internal` (optional)

### Infrastructure
- `infra/platform`
- `infra/io`
- `infra/logging`

### Libraries / Packaging
- `lib/shared` or `lib/dll`
- `lib/static` when applicable

### Quality
- `tests/unit`
- `tests/integration`
- `tests/system`

These are the base modules, not a final limit.

---

## Responsibility of Each Base Module

### `core/domain`
- core rules
- business or engine logic
- pure logic where possible

### `core/runtime`
- lifecycle orchestration
- execution flow
- component wiring not tied to packaging

### `core/utils`
- small shared helpers only
- must not become a dumping ground

### `api/public`
- exported headers
- stable contracts
- public-facing data types

### `infra/platform`
- OS-specific adapters
- process, file, threading, timing, handles

### `infra/io`
- filesystem, streams, sockets if not split further

### `infra/logging`
- telemetry sinks
- logging abstraction
- diagnostics integration

### `lib/shared` / `lib/dll`
- shared library packaging boundary
- exports and loader-facing shape

### `tests/*`
- verification by test type

---

## Scaling Rules

Create more modules only when:
- responsibility is clearly distinct
- ownership is clearer
- build isolation helps
- API surface deserves a separate boundary
- testing and release management improve

Examples of valid additional modules:
- `core/math`
- `core/serialization`
- `infra/network`
- `infra/db`
- `interop/c`
- `interop/kotlin`
- `tooling/debug`
- `tooling/profiler`

Do not create modules just to mirror folders or tiny helpers.

---

## Dependency Direction

Preferred direction:

`app/tool -> api/public -> core -> infra`

or

`tests -> api/public/core/infra`

Rules:
- public API depends inward, not the reverse
- infra should not own domain logic
- testing modules may depend on all required layers
- interop façades should stay thin

---

## Professional Default Standard

- narrow modules
- obvious public/private boundaries
- platform and compiler specifics isolated
- dedicated interop façade when crossing language boundaries
- dedicated tests by layer and artifact type
