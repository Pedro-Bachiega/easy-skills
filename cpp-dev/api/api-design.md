# API Design Rules

Defines public API quality standards.

## Principles

- small surface
- obvious ownership
- obvious error behavior
- obvious threading behavior
- hard to misuse

## Public API Should

- separate setup from usage
- separate construction from configuration when useful
- prefer explicit names
- expose version and capability queries when compatibility matters
- remain stable across minor releases where promised

## Public API Should Not

- expose internal implementation details
- assume hidden global state
- require consumer knowledge of internal scheduling
- depend on unspecified call order unless documented
