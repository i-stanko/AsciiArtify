# Proof of Concept (PoC) for GitOps Deployment with ArgoCD

## Introduction
The goal of this Proof of Concept (PoC) is to demonstrate the feasibility of deploying the GitOps system for the "AsciiArtify" project using ArgoCD. The PoC will involve setting up a Kubernetes cluster and configuring ArgoCD to enable continuous deployment of the application.

## Steps for Deployment

- ### Setup Kubernetes Cluster
```
kind create cluster --name argo
kind get clusters
```

- ### Install ArgoCD
```
k create namespace argocd
k get ns
k apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

k get all -n argocd
k get pods -n argocd
```

- ### Configure Access
```
k port-forward svc/argocd-server -n argocd 8080:443
```

```
k -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```

## Demo Example

![demo](assets/peek-argocd.gif)
