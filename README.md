# Helm Charts

for
* [Packit Service Validation cron job](https://github.com/packit/deployment/tree/main/cron-jobs/packit-service-validation)

## Deployment

All charts are deployed automatically via GitHub/Gitlab CI/CI.

For instructions how to do it manually, see
* [packit-service-validation/README.md](values/packit-service-validation/README.md)

## Releases

There's a [release workflow](https://github.com/packit/udp/blob/main/.github/workflows/release.yml)
to automate releasing the Helm charts and
adding them to a repository on every push to `main`.
Don't forget to bump a chart version
[packit-service-validation](https://github.com/packit/helm/blob/main/helm-charts/packit-service-validation/Chart.yaml#L5))
if you want a new chart version to be released.

### [Repository](https://helm.sh/docs/topics/charts/#chart-repositories)

Is hosted on GitHub Pages in this repo and reachable at [helm.packit.dev](https://helm.packit.dev)


    $ helm repo add packit helm.packit.dev
    "packit" has been added to your repositories

    $ helm repo update
    Hang tight while we grab the latest from your chart repositories...
    ...Successfully got an update from the "packit" chart repository
    Update Complete. ⎈Happy Helming!⎈

    $ helm search repo packit
    NAME                            	CHART VERSION	APP VERSION	DESCRIPTION
    packit/packit-service-validation	1.2.1        	           	Helm chart for deploying packit-service-validat...


## [Unified Openshift Deployment Process](https://docs.google.com/presentation/d/1MlLuuawzxJg6U15zbPby6JAtNNEWZAhfGEWNcpYSWeo)

We use images created by a GitHub workflow and pushed to Quay.io,
the **tag** for an image is the first *7 digit for the commit SHA*.
