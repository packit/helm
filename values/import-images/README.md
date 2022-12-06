## Install

Login to the Openshift cluster:

    oc login --token=sha256~....  --server= ....

### Install from this repo

    make install PROJECT=packit-prod

### Install from chart repository

If you're going to use the chart from outside (without having this repo cloned),
you can install the chart from our chart repository. You just need to have a file
with keys overriding those defined in `values.yaml` with `~` value.

    helm repo add packit https://helm.packit.dev
    helm repo update
    helm upgrade --install --cleanup-on-fail import-images packit/import-images --values your-values-file.yaml

### Render templates

If you just want to see how the rendered templates would look like:

    make dryrun PROJECT=packit-prod
