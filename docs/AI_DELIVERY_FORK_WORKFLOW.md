# AI Delivery Fork Workflow

This repository is a fork used by AI Delivery Platform. Keep upstream synchronization and product integration work separated.

## Branch Roles

Use these branch roles by default:

```text
origin/main
  Tracks bytedance/deer-flow main as closely as possible.
  Do not land AI Delivery product changes here.

origin/integration/ai-delivery
  Stable integration branch for AI Delivery Platform.
  Product-specific DeerFlow changes land here after review.

codex/<feature-name>
  Short-lived feature branches for implementation and review.

archive/<name>
  Historical snapshots of old integration states that should not remain active.
```

## Upstream Sync

To refresh the fork from official DeerFlow:

```bash
git fetch origin upstream --prune
git switch main
git merge --ff-only upstream/main
git push origin main
```

If `integration/ai-delivery` should be reset to a clean upstream baseline, archive the old head first:

```bash
git push origin <old-sha>:refs/heads/archive/integration-ai-delivery-<short-sha>
git switch -C integration/ai-delivery upstream/main
git push --force-with-lease origin integration/ai-delivery
```

Use `--force-with-lease`, not plain `--force`.

## Feature Workflow

Create feature branches from the current `integration/ai-delivery` baseline unless the work is explicitly an upstream sync:

```bash
git fetch origin upstream --prune
git switch integration/ai-delivery
git pull --ff-only origin integration/ai-delivery
git switch -c codex/<feature-name>
```

Open pull requests into:

```text
codex/<feature-name> -> integration/ai-delivery
```

Do not open AI Delivery feature pull requests into `main`.

## Release Pinning

After a reviewed integration point is accepted, tag the integration branch:

```bash
git tag ai-delivery-deerflow-YYYY-MM-DD.N
git push origin ai-delivery-deerflow-YYYY-MM-DD.N
```

AI Delivery Platform should pin DeerFlow by tag or commit SHA, not by an unreviewed moving branch.

## When To Keep Old Work

If an older integration commit may contain useful ideas but should not remain active, keep it under `archive/*`. Cherry-pick only the specific changes that are still needed onto a fresh feature branch.
