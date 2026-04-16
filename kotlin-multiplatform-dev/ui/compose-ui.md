# Compose UI Specialty

This file defines the Compose UI specialty for a Kotlin Multiplatform professional project.

It is intentionally limited to UI concerns and should be loaded only when working on:
- screens
- UI components
- design system implementation
- UI state consumption
- navigation rendering
- user interaction handling in the presentation layer

It must NOT be used as the source of truth for:
- business rules
- domain modeling
- networking
- persistence
- platform service design
- cross-platform architecture rules

Those concerns belong to their own specialty files.

---

## Purpose

The Compose UI specialty defines how UI is structured, composed, and connected to presentation state in a Kotlin Multiplatform application using Compose.

Its goals are:
- minimal UI-specific context
- predictable screen structure
- consistency across targets
- easy reuse of components
- strict separation between UI and business logic
- support for Android, JVM, and iOS Compose hosts where applicable

---

## Scope

This file covers:
- UI structure
- screen composition
- component hierarchy
- state rendering
- event forwarding
- local UI state
- theming structure
- previews
- accessibility expectations at the component level
- navigation rendering conventions
- Compose-specific performance and maintainability rules

This file does NOT define:
- domain behavior
- use case orchestration
- repository logic
- networking
- persistence
- platform APIs outside UI host integration

---

## References

This specialty should be used together with:
- `README.md`
- `core/architecture.md`
- `business/state.md`
- `business/usecases.md`
- `platform/android.md`
- `platform/jvm.md`
- `platform/ios.md`

It must not duplicate their responsibilities.

---

## Core UI Principles

1. UI is a renderer of state, not the owner of business rules.
2. UI emits intents/events upward and renders state downward.
3. Screens coordinate sections and components; components remain focused and reusable.
4. State exposed to UI must already be prepared for rendering.
5. UI-specific derivation is allowed only when it is trivial and presentation-only.
6. UI should remain deterministic for a given input state.
7. Components should be stateless by default and stateful only when local UI interaction requires it.
8. Navigation should be treated as UI flow, not domain logic.
9. Compose code should optimize for readability, stability, and recomposition safety.
10. Platform-specific UI differences must be isolated and minimal.

---

## UI Layer Responsibilities

The Compose UI layer is responsible for:
- rendering screens and widgets
- displaying state from presentation/state holders
- collecting user input
- forwarding UI events
- handling transient visual state
- rendering navigation destinations
- applying design tokens and themes
- supporting accessibility semantics
- ensuring adaptive layouts when required

It is NOT responsible for:
- deciding business rules
- directly calling infrastructure code from composables
- storing app logic in composables
- embedding platform services into reusable UI components
- mutating domain state directly

---

## Recommended UI Module Boundaries

When Compose is present, prefer separating UI modules from non-UI modules.

Recommended structure:

- `:ui:designsystem` → theme, tokens, reusable primitives
- `:ui:components` → reusable composite components
- `:ui:screens` → screen-level implementations
- `:ui:navigation` → navigation graph and route rendering
- `:presentation` or `:core:state` → screen state contracts and event handlers

Rules:
- UI modules may depend on presentation/state contracts.
- UI modules must not depend directly on data/infrastructure modules.
- Design system modules must stay free of feature-specific business logic.
- Feature screens should consume stable state models and callbacks.

---

## Source Set Strategy

Compose UI rules apply to whichever targets are using Compose as the UI technology.

Typical placement:
- shared Compose UI in `commonMain`
- platform host integration in platform source sets
- platform-only visual adaptations only when necessary

Use shared UI in `commonMain` for:
- screens
- reusable components
- theme definitions
- screen content
- navigation rendering abstractions where possible

Use platform source sets for:
- app bootstrap
- host container setup
- platform window or activity integration
- platform-specific system UI integration
- platform-specific interop wrappers needed by UI

Avoid moving UI into platform source sets unless there is a concrete platform requirement.

---

## Screen Structure

Each screen should be split into explicit layers.

Recommended screen structure:
1. Route
2. Screen
3. Content
4. Section
5. Reusable component

### Route

The route is responsible for:
- obtaining screen state from the presentation layer
- collecting lifecycle-aware state where platform integration requires it
- wiring callbacks
- triggering navigation callbacks

