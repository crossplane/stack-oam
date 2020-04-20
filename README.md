# stack-oam

This stack provisions OAM Workload and Trait definitions to be used in
components.

## Requirements

`stack-oam` only requires that Crossplane be installed in a Kubernetes cluster,
but to use the registered definitions you should install one of the following:

- [addon-oam-kubernetes-local](https://github.com/crossplane/addon-oam-kubernetes-local)
- [addon-oam-kubernetes-remote](https://github.com/crossplane/addon-oam-kubernetes-remote)

## Install

To install `stack-oam`, use a `ClusterStackInstal`:

```yaml
apiVersion: stacks.crossplane.io/v1alpha1
kind: ClusterStackInstall
metadata:
  name: "stack-oam"
  namespace: crossplane-system
spec:
  package: "crossplane/stack-oam:<version>"
```

## Usage

To install all of the Workload and Trait definitions, create a `Definitions`
instance:

```yaml
apiVersion: oam.stacks.crossplane.io/v1alpha1
kind: Definitions
metadata:
  name: oam-defs
```

## Build

`make build`

## Developing Locally

`stack-oam` can be tested locally by installing
[Kind](https://kind.sigs.k8s.io/) and
[Crossplane](https://crossplane.io/docs/v0.9/install.html), then running the
following commands:

```
kind create cluster
make build
kind load docker-image crossplane/stack-oam:local
kubectl apply -f install.yaml
kubectl apply -f example.yaml
```
