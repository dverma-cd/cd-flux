# CD Flux 📦➡️🌥️

FluxCD repository that drives AKS deployments for `my-app`.

## Layout
- `apps/my-app/dev/helmrelease.yaml` — uses the dev image tag from ACR.
- `apps/my-app/prod/helmrelease.yaml` — prod image tag for AKS prod.

## How tags get here
- **Dev path**: `cd-app/.github/workflows/dev.yaml` runs on `feature/**` and `fix/**`, builds/pushes the image to ACR, then commits the new tag straight into this repo (dev HelmRelease) when `REPO2_PAT` is available. Flux sees the change and deploys to the dev namespace automatically.
- **Prod path**: `cd-app/.github/workflows/prod.yaml` (on `master` or manual dispatch) builds/pushes the image, then creates/updates branch `release-<TAG>` here with the prod tag change and opens a PR to `master`. Merge the PR to roll out to prod via Flux.

## Manual tweaks
- Edit the HelmRelease you want and push to `master` (or merge the release PR). Flux will reconcile and deploy.
