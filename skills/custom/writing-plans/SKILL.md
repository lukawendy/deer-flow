---
name: writing-plans
description: Turn repository context and constraints into an approval-ready execution plan.
license: Apache-2.0
---

# Writing Plans

Use this skill when the task requires an implementation plan that another stage or agent will execute later.

## Goals

- produce a plan that is easy for a human to approve
- make scope, risks, and validation explicit
- define the smallest executable sequence of work

## Plan Requirements

The plan should usually contain:

- Request
- Constraints
- Repository Context
- Proposed Next Steps
- Risks

Where useful, also include:

- suspected files or modules
- validation strategy
- rollback or containment notes

## Workflow

1. Summarize the request in one short paragraph.
2. Extract all hard constraints.
3. Inspect just enough repository context to localize the work.
4. Break the implementation into small ordered tasks.
5. Describe how success will be validated.
6. Call out major risks, assumptions, and unknowns.

## Quality Bar

A good plan is:

- specific enough for implementation
- narrow enough to avoid unnecessary change
- explicit about what is not being changed
- readable as a markdown artifact

## Guardrails

- Do not write code.
- Do not pretend repository facts you have not checked.
- Do not skip validation strategy.
