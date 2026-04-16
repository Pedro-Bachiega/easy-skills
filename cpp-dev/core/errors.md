# Error Handling Strategy

Defines how errors are represented and propagated.

## Default Policy

Use one clear project-wide strategy and keep it consistent.

Possible strategies:
- exceptions internally, translated at boundaries
- status/result types across critical boundaries
- error codes for C ABI and FFI surfaces

## Rules

- never let C++ exceptions cross a C ABI boundary
- never let implementation-specific exception types leak across foreign language boundaries
- preserve actionable diagnostics
- include error category and context
- fail fast on impossible states where appropriate

## Boundary Rules

### Public C++ API
- may use exceptions if the project standard allows it

### C ABI / DLL export for foreign consumers
- use explicit status codes
- expose error retrieval APIs or structured error payloads
- document ownership of returned error details

### Internal infrastructure
- may use exceptions or result types consistently
