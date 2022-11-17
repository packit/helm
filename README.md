# udp

[Unified Openshift deployment Project](https://docs.google.com/presentation/d/1MlLuuawzxJg6U15zbPby6JAtNNEWZAhfGEWNcpYSWeo) for the [Packit Validation Service](https://github.com/packit/deployment/tree/main/cron-jobs/packit-service-validation).

To deploy the *Packit Validation Service* through *Helm* into *cyborg* follow this steps:

### Setup deployment

Helm uses an **image** created through a GitHub action and pushed to Quay.io, the **tag** for this image is the first *7 digit for the commit SHA* of the packit/deployment repo.

To use a new image update the referenced tag [here](https://github.com/packit/udp/blob/main/ocp-deployments/packit-service-validation-prod.yaml#L18).

Copy your OpenShift *API token* from the [PSI Cluster](https://ocp4.psi.redhat.com/)

```
git clone https://github.com/packit/udp.git
oc login --token=sha256~....  --server= ....
oc project cyborg
export PACKIT_SENTRY=$( echo -n 'token from bitwarden' | base64 )
export PACKIT_GITHUB_TOKEN=$( echo -n 'token from bitwarden' | base64 )
```

### Install Service
```
helm upgrade --install --cleanup-on-fail packit-service-validation ocp-helm-charts/packit-service-validation/ --set secrets.sentry=${PACKIT_SENTRY} --set secrets.github=${PACKIT_GITHUB_TOKEN} --values ocp-deployments/packit-service-validation-prod.yaml
```

### Uninstall Service
```
helm uninstall packit-service-validation
```
