# Security Review

Reviews trust boundaries, unsafe operations, and misuse risk.

## Check
- are inputs validated
- are dangerous capabilities constrained
- is the code safe for its intended environment
- are privilege boundaries respected
- is boundary misuse possible through API ambiguity

## Flag
- unsafe default behavior
- hidden dangerous capability
- buffer misuse
- unchecked casts at boundaries
- unsafe runtime modification without clear authorization scope
- code that would meaningfully enable unauthorized tampering

## Special Rule
For any runtime instrumentation, hooks, or loading behavior:
- ensure scope is explicitly authorized
- ensure behavior is reversible and testable
- ensure there is no stealth, concealment, or abuse-oriented design
