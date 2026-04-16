# Testing Strategy

## Responsibilities

* test coverage for shared Kotlin behavior
* regression safety for business and state changes
* validation of platform-specific boundaries when needed
* screenshot coverage for relevant Compose components and screen states
* unit coverage for pure logic
* jvm related targets only: unit coverage for UI behavior, using junit4 compose rule and assertions
* android only: instrumented coverage for UI behavior, using Robolectric or equivalent when appropriate

## Rules

* test shared logic in common code when possible
* cover failure paths, not just happy paths
* use screenshot tests for important visual states, variants, and regressions
* jvm related targets only: unit tests with compose rule for UI behavior, interactions, and host integration
* android only: use instrumented tests for UI behavior, interactions, and host integration
* keep unit tests focused on pure logic and deterministic transformations
* add boundary tests when source sets or platform adapters change
* load only the row that matches the change you are testing
* prefer unit tests for logic, screenshot tests for visuals, and instrumented tests for behavior
* when validating Android instrumented tests, run `connectedDebugAndroidTest`
* add boundary coverage when the change crosses a source set, platform adapter, or UI host boundary

## Focus Areas

* state holders and reducers
* use case orchestration
* presentation logic and reducers in unit tests
* platform adapter behavior
* serialization and storage edges
* Compose UI loading, empty, and error states
* component variants, theming, and stateful layout regressions in screenshot tests

---

## Testing Matrix

Use the smallest test type that proves the behavior.

| Test type | Use when | Typical scope | Do not use for |
| --- | --- | --- | --- |
| Unit | Logic is pure and deterministic | reducers, mappers, validators, state derivations | rendering, semantics, host integration |
| Screenshot | Visual output or layout is important | screen states, component variants, theming, regressions | business logic, interaction behavior, platform wiring |
| Instrumented (or compose rule emulating instrumentation) | Behavior depends on Compose runtime or host integration | clicks, input, semantics, navigation triggers, lifecycle behavior | pure logic that can be tested faster in unit tests |
| Robolectric or equivalent | Android host behavior needs a lighter-weight environment | framework integration, lifecycle-sensitive behavior, Android-specific state | cross-platform UI rendering or pure logic |
