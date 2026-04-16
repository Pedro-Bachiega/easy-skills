# FFI Review

Reviews foreign-function boundaries.

## Check
- simple stable external types
- string encoding rules clear
- buffer sizing rules explicit
- handle ownership explicit
- error reporting explicit
- callbacks documented carefully
- boundary coarse-grained enough

## Flag
- chatty boundary design
- unclear ownership
- implicit encoding assumptions
- callbacks with unclear thread context
- native exceptions or complex C++ types leaking across the boundary
