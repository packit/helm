# Helm charts

Each directory consists of:
* [Chart.yaml](https://helm.sh/docs/topics/charts/#the-chartyaml-file) -
  Don't forget to bump the [version](https://helm.sh/docs/topics/charts/#charts-and-versioning)
  there if you want to release a new chart version.
* [templates/](https://helm.sh/docs/topics/charts/#template-files) -
  Go templates with Kubernetes/OpenShift workflows,
  see [best practices](https://helm.sh/docs/chart_best_practices/templates).
* [values.yaml](https://helm.sh/docs/topics/charts/#values-files) -
  Default values to be used in `templates/`,
  see [this guide](https://helm.sh/docs/chart_template_guide/values_files)
  and [best practices](https://helm.sh/docs/chart_best_practices/values).
  There's also [values/](../values) with customized values.
