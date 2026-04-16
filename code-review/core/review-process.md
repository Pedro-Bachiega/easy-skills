# Review Process

Defines the standard review method.

## Goal

Produce reviews that are:
- technically correct
- risk-aware
- scoped to the actual changes
- concise but complete
- optimized for minimal context

## Review Order

Review in this order:

1. Understand change scope
2. Identify affected boundaries
3. Route to needed specialties
4. Review correctness
5. Review safety and misuse risk
6. Review tests and validation
7. Review maintainability
8. Produce structured findings

## Required Review Questions

For every PR:
- What changed?
- What layer changed?
- What boundary changed?
- What can break?
- What tests prove safety?
- What specialty files are actually needed?

## Output Format

### Summary
One short paragraph describing the PR and overall risk.

### Findings
Each finding must include:
- severity
- affected area
- issue
- why it matters
- required fix or recommended improvement

### Missing Validation
Explicitly state what has not been proven by the PR.

### Routing Note
List which review specialties were used.

## Review Style Rules

- prioritize correctness over style
- prioritize boundary safety over local elegance
- flag missing tests explicitly
- avoid speculative criticism without grounding
- keep findings actionable