The route should not:
- contain layout complexity
- contain business rules
- directly perform infrastructure operations

### Screen

The screen is responsible for:
- orchestrating major layout regions
- passing state to content
- handling top-level UI event wiring

The screen should:
- remain easy to scan
- avoid deep business branching
- focus on composition

### Content

The content layer is responsible for:
- rendering the main screen body
- grouping sections
- converting screen state into visual layout

### Section

Sections are medium-granularity building blocks:
- headers
- lists
- forms
- summaries
- toolbars
- state banners

### Reusable Component

Reusable components are:
- buttons
- cards
- chips
- rows
- placeholders
- inputs
- dialogs
- visual indicators

---

## Naming Conventions

Use explicit Compose naming.

Recommended conventions:
- `FeatureRoute`
- `FeatureScreen`
- `FeatureContent`
- `FeatureSection`
- `FeatureCard`
- `FeatureItemRow`
- `FeatureDialog`

For screen contracts:
- `FeatureUiState`
- `FeatureUiEvent`
- `FeatureUiAction` if needed
- `FeatureUiEffect` only when one-off effects are unavoidable

For previews:
- `FeatureScreenPreview`
- `FeatureCardPreview`

Avoid vague names like:
- `Content`
- `Container`
- `Manager`
- `Handler`
- `HelperComposable`

unless they are locally scoped and obvious.

---

## UI State Rules

UI must consume state that is already presentation-ready.

Preferred properties of UI state:
- immutable
- stable in meaning
- explicit
- free from infrastructure details
- easy to preview
- easy to test

### UI State Should Include

- text already selected for display when appropriate
- flags for loading, empty, and error states
- item collections already shaped for rendering
- selection state
- enablement/disablement state
- visibility state for optional UI elements

### UI State Should Not Include

- repositories
- platform objects
- raw DTOs
- database entities unless already mapped for UI
- ambiguous flags without clear meaning
- hidden side effects

### Avoid

- multiple booleans representing mutually exclusive screen modes
- UI needing to compute business rules from raw domain data
- passing nullable state where a sealed UI model is clearer

Preferred alternatives:
- sealed screen state models
- distinct models for content/loading/error
- small, explicit nested state models

---

## UI Events

Compose UI should emit user intent upward through explicit callbacks.

Preferred event styles:
- `onRetry()`
- `onBack()`
- `onItemClick(itemId)`
- `onQueryChange(value)`
- `onSubmit()`

Use typed event objects when the screen is complex, but do not over-abstract simple interactions.

Rules:
- UI events represent user intent, not implementation details.
- UI should not decide how events are handled.
- Event names should describe what the user intended, not what the code does internally.

Good:
- `onRefreshRequested`
- `onProfileSelected`
- `onDismissError`

Bad:
- `onLaunchCoroutine`
- `onCallRepository`
- `onMutateState`

---

## Local UI State

Local UI state is allowed only for presentation-local concerns.

Good uses:
- expanded/collapsed state
- input focus state
- temporary text field state before submission
- dialog open/closed state
- pager/tab selection
- animation toggles
- transient gesture-driven state

Do not use local state for:
- business decisions
- long-lived app data
- cross-screen synchronization
- data fetched from repositories
- anything that must survive across presentation owners unless intentionally hoisted

Rule:
- hoist state when multiple composables need to coordinate on it or when it affects the screen contract.

---

## Stateless First

Default all reusable components to stateless APIs.

Preferred pattern:
- state in parameters
- event callbacks in parameters
- no hidden mutation

Example pattern:
- `checked: Boolean`
- `onCheckedChange: (Boolean) -> Unit`

Use stateful wrappers only when they improve usability and the boundary remains clear.

---

## State Hoisting

State hoisting rules:
- hoist to the lowest common owner
- keep reusable components stateless whenever practical
- do not hoist transient state unnecessarily high
- hoist business-relevant state out of the UI layer

A component should own its own state only when:
- the state is purely visual
- no other component needs to observe it
- no external logic depends on it

---

## Side Effects

Compose side effects must be explicit, minimal, and justified.

Allowed side-effect tools include:
- `LaunchedEffect`
- `DisposableEffect`
- `remember`
- `rememberUpdatedState`
- `derivedStateOf`
- `snapshotFlow` only when truly necessary

