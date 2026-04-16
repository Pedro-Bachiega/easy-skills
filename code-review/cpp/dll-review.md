# DLL / Shared Library Review

Reviews exported native library surfaces and packaging behavior.

## Check
- export surface minimized
- public/private headers separated
- ABI-sensitive types reviewed carefully
- version query or compatibility strategy present where needed
- thread safety and ownership rules documented or inferable
- load/unload behavior tested

## Flag
- exported STL-heavy or compiler-sensitive interfaces for foreign consumers
- public exceptions crossing the wrong boundary
- allocation/free mismatch risk
- undocumented initialization requirements
- missing export/version/load tests
