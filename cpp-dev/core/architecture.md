# Architecture Rules

Defines system-wide architectural constraints for professional C++ projects.

## Layers

Recommended layers:
1. Public API
2. Application / orchestration
3. Domain / core logic
4. Infrastructure / OS / external integrations
5. Diagnostics / tooling

## Rules

- Keep domain logic independent from UI, transport, and platform details.
- Separate public interfaces from implementation details.
- Prefer explicit ownership boundaries.
- Design for testability first.
- Keep OS-specific code isolated.
- Avoid global mutable state.
- Make threading and lifetime boundaries obvious.

## Allowed

- RAII-based ownership
- dependency inversion
- narrow public APIs
- pImpl when ABI stability matters
- C façade over C++ internals when cross-language stability matters

## Forbidden

- hidden ownership transfer
- ambiguous thread-affinity
- exceptions crossing unsafe FFI boundaries
- unstable C++ ABI exposure to foreign languages
