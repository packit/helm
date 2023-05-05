DEPLOYMENT ?= production
CHART ?= ../../helm-charts/packit-service-validation/

# Upgrade (or install if doesn't exist) the release/chart with values from $(DEPLOYMENT).yaml
# You have to be logged in a cluster
install:
	helm upgrade $(EXTRA_OPTIONS) --install --cleanup-on-fail packit-$(DEPLOYMENT)-validation $(CHART) --set secrets.sentry=${SENTRY} --set secrets.github=${GITHUB} --set secrets.gitlab=${GITLAB} --set secrets.gitlabgnome=${GITLAB_GNOME} --set secrets.gitlabfreedesktop=${GITLAB_FREEDESKTOP} --set secrets.salsadebian=${SALSA_DEBIAN} --values $(DEPLOYMENT).yaml

# Generate the templates on cluster but doesn't perform the upgrade/install
# You have to be logged in a cluster
dryrun:
	make install EXTRA_OPTIONS="--debug --dry-run"

# Generate the templates locally, you don't need to be logged in a cluster
template:
	helm template --debug foobar $(CHART)
