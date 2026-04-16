# API Review

Reviews public and semi-public contracts.

## Check
- is the API small and obvious
- is ownership clear
- are threading guarantees documented or inferable
- is error behavior explicit
- is misuse resistance reasonable
- are changes backward compatible where required

## Flag
- ambiguous ownership
- unstable or leaky abstractions
- public API exposing internal implementation details
- undocumented breaking behavior
- callback/threading ambiguity
- excessive surface area

## Special Attention
For native/public boundaries:
- versioning
- ABI stability
- struct layout assumptions
- handle lifecycle rules
- string and buffer contracts
