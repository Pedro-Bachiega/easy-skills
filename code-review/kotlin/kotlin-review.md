# Kotlin Review

Reviews Kotlin code quality and maintainability.

## Check
- naming clarity
- immutability where appropriate
- nullability correctness
- explicitness of state and event flow
- extension/helper usage staying readable
- coroutine or async usage being structured and safe
- no platform leakage into shared logic unless intended

## Flag
- overly implicit state changes
- hidden side effects
- nullable abuse
- giant utility files
- business logic embedded in UI or platform glue
- poor source set separation in shared code
