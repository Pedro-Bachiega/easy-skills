# Performance Review

Reviews performance-sensitive changes.

## Check
- did allocations increase
- did recompositions or render churn increase
- did call frequency across boundaries increase
- did synchronization costs increase
- is batching needed
- is the cost visible in the API

## Flag
- unnecessary conversions
- hidden copies
- chatty FFI boundaries
- avoidable locking
- unbounded work on UI or hot paths
- performance claims without measurement

## Rule
Do not block merge for hypothetical micro-issues unless the path is clearly hot or the regression is obvious.
