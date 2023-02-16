# Values

This directory contains customized value files for each [chart](../helm-charts).
They are passed to the `helm upgrade` command with `--values` flag when the chart is installed/upgraded.

There are `README`s and `make` targets to help you if you want to experiment
with installing/upgrading the charts manually.

But in most cases, CD (continuous delivery) will do that for you automatically
so all you need to do is just edit the values (YAML) files.
