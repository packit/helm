DEPLOYMENT ?= production
CHART ?= ../../helm-charts/packit-service-validation/

# Upgrade (or install if doesn't exist) the release/chart with values from $(DEPLOYMENT).yaml
# You have to be logged in a cluster
install:
	helm upgrade $(EXTRA_OPTIONS) --install --cleanup-on-fail \
		packit-$(DEPLOYMENT)-validation $(CHART) \
		--set-string "secrets.sentry=$${SENTRY}" \
		--set-string "secrets.github=$${GITHUB}" \
		--set-string "secrets.gitlab=$${GITLAB}" \
		--set-string "secrets.gitlabgnome=$${GITLAB_GNOME}" \
		--set-string "secrets.gitlabfreedesktop=$${GITLAB_FREEDESKTOP}" \
		--set-string "secrets.salsadebian=$${SALSA_DEBIAN}" \
		--set-string "secrets.pagure_token=$${PAGURE_TOKEN}" \
		--set-string "secrets.pagure_ssh_key=$${PAGURE_SSH_KEY}" \
		--set-string "secrets.pagure_keytab=$${PAGURE_KEYTAB}" \
		--values $(DEPLOYMENT).yaml

# Generate the templates on cluster but doesn't perform the upgrade/install
# You have to be logged in a cluster
dryrun:
	make install EXTRA_OPTIONS="--debug --dry-run"

# Generate the templates locally, you don't need to be logged in a cluster
template:
	helm template --debug foobar $(CHART)
