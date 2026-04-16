# Android Target

## Responsibilities

* Activity setup
* lifecycle binding
* permissions
* Android services

## Rules

* Keep Activities thin
* Use interfaces to access platform features
* No business logic here

## Source Set

* androidMain → implementations
* androidTest → platform tests

## Examples

* notifications
* intents
* WorkManager

## Exclusion

Compose rules → @compose-ui.md
