# Compose Review

Reviews Compose UI structure and behavior.

## Check
- route/screen/content separation where complexity warrants it
- stateless components by default
- state hoisting done appropriately
- UI rendering from presentation-ready state
- loading/error/empty/content states covered
- accessibility semantics considered
- previews or testability preserved
- navigation logic staying at the route edge

## Flag
- business logic in composables
- side effects compensating for poor architecture
- giant screen composables
- direct repository or infrastructure calls from UI
- ambiguous mutable UI state
