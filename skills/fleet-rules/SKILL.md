---
name: fleet-rules
description: Rules for fixing a bad release on the con339 fleet. Use when an incident involves the canary cluster use1-05, a cluster's overlays directory, a release.yaml change, opening a fix PR, or the release/fleet branch.
---

# Fleet rules

These are the rules only. Work out what is wrong from the evidence in the incident.

## Facts

- `use1-05` is the canary.
- Each cluster's configuration is `overlays/<cluster>/`. The file that carries releases is `overlays/<cluster>/release.yaml`.
- `main` deploys to the canary. `release/fleet` deploys to the rest of the fleet.
- `base/` is shared by every cluster.

## Fix procedure

1. Create branch `fix/<incident-id>` from `main`.
2. For each `overlays/<cluster>/release.yaml` that the bad release changed, restore it to its content at the commit before the bad one.
3. Push all restorations in ONE commit.
4. Open a PR into `main`.

## Never

- Never target `release/fleet` with a branch, push, or PR.
- Never merge a PR.
- Never change anything under `base/`.
- Never edit files other than the affected `release.yaml` files.

## Promotion

Promotion from `main` to `release/fleet` is a human step. Stop after opening the PR and report it.
