# Build Review

Reviews build and packaging changes.

## Check
- target definitions remain clear
- public includes and private includes are separated
- warnings and standard settings stay consistent
- symbols and packaging outputs are appropriate
- linkage/runtime assumptions are intentional
- generated files and release artifacts are handled cleanly

## Flag
- accidental ABI-affecting changes without review
- hidden compiler-specific assumptions
- release builds missing symbols strategy
- packaging drift not reflected in tests or docs