Rules:
- never perform uncontrolled work during composition
- key side effects correctly
- side effects should relate to UI lifecycle, not replace application architecture
- avoid using side effects to patch incorrect state design

Use side effects for:
- requesting focus
- collecting one-off UI effects
- reacting to lifecycle-bound events
- controlling animations tied to state changes

Do not use side effects for:
- embedding repository logic in composables
- initiating business workflows directly from leaf components
- bypassing the presentation layer

---

## One-Off Effects

One-off effects should be rare and reserved for UI-triggered transient actions such as:
- snackbars
- toasts
- navigation triggers
- opening external links
- requesting focus
- scrolling to a position

Guidelines:
- keep effects separate from persistent screen state when they are truly one-time
- expose effects through a predictable presentation contract
- collect effects at the route/screen edge, not deep in child components

Do not model persistent state as one-off effects.

---

## Navigation Conventions

Navigation belongs to the UI specialty.

Rules:
- routes represent screen destinations
- navigation arguments should be minimal and stable
- pass identifiers, not large mutable objects
- domain logic must not depend on navigation frameworks

Preferred approach:
- `Route` handles navigation callbacks
- screen state remains navigation-framework agnostic
- destination registration is centralized in a navigation-specific package or module

Avoid:
- embedding navigation library code deep in reusable components
- pushing navigation framework objects into domain or shared business layers
- passing repository-backed objects through navigation

---

## Design System Structure

Use a dedicated design system layer.

Recommended sections:
- theme
- typography
- spacing
- shape
- elevation
- color roles
- icons
- component tokens
- reusable primitives

The design system should:
- centralize visual rules
- reduce duplication
- support platform adaptation when needed
- avoid feature-specific naming

Preferred module/package structure:
- `theme/`
- `tokens/`
- `components/`
- `icons/`
- `foundation/`

Do not place feature-specific business logic in the design system.

---

## Theming Rules

Theme responsibilities:
- define color roles
- define typography scale
- define spacing strategy
- define shapes and elevations
- expose composition locals only when justified

Rules:
- theme tokens must be semantic, not screen-specific
- avoid direct hard-coded values across features
- centralize reusable dimensions and visual constants
- keep theming adaptable for dark/light and platform nuances

Prefer:
- semantic names like `surface`, `onSurface`, `errorContainer`
- spacing tokens such as `spaceXs`, `spaceSm`, `spaceMd`, `spaceLg`

Avoid:
- arbitrary duplicated dp values across files
- feature-specific color names in shared theme layers
- mixing unrelated visual rules in screen files

---

## Component Design Rules

Each component should:
- have a clear responsibility
- expose a small API
- support previewable sample data
- avoid hidden dependencies
- render deterministically from inputs

Component API guidelines:
- required parameters first
- modifiers exposed consistently
- callbacks explicit
- avoid excessive parameter count
- group complex visual configuration into stable parameter objects when needed

Preferred parameter order:
1. required data
2. event callbacks
3. modifier
4. optional visual parameters

Avoid components that:
- fetch their own data
- know about repositories
- perform navigation internally unless explicitly a route-level component
- contain multiple unrelated visual responsibilities

---

## Modifier Conventions

Modifier rules:
- always expose `modifier: Modifier = Modifier` for reusable composables
- apply external modifier at the top-level container
- avoid swallowing caller layout control
- do not pass modifier to multiple unrelated internal children unless explicitly documented

Good pattern:
- one root modifier parameter per composable

Avoid:
- hidden padding that prevents reuse in layouts
- layout behavior that surprises callers
- over-chaining modifiers when extracting a small helper improves readability

---

## Layout Rules

Layouts should be:
- readable
- shallow where possible
- grouped by semantic region
- adaptive when required by platform or window size

Guidelines:
- prefer clear hierarchy over clever compactness
- extract layout sections when a composable grows beyond easy scanning
- keep deeply nested containers under control
- use lazy containers for lists with real scrolling datasets
- use stable item keys where relevant

Avoid:
- giant screen composables
- mixed scrolling containers without care
- duplicating layout structures across screens that should be components

---

## Lists and Collections

For list rendering:
- use lazy layouts for dynamic or long collections
- provide stable keys when item identity exists
- keep row components stateless
- move item formatting out of the row when it grows complex

