# Memory and Lifetime Rules

This file defines ownership, lifetime, and allocation strategy.

## Core Principle

> Every resource must have one obvious owner and one obvious release path.

## Defaults

- prefer RAII
- prefer stack allocation when practical
- use smart pointers to express ownership clearly
- use references or observer pointers for non-owning access
- document lifetime dependencies explicitly

## Ownership Rules

- `std::unique_ptr` for exclusive ownership
- `std::shared_ptr` only when shared lifetime is truly required
- raw pointers are non-owning by default
- references imply non-null borrowed access
- avoid storing borrowed pointers beyond their valid lifetime

## DLL / FFI Boundary Rule

Do not allocate in one binary boundary and require deallocation in another unless the contract is explicitly designed and tested for that.

Prefer:
- caller-allocated buffers with size reporting
- opaque handles with matching destroy functions
- ownership-preserving wrapper APIs

## Allocation Strategy

- optimize allocation only after measuring
- isolate custom allocators where justified
- avoid hidden heap churn in hot paths
- treat allocator choice as architecture, not convenience

## Forbidden

- ambiguous ownership
- mixed manual/free store patterns without reason
- leaked handles
- freeing resources in a different ownership domain accidentally
