# Debugging and Diagnostics

Defines debugging workflow expectations.

## Areas

- symbols and symbol loading
- crash dump analysis
- memory diagnostics
- race diagnostics
- boundary verification
- loader diagnostics
- exported symbol inspection
- interop diagnostics

## Rules

- always keep symbol strategy documented
- make release crash triage possible
- isolate reproducible harnesses for DLL and interop bugs
- validate boundary assumptions with small probes first
- distinguish initialization bugs from steady-state bugs

## For DLL and FFI Work

Always be able to answer:
- did the library load
- did symbols resolve
- did version checks pass
- did ownership rules hold
- did encoding conversion succeed
- did teardown happen cleanly
