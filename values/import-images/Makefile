PROJECT ?= packit-prod

install:
	oc project $(PROJECT)
	helm upgrade $(EXTRA_OPTIONS) --install --cleanup-on-fail import-images ../../helm-charts/import-images/ --values $(PROJECT).yaml

dryrun:
	make install EXTRA_OPTIONS="--debug --dry-run"
