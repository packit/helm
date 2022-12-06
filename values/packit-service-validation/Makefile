DEPLOYMENT ?= production

install:
	helm upgrade $(EXTRA_OPTIONS) --install --cleanup-on-fail packit-$(DEPLOYMENT)-validation ../../helm-charts/packit-service-validation/ --set secrets.sentry=${SENTRY} --set secrets.github=${GITHUB} --values $(DEPLOYMENT).yaml

dryrun:
	make install EXTRA_OPTIONS="--debug --dry-run"
