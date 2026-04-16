# C++ Review

Reviews general C++ correctness and maintainability.

## Check
- clear ownership intent
- RAII use
- exception safety consistent with project policy
- no avoidable raw owning pointers
- readable control flow
- narrow interfaces
- compiler/runtime assumptions not hidden

## Flag
- ambiguous ownership
- weak teardown behavior
- hidden lifetime coupling
- unsafe casts without strong justification
- global mutable state without control
- template or macro complexity without payoff
