# Architecture Review

Reviews architectural integrity.

## Check
- are layers still clear
- did dependencies move in the wrong direction
- did the change increase coupling
- is platform-specific logic leaking into shared logic
- is interop logic staying at the edge
- are responsibilities in the right module/file

## Flag
- mixed concerns
- boundary violations
- duplicated architectural rules
- platform logic placed in shared/core code incorrectly
- UI owning business rules
- foreign language wrappers owning native business logic

## Required Questions
- should this live here
- is this the correct boundary
- will this be harder to evolve later
