# Packaging and Distribution

Defines artifact packaging rules.

## Responsibilities

- release artifact layout
- symbol management
- runtime dependencies
- versioning and compatibility
- distribution testing

## DLL Packaging Rules

Ship with:
- the DLL/shared library
- import library if needed
- public headers
- version metadata
- debug symbols or symbol server strategy as appropriate
- runtime dependency documentation

## Versioning

Public artifacts must define:
- semantic versioning or equivalent compatibility policy
- ABI compatibility expectations
- deprecation rules

## Do Not

- change public ABI casually
- ship undocumented runtime prerequisites
- expose unstable internal headers as public API
