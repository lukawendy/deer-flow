---
name: test-driven-development
description: Keep implementation grounded in validation and regression awareness.
license: Apache-2.0
---

# Test-Driven Development

Use this skill when implementation should stay close to expected behavior and regression risk needs to stay low.

## Principles

- define the behavior to protect before editing broadly
- add or update the smallest meaningful test when feasible
- prefer narrow validation before broad suites

## Workflow

1. Identify the behavior that must hold after the change.
2. Check whether an existing test already covers it.
3. Add or update a focused test when practical.
4. Run the smallest relevant validation first.
5. Record what was validated and what remains unverified.

## Guardrails

- Do not claim full coverage if only partial validation ran.
- Do not add large new test infrastructure unless required.
