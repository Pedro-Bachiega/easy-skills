# Logging and Telemetry

Defines logging guidance.

## Rules

- logging must support debugging without destabilizing hot paths
- keep logging category-based
- ensure logs across DLL boundaries are understandable
- do not log secrets
- make diagnostic verbosity configurable

## Boundary Guidance

For libraries:
- do not assume host logging backend
- provide callback or adapter-based logging integration when needed
- allow host-controlled verbosity
