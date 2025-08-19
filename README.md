# helm-brouter-web
Helm charts for [BRouter](https://github.com/abrensch/brouter) and [brouter-web](https://github.com/nrenner/brouter-web)
and an umbrella chart that combines the two.

For local testing, start a [kind](https://kind.sigs.k8s.io/docs/user/quick-start/) cluster and configure `kubectl` accordingly:
```shell
kind create cluster --config kind-config.yaml
kubectl config use-context kind-kind
```

Add the helm repository:
```shell
helm repo add brouter-stack https://joe-akeem.github.io/brouter-helm-stack/
```

List the available charts:
```shell
helm repo update
helm search repo brouter
```

To start the whole stack, including frontend and backend, install the umbrella chart from the helm repository:
```shell
helm install brouter-stack brouter-stack/brouter-stack
```

Installing the helm chart from this GitHub repository:
```shell
helm dependency build ./brouter-stack-charts/brouter-stack
helm install brouter-stack ./brouter-stack-charts/brouter-stack
```

The BRouter app has a sidecar component which downloads routing profile and segment data. To specify which segments
and profiles to download, update `loader.downloadScript` in the `values.yaml`. The files are updated on a regular basis
if needed.

For local testing, setup port forwarding:
```shell
kubectl port-forward service/brouter-stack-brouter-web 8090:80
kubectl port-forward service/brouter-stack 17777:17777
```

When done, delete the kind cluster.
```shell
kind delete cluster
```
