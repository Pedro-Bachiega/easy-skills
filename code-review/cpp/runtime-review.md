# Runtime Instrumentation Review

Reviews authorized runtime instrumentation, hooks, or controlled runtime loading code.

## Scope

This review file applies only to:
- owned software
- internal tooling
- authorized lab/testing environments
- compatibility instrumentation
- debugging and observability use

## Check
- is the scope explicitly authorized
- is there a safer supported extension point instead
- is activation explicit
- is cleanup/unhook behavior present
- are version assumptions constrained
- are tests proving non-target and rollback behavior present
- is the design free of stealth or concealment goals

## Flag
- unclear authorization scope
- irreversible behavior
- lack of rollback or cleanup
- no version or environment checks
- design choices that materially enable unauthorized tampering
