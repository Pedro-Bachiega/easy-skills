# C ABI Façade Design

Defines how to create a stable native interface for foreign consumers.

## Purpose

A C ABI façade is the preferred boundary when:
- another language consumes the library
- ABI stability matters
- compiler/runtime mismatch risk exists
- exceptions and templates should stay internal

## Design Rules

- use plain structs with explicit layout only when safe
- otherwise use opaque handles
- expose create/destroy pairs
- use explicit status codes
- pass buffer + size pairs
- include version and feature query functions
- define UTF-8 string policy clearly

## Avoid

- exposing STL types
- exposing exceptions
- returning ownership ambiguously
- exporting class hierarchies as the primary interop boundary

## Testing

- compile consumer smoke tests
- validate structure layout assumptions
- verify error paths and invalid handle behavior
