# FFI Strategy

Defines foreign-function interface rules for consuming C++ from other languages.

## Core Principle

> Prefer a narrow, stable boundary with simple types.

## Rules

- keep the boundary coarse-grained
- use C ABI as the stable external contract
- convert language-specific data at the edge
- document ownership, encoding, threading, and lifetime rules
- avoid callback designs unless necessary and well-defined

## Boundary Checklist

Every FFI surface must document:
- initialization model
- shutdown model
- handle ownership
- string encoding
- thread safety
- callback thread context
- error reporting
- versioning expectations

## Avoid

- leaking internal type system details
- returning pointers with unclear lifetime
- exposing implementation-specific allocators
- large numbers of chatty fine-grained calls
