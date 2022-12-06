# Helm Charts

for
* [Packit Service Validation cron job](https://github.com/packit/deployment/tree/main/cron-jobs/packit-service-validation)
* [Import-images cron job](https://github.com/packit/deployment/tree/main/cron-jobs/import-images)

## Deployment

All charts are deployed automatically via GitHub/Gitlab CI/CI.

For instructions how to do it manually, see
* [packit-service-validation/README.md](values/packit-service-validation/README.md)
* [import-images/README.md](values/import-images/README.md)

## Releases

There's a [release workflow](https://github.com/packit/udp/blob/main/.github/workflows/release.yml)
to automate releasing the Helm charts. It uses
[Helm Chart Releaser Action](https://github.com/marketplace/actions/helm-chart-releaser)
which turns this project into a self-hosted Helm chart repository.
It does this – during every push to `main` – by checking each chart in the project,
and whenever there's a new chart version, creates a corresponding GitHub release
named for the chart version, adds Helm chart artifacts to the release,
and creates or updates an `index.yaml` file with metadata about those releases,
which is then hosted on GitHub Pages at [helm.packit.dev](https://helm.packit.dev).

## [Unified Openshift Deployment Process](https://docs.google.com/presentation/d/1MlLuuawzxJg6U15zbPby6JAtNNEWZAhfGEWNcpYSWeo)

We use images created by a GitHub workflow and pushed to Quay.io,
the **tag** for an image is the first *7 digit for the commit SHA*.
