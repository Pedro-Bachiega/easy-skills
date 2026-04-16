# Kotlin Multiplatform Review

Reviews KMP-specific boundaries.

## Check
- is shared logic staying in common code where appropriate
- is platform-specific logic staying in source sets
- are modules responsibility-based rather than target-based
- are expect/actual decisions justified
- are app modules the only platform-specific modules when following this architecture

## Flag
- platform-specific modules outside app launchers
- shared code importing platform details incorrectly
- duplicated platform implementations that should be source-set specializations
- expect/actual used where interface-based design would be simpler
- common code depending on Android/JVM/iOS details
