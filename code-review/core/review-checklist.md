# Universal Review Checklist

Use this checklist for every PR.

## Correctness
- does the code do what it claims
- are edge cases considered
- are failure paths handled
- is behavior consistent with the existing architecture

## Scope Control
- is the change too broad
- are unrelated refactors mixed in
- can reviewers reason about the change safely

## Readability
- are names clear
- are responsibilities obvious
- is control flow understandable
- are abstractions justified

## Maintainability
- does this reduce or increase coupling
- does it introduce hidden assumptions
- is there duplication that should be centralized

## Safety
- are trust boundaries explicit
- are inputs validated
- are ownership/lifetime rules safe
- are risky operations constrained

## Testing
- are tests present
- do tests cover the real risk
- are boundary and failure cases covered
- is integration validation needed

## Documentation
- should public behavior be documented
- should versioning, ABI, or migration notes be updated
