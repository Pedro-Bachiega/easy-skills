# Hooks (Authorized Instrumentation Only)

Defines the rules for implementing hooks in controlled, authorized environments.

## Scope

This file covers:
- in-process extension points
- sanctioned interception for debugging or testing
- compatibility instrumentation in owned software
- wrapper/adaptor hook design
- safe validation and rollback expectations

This file does NOT support:
- covert tampering
- stealthy interception
- bypassing protections
- third-party abuse

## Preferred Order of Approaches

Use these in order of preference:
1. official plugin or callback APIs
2. compile-time instrumentation
3. documented wrapper/interposition points
4. explicit test-only hook seams
5. tightly scoped in-process hooks in owned/lab scenarios

## Rules

- prefer supported extension points over binary patching
- document target version assumptions
- make enable/disable behavior explicit
- provide rollback/cleanup logic
- validate on exact owned test targets
- isolate hook logic from core business logic
- log activation and failure paths in debug builds

## Design Guidance

A hook-related component should define:
- target scope
- supported versions/builds
- activation conditions
- safety checks
- cleanup/unhook path
- test coverage expectations

## Testing

Authorized hook work must include:
- activation tests
- non-activation tests
- rollback/unhook tests
- crash regression tests
- version mismatch behavior tests

## Safer Alternative

Prefer adding official extension seams in the owned target rather than maintaining brittle runtime interception.
