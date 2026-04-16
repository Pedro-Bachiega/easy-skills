# Memory Review

Reviews ownership, lifetime, allocation, and destruction safety.

## Check
- who owns each resource
- whether release paths are obvious
- whether allocation/deallocation stay in the correct domain
- whether binary boundary memory rules are safe
- whether handles are destroyed correctly
- whether shutdown order is sound

## Flag
- use-after-free risk
- double free risk
- hidden borrowed lifetime assumptions
- ownership crossing a DLL/FFI boundary ambiguously
- resource cleanup only on happy path