Rules:
- list rows should receive display-ready models
- scrolling behavior should remain predictable
- empty state, loading state, and populated state should be handled explicitly

---

## Forms and Inputs

Forms should follow these rules:
- input state should be explicit
- validation presentation should be deterministic
- field components should expose value and callbacks clearly
- submission logic belongs above the field component level

Prefer:
- field state models with value, error, enabled, label, placeholder when needed
- explicit validation messages
- focus progression handled intentionally

Do not:
- bury validation rules in visual components
- perform domain validation directly in leaf composables unless purely presentational
- scatter field behavior across unrelated helpers

---

## Loading, Empty, and Error States

Every feature screen should explicitly define rendering for:
- loading
- empty
- error
- content

Rules:
- these states must be visible in previews and test coverage
- avoid mixing partial states ambiguously
- content and feedback states should have predictable rendering priority

Preferred patterns:
- sealed state model
- explicit sections within `FeatureContent`

---

## Accessibility

Accessibility is required, not optional.

Compose UI should:
- provide meaningful labels and semantics
- support touch targets of adequate size
- expose state meaningfully for assistive technologies
- avoid relying only on color to communicate critical meaning
- preserve readable text hierarchy and contrast through the theme

Rules:
- interactive elements must be identifiable
- icons that communicate meaning should have accessible labels unless decorative
- decorative visuals should not create noise in semantics
- screen structure should remain understandable to keyboard and assistive navigation where applicable

---

## Adaptive and Responsive UI

For multiplatform UI, layouts should adapt thoughtfully.

Guidelines:
- treat compact and expanded layouts as deliberate variants
- avoid hardcoding assumptions about screen size or orientation
- isolate adaptive rules into layout helpers or screen-level logic
- keep components reusable across phone, tablet, desktop, and larger windows when feasible

Use adaptation for:
- pane layout changes
- navigation presentation changes
- spacing and max-width adjustments
- density of displayed information

Do not:
- fork entire screens unnecessarily
- hide architecture problems behind ad hoc responsive hacks

---

## Platform Differences

Compose UI should remain shared unless the visual or host behavior truly differs.

Acceptable platform-specific UI differences:
- window controls
- system bars integration
- platform idiomatic gesture or shortcut support
- host-level input differences
- accessibility integration differences when required

Rules:
- isolate platform UI differences behind small adapters
- do not duplicate shared screen implementations without a real need
- keep visual divergence intentional and documented

---

## Performance Rules

Compose performance should be designed in, not patched later.

Rules:
- keep state models stable and explicit
- avoid unnecessary recomposition triggers
- prefer immutable UI models
- extract expensive calculations from composition when possible
- use `remember` only when it improves correctness or performance clearly
- use lazy lists appropriately
- provide stable item identity

Avoid:
- passing frequently changing large objects unnecessarily
- doing non-trivial computation inline every recomposition
- storing unstable state in wide screen trees without need
- premature micro-optimizations that reduce readability

Preferred mindset:
- clear data flow first
- stability and measurement second
- targeted optimization third

---

## Preview Rules

Every meaningful reusable component and major screen state should be previewable.

Preview requirements:
- default content preview
- loading preview when relevant
- error preview when relevant
- empty preview when relevant
- edge-case preview for complex components

Preview data should:
- be fake
- be deterministic
- not depend on network, storage, or runtime services

Rules:
- previews should live close to the component/screen
- previews must not require app bootstrapping
- preview names should be explicit

---

## Testing Strategy

Compose UI testing should be layered:

- screenshot tests for relevant components and screen states
- instrumented tests for behavior, interaction, and host integration
- unit tests for pure logic that does not need Compose runtime or device behavior

### Screenshot Tests

Use screenshot tests to cover:
- major screen states
- component variants
- theme and layout regressions
- loading, empty, error, and content rendering

### Instrumented Tests

Use instrumented tests to cover:
- click and input behavior
- semantics and accessibility-critical interactions
- navigation triggers at the UI boundary
- lifecycle-sensitive behavior
- host integration that may require Android instrumentation, Robolectric, or an equivalent library when the platform allows it

### Unit Tests

