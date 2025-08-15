# helm-brouter-web
Helm charts for [BRouter](https://github.com/abrensch/brouter) and [brouter-web](https://github.com/nrenner/brouter-web)
and an umbrella chart that combines the two.

For local testing, start a [kind](https://kind.sigs.k8s.io/docs/user/quick-start/) cluster and configure `kubectl` accordingly:
```shell
kind create cluster --config kind-config.yaml
kubectl config use-context kind-kind
```

Create a persistent volume to save the routing profiles that are used by BRouter and BRouter Web.
For testing the `profiles-pv.yaml` manifest can be used. Also create a persistent volume claim that
can be used by both, BRouter and BRouter Web.
```shell
kubectl apply -f profiles-pv.yaml
kubectl apply -f profiles-pvc.yaml
```

Add the helm repository:
```shell
helm repo add brouter-web https://joe-akeem.github.io/brouter-helm-stack/
```

List the available charts:
```shell
helm search repo brouter
```

To start the whole stack, including frontend and backend, install the umbrella chart from the repository:
```shell
helm install brouter-stack brouter/brouter-stack
```

The BRouter app has a sidecar component which downloads routing profile and segment data. To specify which segments
and profiles to download, update `loader.downloadScript` in the `values.yaml`. The files are updated on a regular basis
if needed. Update `loader.intervalSeconds` to change the update interval.

For local testing, setup port forwarding:
```shell
kubectl port-forward service/brouter-web 8090:80
kubectl port-forward service/brouter 17777:17777
```

When done, delete the kind cluster.
```
kind delete cluster
```
