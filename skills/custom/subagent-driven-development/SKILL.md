---
name: subagent-driven-development
description: Decompose implementation work cleanly when parallel subtasks are justified.
license: Apache-2.0
---

# Subagent-Driven Development

Use this skill when implementation naturally splits into independent subtasks such as code changes, validation, and repo inspection.

## When To Use

- separate files or modules can be inspected independently
- validation can run in parallel with narrow analysis
- the work is large enough to benefit from decomposition

## Rules

- decompose only when it simplifies the task
- keep each subtask narrow and independently checkable
- synthesize results before deciding on final edits

## Guardrails

- Do not spawn parallel work for trivial tasks.
- Do not let subtasks drift from the approved plan.