Use unit tests for:
- reducers and presentation logic
- state derivations that do not need Compose runtime
- pure formatting and mapping helpers
- deterministic logic that should stay fast and isolated

Do not use unit tests as a substitute for screenshot or instrumented coverage when UI behavior is involved.

---

## Testing Matrix

When creating or changing tests, load only the section that matches the work.

| Test type | Load this section | Use when | Typical scope |
| --- | --- | --- | --- |
| Unit | `Testing Strategy` and `Testing Expectations for UI` | the behavior is pure logic | reducers, mappers, validation, state derivation |
| Screenshot | `Testing Strategy`, `Screenshot Tests`, and `Testing Expectations for UI` | the output is visual or stateful | screen states, component variants, theme regressions |
| Instrumented | `Testing Strategy`, `Instrumented Tests`, and `Testing Expectations for UI` | behavior depends on Compose runtime or host integration | interactions, semantics, lifecycle, navigation triggers |
| Host-light testing | `Testing Strategy` and `Instrumented Tests` | Android behavior needs a lighter environment | Robolectric or equivalent framework coverage |

Token guidance:

- load only the matching row and the minimum surrounding context
- avoid loading unrelated Compose sections when a test only touches one behavior
- prefer the shortest path that still proves the change

---

## Testing Expectations for UI

UI tests should focus on rendering and interaction, not business rules.

What to test:
- key states render correctly
- important interactions emit expected events
- accessibility-critical semantics where feasible
- conditional rendering paths
- navigation triggers at the UI boundary

What not to over-test:
- trivial Compose internals
- implementation detail layout nodes that are likely to change without behavior changes

Prefer:
- screen contract tests
- component interaction tests
- screenshot tests for stable visual regressions
- snapshot-like verification only when stable and useful in your tooling strategy

---

## File Organization Inside UI Features

Recommended per-feature organization:

- `FeatureRoute.kt`
- `FeatureScreen.kt`
- `FeatureContent.kt`
- `components/`
- `model/`
- `preview/` if needed
- `navigation/` if feature-local navigation exists

For design system:

- `theme/`
- `tokens/`
- `components/`
- `foundation/`

Keep package names explicit and shallow enough to navigate easily.

---

## What Must Stay Out of Compose Files

Do NOT place these directly into Compose UI files unless they are trivial adapters:
- repository calls
- persistence decisions
- networking logic
- domain calculation logic
- platform service orchestration
- application bootstrapping
- dependency container setup

Compose files may call callbacks and render state.
They must not become hidden controllers.

---

## Decision Rules

When deciding where something belongs:

Put it in Compose UI if it is about:
- rendering
- layout
- interactions
- theme
- navigation presentation
- visual state
- accessibility semantics
- adaptive UI arrangement

Put it outside Compose UI if it is about:
- business rules
- data fetching
- persistence
- platform service orchestration
- serialization
- domain transformation not specific to rendering

---

## Anti-Patterns

Avoid these anti-patterns:
- fat screen composables with business logic
- direct repository usage in UI
- raw domain/infrastructure objects leaking into leaf UI components
- stateful reusable components by default
- using side effects to compensate for poor architecture
- navigation framework objects passed throughout the tree
- inconsistent component naming
- duplicated theme values in feature files
- loading business context into the UI specialty

---

## Professional Default Standard

For professional projects, assume the following default:
- shared Compose UI lives in common code whenever practical
- route/screen/content separation is mandatory for non-trivial screens
- reusable components are stateless by default
- UI state is immutable and presentation-ready
- design system is centralized
- platform-specific UI divergence is minimized
- previews are required for major states
- accessibility is part of the definition of done

---

## Minimal Context Loading Guide

Load this file only when the task is about Compose UI behavior or structure.

Also load:
- `business/state.md` when working with screen state contracts
- `business/usecases.md` when verifying event boundaries
- `core/architecture.md` when checking separation of concerns
- target platform files only if host integration matters

When creating or altering tests, load only the relevant testing section:
- `Testing Strategy` for the overall policy
- `Screenshot Tests` for visual regressions
- `Instrumented Tests` for behavior and host integration
- `Unit Tests` for pure logic
- `Testing Expectations for UI` for what counts as UI coverage

Do NOT load infrastructure specialties unless the UI task directly depends on them.

This keeps Compose tasks focused and context-light.
