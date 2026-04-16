# Performance Rules

This file defines the performance mindset and constraints.

## Core Principle

> Measure first. Optimize second. Preserve correctness always.

## Rules

- profile before optimizing
- optimize hot paths, not guesses
- avoid premature complexity
- make cost visible in APIs
- treat allocation, copies, synchronization, and crossing ABI boundaries as measurable costs

## Areas to Watch

- heap churn
- string conversions
- lock contention
- thread oversubscription
- unnecessary virtual dispatch in critical paths
- boundary marshalling between languages

## DLL / Interop Performance

- minimize conversion churn across boundaries
- prefer coarse-grained calls over chatty FFI
- keep ABI payloads simple and stable
- batch where practical
