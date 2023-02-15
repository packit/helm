PROJECT ?= packit-prod
CHART ?= ../../helm-charts/import-images/

# Upgrade (or install if doesn't exist) the release/chart with values from $(PROJECT).yaml
# You have to be logged in a cluster
install:
	oc project $(PROJECT)
	helm upgrade $(EXTRA_OPTIONS) --install --cleanup-on-fail import-images $(CHART) --values $(PROJECT).yaml

# Generate the templates on cluster but doesn't perform the upgrade/install
# You have to be logged in a cluster
dryrun:
	make install EXTRA_OPTIONS="--debug --dry-run"

# Generate the templates locally, you don't need to be logged in a cluster
template:
	helm template --debug foobar $(CHART)
