# Interop Review

Reviews Kotlin/native interoperability.

## Check
- wrapper boundaries are thin and clear
- resources are released explicitly
- errors are translated consistently
- blocking vs non-blocking behavior is visible
- thread-safety assumptions are documented or enforced
- conversions happen at the edge, not everywhere

## Flag
- Kotlin wrapper leaking native handles carelessly
- native lifetime hidden behind GC assumptions
- exception or status translation ambiguity
- duplicate conversion logic spread through the app
