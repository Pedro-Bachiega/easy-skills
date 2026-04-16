# DLL / Shared Library Development

Defines how shared libraries should be designed, exported, and tested.

## Purpose

Support professional development of shared libraries for:
- internal modularization
- plugin-like extension boundaries
- foreign language integration
- reusable native components

## Export Rules

- expose the smallest public surface possible
- prefer explicit export macros
- separate public and private headers
- avoid exposing template-heavy unstable ABI as the main foreign-facing surface
- prefer a thin stable façade over complex internal types

## ABI Stability

When a library is consumed outside the exact same compiler/runtime environment:
- prefer a C ABI façade
- avoid exporting STL containers directly
- avoid exceptions across the boundary
- avoid ownership ambiguity
- use opaque handles where useful

## Public Surface Design

Public DLL APIs should favor:
- explicit initialization/shutdown
- opaque handles
- caller-provided buffers or length-query patterns
- clear destroy/release functions
- explicit version query functions

## Memory Boundary Rule

Do not assume the caller can free memory allocated by the DLL safely unless the API explicitly defines how.

## Threading Rule

Document:
- whether calls are thread-safe
- whether handles are thread-safe
- whether initialization is global or per-instance

## Testing Requirements

Every DLL should have:
- load/unload tests
- version compatibility tests
- exported symbol verification
- boundary error tests
- ownership tests
- integration tests from at least one external consumer
