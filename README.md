# [Unified Openshift Deployment Process](https://docs.google.com/presentation/d/1MlLuuawzxJg6U15zbPby6JAtNNEWZAhfGEWNcpYSWeo)

for the [Packit Service Validation](https://github.com/packit/deployment/tree/main/cron-jobs/packit-service-validation).

To deploy the *Packit Service Validation* through *Helm* follow this steps:

### Setup deployment

Helm uses an **image** created through a GitHub action and pushed to Quay.io,
the **tag** for this image is the first *7 digit for the commit SHA* of the packit/deployment repo.

To use a new image update the referenced tag
[here](https://github.com/packit/udp/blob/main/ocp-deployments/packit-service-validation-prod.yaml#L18).

### Install Helm Chart

Login to OpenShift cluster and switch to proper project. In case of packit-service validation
it's `cyborg` project @ [PSI Cluster](https://ocp4.psi.redhat.com).

    oc login --token=sha256~....  --server= ....
    oc project cyborg

Get secrets from Bitwarden.
Sentry from `extra-vars.yml` in `secrets-packit-[prod|stg]` item and
GitHub token from `Release/usercont bot` item.

    export SENTRY=$( echo -n 'token from bitwarden' | base64 )
    export GITHUB=$( echo -n 'token from bitwarden' | base64 )

#### Install from this repo

    helm upgrade --install --cleanup-on-fail packit-service-validation ocp-helm-charts/packit-service-validation/ --set secrets.sentry=${SENTRY} --set secrets.github=${GITHUB} --values ocp-deployments/packit-service-validation/prod.yaml

#### Install from chart repository

    helm repo add packit https://helm.packit.dev
    helm repo update
    helm upgrade --install --cleanup-on-fail packit-service-validation packit/packit-service-validation --set secrets.sentry=${SENTRY} --set secrets.github=${GITHUB} --values ocp-deployments/packit-service-validation/prod.yaml

### Render templates

If you just want to see how the rendered templates would look like,
add `--dry-run --debug` to the above `helm upgrade` command.

### Releases
There's a [release workflow](https://github.com/packit/udp/blob/main/.github/workflows/release.yml)
to automate releasing the Helm charts. It uses
[Helm Chart Releaser Action](https://github.com/marketplace/actions/helm-chart-releaser)
which turns this project into a self-hosted Helm chart repository.
It does this – during every push to `main` – by checking each chart in the project,
and whenever there's a new chart version, creates a corresponding GitHub release
named for the chart version, adds Helm chart artifacts to the release,
and creates or updates an `index.yaml` file with metadata about those releases,
which is then hosted on GitHub Pages at [helm.packit.dev](https://helm.packit.dev).
