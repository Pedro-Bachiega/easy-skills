# Modern C++ Language Rules

This file defines the default language rules for professional C++ development.

## Standard

Default to a modern C++ standard supported by the project baseline.
Prefer a single project-wide standard target.

## Style Principles

- prefer clarity over cleverness
- keep object lifetimes obvious
- avoid macro-heavy design unless required
- use constexpr where it improves correctness or clarity
- prefer standard library facilities before custom utilities

## Defaults

- use `std::string_view` for non-owning string parameters when safe
- use `std::span` for non-owning contiguous ranges when available
- use `enum class`
- use `override`
- use `noexcept` intentionally, not mechanically
- prefer `using` over `typedef`
- prefer range-based and algorithmic style where readable

## Avoid

- raw owning pointers
- implicit ownership transfer
- unchecked narrowing
- surprise copies in hot paths
- exceptions across FFI boundaries
- exposing STL-heavy APIs across unstable ABI boundaries

## Templates

Use templates when they:
- reduce duplication meaningfully
- improve performance with clear benefit
- express generic constraints well

Avoid template metaprogramming that harms maintainability without strong payoff.
