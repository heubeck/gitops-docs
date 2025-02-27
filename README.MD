# GitOps with Flux, a basic setup

The following referes to [this repository](https://github.com/heubeck/gitops-flux-basic).

## Local k8s kind cluster

* [Install k8s kind](https://kind.sigs.k8s.io/docs/user/quick-start/#installation)

```shell
# Create new cluster and configure kubectl
kind create cluster --config ./kind/config.yaml && kind export kubeconfig --kubeconfig /home/heubeck/.kube/config

# Destroy it
kind delete cluster
```

## Flux

* [Install flux cli](https://fluxcd.io/docs/cmd/#install-using-bash)

```shell
# Bootstrap
export GITHUB_TOKEN=...
flux bootstrap github --owner=heubeck --repository=gitops-flux-basic --private=false --personal=true
```

## Linkerd

* [Install linkerd cli](https://linkerd.io/2.11/getting-started/#step-1-install-the-cli)
* [Install linkerd smi extension](https://linkerd.io/2.11/tasks/linkerd-smi/)

## Access components

* [Examiner](https://github.com/heubeck/examiner) - Bound to ingress: GET http://localhost/examine
* Prometheus - Port forwarding: `kubectl port-forward -n monitoring svc/prometheus-operated 9090:9090`
* Linkerd Viz - Port forwarding: `kubectl port-forward -n linkerd-viz svc/web 8084:8084` or with cli: `linkerd viz dashboard`
