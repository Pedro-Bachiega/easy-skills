# Concurrency Rules

Defines threading and synchronization guidance.

## Core Principle

> Concurrency must be explicit in ownership, scheduling, and synchronization.

## Rules

- define thread-affinity of objects when relevant
- isolate mutable shared state
- prefer message passing or task ownership when practical
- minimize lock scope
- document shutdown behavior
- design cancellation intentionally

## Allowed

- worker pools
- futures/promises where appropriate
- atomics for simple synchronization
- lock-based protection where ownership is clear

## Avoid

- ad hoc detached threads
- hidden background work
- data races by convention
- callbacks with ambiguous thread context
- blocking foreign UI threads accidentally during interop

## Testing

Every concurrency-sensitive component should have:
- determinism strategy where possible
- stress tests
- shutdown tests
- race-focused diagnostics
