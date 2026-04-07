# CD Flux

Flux HelmRelease definitions for `my-app`.

## Structure
- `apps/my-app/dev/helmrelease.yaml` — points to `cdappacr.azurecr.io/my-app:...` for dev.
- `apps/my-app/prod/helmrelease.yaml` — prod image reference.

## How it’s updated by pipelines
- Dev workflow (`cd-app/.github/workflows/dev.yaml`): when `REPO2_PAT` is set, it checks out this repo (branch `feature/docker-app` while under development), bumps the dev tag, and commits/pushes directly.
- Prod workflow (`cd-app/.github/workflows/prod.yaml`): builds image, checks out this repo, updates prod tag on a branch `release-<tag>`, pushes, and opens a PR to `master`.

## Manual updates
Edit the desired HelmRelease file and commit to `master`, or merge the auto-created release PRs.
