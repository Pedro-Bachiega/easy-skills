# Runtime Loading / Injection (Authorized Lab Use Only)

Defines the policy and engineering constraints for runtime loading or injection work in controlled environments.

## Scope

This file is limited to:
- owned-process debugging labs
- internal QA instrumentation
- compatibility validation
- sanctioned runtime observability experiments
- explicit customer/employer-approved assessment environments

It does NOT support unauthorized deployment or stealth.

## Preferred Alternatives

Before any runtime injection approach, prefer:
1. official plugin systems
2. command-line feature flags
3. environment-configured loading
4. test harness integration
5. debug-only loader seams

Only consider runtime injection when no safer supported extension point exists and authorization is explicit.

## Engineering Rules

- scope to exact owned target versions
- keep payload narrow and reversible
- require explicit operator intent
- document environment assumptions
- separate loader concerns from payload concerns
- design cleanup and shutdown paths
- log success/failure in lab builds
- test only in isolated environments

## Boundary Rules

- do not embed unrelated business logic in injected components
- keep instrumentation small
- avoid persistent modifications
- do not attempt concealment
- do not bypass protections

## Testing

Required:
- environment validation tests
- load/unload tests where supported
- process stability tests
- version compatibility tests
- negative tests for unsupported targets

## Safe Usage Standard

If an official extension mechanism can solve the problem, use that instead.
