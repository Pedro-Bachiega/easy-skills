# Build System Guidance

This file defines the build strategy.

## Default

Use CMake as the primary build system unless the project has an explicit alternative requirement.

## Rules

- define targets explicitly
- keep target ownership clear
- separate public include directories from private ones
- centralize compiler warnings and baseline options
- treat build flags as part of project architecture

## Build Output Types

- static libraries
- shared libraries / DLLs
- executables
- tests
- tooling binaries

## Professional Defaults

- enable strong warnings
- use separate debug and release profiles
- produce debug symbols
- isolate platform-specific flags
- keep generated files out of source layout

## ABI Considerations

- document compiler/runtime assumptions
- test release artifact compatibility
- avoid accidental ABI drift in exported interfaces
