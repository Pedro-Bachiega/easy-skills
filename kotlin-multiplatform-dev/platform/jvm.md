# JVM Target

## Responsibilities

* desktop app host or server entrypoint
* filesystem access
* process execution

## Rules

* isolate runtime-specific logic
* reuse shared logic whenever possible

## Source Set

* jvmMain
* jvmTest

## Examples

* file IO
* CLI tools
* local caching

## Exclusion

UI rules → @compose-ui.md
