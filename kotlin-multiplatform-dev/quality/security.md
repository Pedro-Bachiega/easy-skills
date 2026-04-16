# Security Review

## Responsibilities

* trust boundary awareness
* safe handling of untrusted input
* misuse-resistant API and adapter design

## Rules

* validate inputs at the boundary
* keep dangerous capabilities explicit
* avoid leaking platform or infrastructure details into shared code
* prefer least-privilege access to platform services

## Focus Areas

* file, network, and runtime boundaries
* platform service permissions
* data sanitization and encoding assumptions
* sensitive data handling in shared Kotlin code
* unsafe UI-triggered actions that cross into infrastructure
