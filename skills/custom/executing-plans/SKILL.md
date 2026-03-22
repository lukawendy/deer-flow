---
name: executing-plans
description: Execute an approved implementation plan in small, traceable steps.
license: Apache-2.0
---

# Executing Plans

Use this skill after a plan has been approved and implementation may begin.

## Goals

- follow the approved plan closely
- prefer the smallest safe code change
- keep implementation auditable

## Workflow

1. Re-read the approved plan and constraints.
2. Identify the minimal files needed for the current task.
3. Make one logical code change at a time.
4. Re-check the changed files after each edit.
5. Summarize what changed, what remains, and what still needs validation.

## Guardrails

- Do not silently broaden scope.
- Do not skip validation notes.
- Do not create merge-ready claims unless tests or checks actually ran.
