---
name: pr-multi-model-review
description: Review a GitHub pull request by fanning out to multiple configured reviewer subagents, then synthesize their markdown reports into one review summary. Use when the user asks to review a PR link with multiple models, multiple perspectives, or independent reviewer agents.
---

# PR Multi-Model Review

Use this skill to review a pull request through independent reviewer subagents and artifact-based handoff.

## Preconditions

- `subagent_enabled` must be true.
- The configured subagents should include reviewer types such as:
  - `code-reviewer-gpt5`
  - `security-auditor-claude`
  - `test-engineer-gemini`
- Each reviewer subagent should have a distinct `model` and perspective in `config.yaml`.

## Artifact Contract

All intermediate and final outputs must be markdown or patch artifacts under `/mnt/user-data`.

Input artifacts:

```text
/mnt/user-data/workspace/pr-review/pr_metadata.md
/mnt/user-data/workspace/pr-review/pr_diff.patch
```

Reviewer outputs:

```text
/mnt/user-data/outputs/reviews/code_review.md
/mnt/user-data/outputs/reviews/security_review.md
/mnt/user-data/outputs/reviews/test_review.md
```

Final output:

```text
/mnt/user-data/outputs/review_summary.md
```

## Workflow

1. Parse the pull request URL.
2. Fetch the pull request patch by appending `.patch` to the PR URL.
3. Write the patch to `/mnt/user-data/workspace/pr-review/pr_diff.patch`.
4. Write basic PR metadata to `/mnt/user-data/workspace/pr-review/pr_metadata.md`.
5. Launch independent reviewer subagents in parallel, one per configured perspective.
6. In each subagent prompt, require the reviewer to read the shared PR artifacts and write exactly one markdown report to its assigned output path.
7. Read all reviewer markdown reports.
8. Synthesize `/mnt/user-data/outputs/review_summary.md`.

## Reviewer Prompts

Use this shape for each reviewer task:

```text
Review the pull request using your configured perspective.

Inputs:
- Metadata: /mnt/user-data/workspace/pr-review/pr_metadata.md
- Patch: /mnt/user-data/workspace/pr-review/pr_diff.patch

Output:
- Write your report to: <assigned output path>

Do not modify source code. Focus on findings, evidence, severity, and concrete recommendations.
```

## Final Summary Format

The final `review_summary.md` must include:

```markdown
# PR Review Summary

## Verdict
APPROVE | REQUEST CHANGES

## Blocking Findings
- ...

## Important Findings
- ...

## Model / Perspective Consensus
- ...

## Disagreements Or Uncertainty
- ...

## Reviewer Artifacts
- `reviews/code_review.md`
- `reviews/security_review.md`
- `reviews/test_review.md`
```

## Rules

- Do not treat a single model's finding as final when other reviewers conflict; surface the disagreement.
- Prefer concrete file and line references from the patch when available.
- Do not create a PR or merge anything.
- Do not ask the subagents to fetch the PR independently; all reviewers must use the shared artifacts.
