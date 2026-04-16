# Kotlin Interop

Defines how Kotlin should integrate with the native library safely and maintainably.

## Purpose

Support Kotlin/JVM or Kotlin-based application layers consuming native code through a stable boundary.

## Default Strategy

Use:
- a stable C ABI in the native library
- a small JVM-facing wrapper layer
- explicit type conversion at the boundary
- generated or carefully maintained bindings

Do not expose raw C++ ABI directly to Kotlin.

## Architecture

Recommended layers:
1. native C++ implementation
2. C ABI façade
3. Kotlin/JVM binding layer
4. Kotlin-friendly wrapper API

## Rules

- keep Kotlin-facing APIs idiomatic and small
- convert strings, arrays, and errors at the wrapper edge
- map native handles to safe wrapper objects
- ensure release/close semantics are explicit
- avoid hidden native resource leaks

## Threading

Document:
- which calls may block
- whether the native layer is thread-safe
- whether callbacks can occur on native worker threads
- how Kotlin callers should coordinate shutdown

## Error Handling

Prefer:
- native status codes
- structured error retrieval
- Kotlin exceptions created in the Kotlin wrapper layer if desired

Do not let native exceptions cross the boundary.

## Testing

Interop testing must include:
- load tests from Kotlin
- smoke tests for create/use/destroy
- error path tests
- string and buffer encoding tests
- concurrency tests when the library is multi-threaded
