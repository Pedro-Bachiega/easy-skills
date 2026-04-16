# Architecture Rules

Defines system-wide architectural constraints.

## Layers

1. Domain
2. Use Cases
3. State
4. Platform Adapters
5. UI (external)

## Rules

* Dependencies must flow inward only.
* Domain has zero platform knowledge.
* Use cases orchestrate domain logic.
* State exposes observable data to UI.
* Platform code implements interfaces, never owns logic.

## Forbidden

* UI logic in domain
* Platform APIs in common code
* Business rules inside ViewModels / controllers

## Allowed

* Pure Kotlin logic in commonMain
* Interface-driven boundaries
