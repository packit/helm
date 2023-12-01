## Install

Login to **MP+ preprod cluster** and switch to `packit--validation` project to install **validation for Packit production instance**.

Or login to **MP+ prod cluster** and switch to `packit--validation` project to install **validation for Packit staging instance**.

In this way instances are validated from outside their clusters.

    oc login --token=sha256~....  --server= ....
    oc project packit--validation

Get secrets from Bitwarden.

Sentry from `extra-vars.yml` in `secrets-packit-[prod|stg]` item,

GitHub token from `Release/usercont bot` item.

GitLab token from `Gitlab.com account for validation` item.

Gitlab gnome token for `packit-validation` user taken from `Gitlab (gnome.org)` item.

Gitlab freedesktop token for `packit-validation` user taken from `Gitlab (freedesktop.org)` item.

Gitlab salsa debian token for `packit-validation` user taken from `Gitlab (salsa.debian.org)` item.

    export SENTRY=$( echo -n 'token from bitwarden' | base64 )
    export GITHUB=$( echo -n 'token from bitwarden' | base64 )
    export GITLAB=$( echo -n 'token from bitwarden' | base64 )
    export GITLAB_GNOME=$( echo -n 'token from bitwarden' | base64 )
    export GITLAB_FREEDESKTOP=$( echo -n 'token from bitwarden' | base64 )
    export SALSA_DEBIAN=$( echo -n 'token from bitwarden' | base64 )

### Install from this repo

    make install DEPLOYMENT=[production|staging]

### Install from chart repository

If you're going to use the chart from outside (without having this repo cloned),
you can install the chart from our chart repository. You just need to have a file
with keys overriding those defined in `values.yaml` with `~` value.

    helm repo add packit https://helm.packit.dev
    helm repo update
    helm upgrade --install --cleanup-on-fail packit-service-validation packit/packit-service-validation --set secrets.sentry=${SENTRY} --set secrets.github=${GITHUB} secrets.gitlab=${GITLAB} --values your-values-file.yaml

### Render templates

If you just want to see how the rendered templates would look like:

    make dryrun DEPLOYMENT=[production|staging]
