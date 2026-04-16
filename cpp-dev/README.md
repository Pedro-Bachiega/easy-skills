# C++ Development Skill (Router)

This file is the entry point and router for the C++ development skill system.

The skill is split into focused specialty files so each task can load only the minimum context required.

## Purpose

This skill supports professional C++ development across:
- core language usage
- project architecture
- libraries and DLLs
- interop with other languages such as Kotlin
- testing
- diagnostics
- build systems
- performance
- authorized instrumentation and hooking in controlled environments

## Core Principle

> Modules of knowledge must be split by responsibility.
> Load only the specialty files required for the task.

---

## Routing Map

### Core Engineering
- @architecture.md → system design, layering, ownership, boundaries
- @modules.md → codebase/module structure and dependency rules
- @language.md → modern C++ language rules and idioms
- @memory.md → ownership, RAII, lifetimes, allocation strategy
- @errors.md → error handling strategy
- @concurrency.md → threads, synchronization, task execution
- @performance.md → profiling mindset and performance rules

### Build & Packaging
- @build.md → build system guidance (CMake-first)
- @packaging.md → artifacts, distribution, symbols, ABI concerns
- @dll.md → shared library / DLL design and export rules

### Interop
- @ffi.md → FFI design for external consumers
- @kotlin-interop.md → Kotlin/JVM integration with native libraries
- @c-api.md → stable C ABI façade design

### Instrumentation & Controlled Runtime Modification
- @hooks.md → authorized in-process hooks and extension boundaries
- @injection.md → authorized runtime loading/injection boundaries for owned software and lab use only
- @debugging.md → debugging, symbols, crash analysis, diagnostics

### Quality
- @testing.md → unit, integration, ABI, fuzz, and system testing
- @api-design.md → public API design rules
- @logging.md → logging and telemetry guidance
- @security.md → secure coding and hardening guidance

---

## Restrictions

This skill does not support:
- stealthy persistence
- evasion
- credential theft
- unauthorized process tampering
- abuse-oriented hooking or injection
- bypassing protections on third-party systems

Any hooking or injection work must be limited to:
- software you own
- software you are explicitly authorized to assess
- internal tooling
- local debugging labs
- compatibility testing
- sanctioned observability/instrumentation

---

## Context Loading Rule

Load only the needed specialties.

Examples:
- exporting a DLL → `dll.md`, `c-api.md`, `build.md`, `testing.md`
- Kotlin integration → `kotlin-interop.md`, `ffi.md`, `c-api.md`, `dll.md`
- memory bug → `memory.md`, `debugging.md`, `testing.md`
- performance issue → `performance.md`, `concurrency.md`, `debugging.md`
- controlled hook in owned process → `hooks.md`, `security.md`, `testing.md`, `debugging.md`

Do not load the entire skill unless the task truly spans multiple specialties.
