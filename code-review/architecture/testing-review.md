# Testing Review

Reviews whether the PR proves safety and correctness adequately.

## Check
- are there tests
- do they cover the changed behavior
- do they cover the most important failure paths
- is integration testing needed
- are platform-specific or boundary-specific tests missing

## Flag
- tests only for happy paths
- no regression tests for fixed bugs
- no teardown/lifecycle tests
- no invalid-input coverage
- no interop or ABI coverage where boundaries changed

## Special Cases
For UI:
- state coverage
- interaction coverage
- loading/error/empty coverage

For C++ native boundaries:
- create/use/destroy lifecycle tests
- buffer and encoding tests
- load/unload tests
- invalid handle tests
