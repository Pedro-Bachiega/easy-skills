# State Review

Reviews presentation state and event-flow design.

## Check
- is UI state immutable and explicit
- are modes represented clearly
- are events named by user intent
- are one-off effects justified
- is business logic staying outside render-only layers

## Flag
- multiple booleans representing exclusive modes
- raw domain or DTO leakage into UI state
- event naming by implementation rather than intent
- hidden business rules in state holders
- poor lifecycle or cancellation handling
