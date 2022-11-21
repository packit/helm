# udp

[Unified Openshift deployment Project](https://docs.google.com/presentation/d/1MlLuuawzxJg6U15zbPby6JAtNNEWZAhfGEWNcpYSWeo)
for the [Packit Service Validation](https://github.com/packit/deployment/tree/main/cron-jobs/packit-service-validation).

To deploy the *Packit Service Validation* through *Helm* follow this steps:

### Setup deployment

Helm uses an **image** created through a GitHub action and pushed to Quay.io,
the **tag** for this image is the first *7 digit for the commit SHA* of the packit/deployment repo.

To use a new image update the referenced tag [here](https://github.com/packit/udp/blob/main/ocp-deployments/packit-service-validation-prod.yaml#L18).

Copy your OpenShift *API token* from the [PSI Cluster](https://ocp4.psi.redhat.com/)

```
git clone https://github.com/packit/udp.git
oc login --token=sha256~....  --server= ....
oc project cyborg
export PACKIT_SENTRY=$( echo -n 'token from bitwarden' | base64 )
export PACKIT_GITHUB_TOKEN=$( echo -n 'token from bitwarden' | base64 )
```

### Install Helm Chart

#### From this repo
```
helm upgrade --install --cleanup-on-fail packit-service-validation ocp-helm-charts/packit-service-validation/ --set secrets.sentry=${PACKIT_SENTRY} --set secrets.github=${PACKIT_GITHUB_TOKEN} --values ocp-deployments/packit-service-validation-prod.yaml
```

#### From chart repository
```
helm repo add packit https://helm.packit.dev
helm repo update
helm upgrade --install --cleanup-on-fail packit-service-validation packit/packit-service-validation --set secrets.sentry=${PACKIT_SENTRY} --set secrets.github=${PACKIT_GITHUB_TOKEN} --values ocp-deployments/packit-service-validation-prod.yaml
```

### Uninstall Helm Chart
```
helm uninstall packit-service-validation
```

### Releases
There's a [release workflow](.github/workflows/release.yml) to automate releasing the Helm charts.
It uses [Helm Chart Releaser Action](https://github.com/marketplace/actions/helm-chart-releaser)
which turns this project into a self-hosted Helm chart repository.
It does this – during every push to `main` – by checking each chart in the project,
and whenever there's a new chart version, creates a corresponding GitHub release
named for the chart version, adds Helm chart artifacts to the release,
and creates or updates an `index.yaml` file with metadata about those releases,
which is then hosted on GitHub Pages at https://helm.packit.dev.
