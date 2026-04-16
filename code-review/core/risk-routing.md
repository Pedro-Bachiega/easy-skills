# Risk Routing

This file decides which specialties to load based on PR content.

## Always Load
- `review-process.md`
- `review-checklist.md`

## Load `architecture-review.md` when
- modules change
- layering changes
- dependencies change
- shared/platform boundaries shift
- responsibilities move between components

## Load `api-review.md` when
- public APIs change
- exported contracts change
- callback signatures change
- DTOs, ABI structs, or route contracts change

## Load `testing-review.md` when
- behavior changes
- new features are added
- boundaries change
- concurrency or lifecycle changes
- security-sensitive behavior changes

## Load `security-review.md` when
- untrusted input changes
- process/file/network/runtime boundaries change
- native interop changes
- runtime modification/instrumentation changes
- hooks, injection, loading, or privileged operations change

## Load `performance-review.md` when
- hot paths change
- allocations change
- rendering behavior changes
- concurrency changes
- interop call frequency changes

## Load `kotlin-review.md` when
- Kotlin files change

## Load `kmp-review.md` when
- source sets change
- `commonMain` / `androidMain` / `iosMain` / `jvmMain` changes
- KMP module structure changes
- expect/actual changes

## Load `compose-review.md` when
- Compose screens/components/theme/navigation change

## Load `state-review.md` when
- UI state, reducers, presentation models, or event contracts change

## Load `cpp-review.md` when
- C++ implementation changes
- templates, classes, ownership, exceptions, or STL usage change

## Load `memory-review.md` when
- ownership changes
- allocation/free behavior changes
- handles/pointers cross boundaries
- destructors or teardown change

## Load `dll-review.md` when
- exports change
- public headers change
- ABI expectations change
- shared library packaging changes

## Load `ffi-review.md` when
- C ABI changes
- string/buffer/handle contracts change
- foreign language bindings are involved

## Load `interop-review.md` when
- Kotlin/native wrappers change
- resource ownership crosses languages
- callback and threading boundaries cross languages

## Load `runtime-review.md` when
- authorized runtime instrumentation changes
- hook seams change
- process-loading logic changes
- controlled lab-only runtime attachment logic changes

## Load `build-review.md` when
- CMake/build flags/linkage/packaging/symbol generation changes
