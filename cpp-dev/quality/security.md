# Security and Hardening

Defines secure coding and release rules.

## Core Principle

> Native code must assume misuse, malformed input, and boundary failure are possible.

## Rules

- validate all external inputs
- treat handles as untrusted at the boundary
- constrain unsafe operations
- avoid buffer overflows and integer overflow assumptions
- isolate privileged operations
- prefer least-privilege execution
- document dangerous capabilities clearly

## For Runtime Instrumentation Work

Any hooking or injection-related work must be limited to:
- owned software
- internal QA/lab environments
- explicit customer or employer authorization

Do not design for:
- stealth
- evasion
- bypassing third-party protections
- persistence
- concealment
