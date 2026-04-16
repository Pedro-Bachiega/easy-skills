# Testing Strategy

Defines the required testing strategy for professional C++ work.

## Testing Layers

### Unit Tests
- pure logic
- edge cases
- error paths
- small utilities

### Integration Tests
- component integration
- file/network/process boundaries
- native-to-wrapper integration
- DLL load/export use

### System Tests
- real packaging layout
- end-to-end workflows
- startup/shutdown
- interoperability with host applications

### ABI / Boundary Tests
- exported symbol presence
- version compatibility
- invalid-handle behavior
- ownership correctness
- error translation correctness

### Fuzz / Robustness Tests
- parser inputs
- malformed boundary inputs
- hostile-but-authorized test data for robustness

## Mandatory Coverage Areas for DLL Projects

- library load/unload
- create/use/destroy lifecycle
- string encoding behavior
- buffer size edge cases
- concurrent access where supported
- repeated initialization/teardown
- failure path cleanup
- external language smoke tests when applicable

## For Authorized Hook / Injection Lab Work

Require:
- exact-scope lab validation
- non-target rejection behavior
- enable/disable tests
- rollback tests
- stability regression tests

## Professional Default Standard

No native boundary is considered complete without boundary-focused tests.
