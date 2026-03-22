---
name: brainstorming
description: Generate implementation-safe idea exploration before committing to a plan.
license: Apache-2.0
---

# Brainstorming

Use this skill when the request is still underspecified, has multiple viable approaches, or may affect several parts of a codebase.

## Goals

- clarify the actual problem before proposing work
- surface assumptions and unknowns early
- identify 2-4 realistic implementation directions
- narrow to the safest path for the current repository and constraints

## Workflow

1. Restate the request in concrete engineering terms.
2. Extract explicit constraints from the user message and repository context.
3. List the most likely root causes, change surfaces, or solution shapes.
4. Compare candidate approaches using:
   - implementation scope
   - regression risk
   - testability
   - reversibility
5. Prefer the smallest safe path that satisfies the request.

## Output Pattern

When used in planning, make the analysis concise and actionable:

- Problem framing
- Key constraints
- Candidate approaches
- Recommended approach
- Open questions or risks

## Guardrails

- Do not start implementation.
- Do not present a single approach without mentioning tradeoffs.
- Do not assume broad refactors are justified unless the request explicitly demands them.
