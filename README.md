# helm-brouter-web
A Helm chart for brouter-web (https://github.com/nrenner/brouter-web)

Add the helm repository:
```shell
helm repo add brouter-web https://joe-akeem.github.io/helm-brouter-web/
```

List the available charts:
```shell
helm search repo brouter
```

The BRouter app has a sidecar component which downloads routing profile and segment data. To specify which segments
and profiles to download, update `loader.downloadScript` in the `values.yaml`. The files are updated on a regular basis
if needed. Update `loader.intervalSeconds` to change the update interval.
