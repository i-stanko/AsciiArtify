# Proof of Concept (PoC) for GitOps Deployment with ArgoCD

## Introduction
The goal of this Proof of Concept (PoC) is to validate the deployment of a GitOps system for the "AsciiArtify" project using ArgoCD. This PoC focuses on setting up a local Kubernetes cluster and installing ArgoCD with access to its web interface to confirm that the system can be successfully deployed and accessed by the team.

## Steps for Deployment

### Setup Kubernetes Cluster
- A local Kubernetes cluster is created using `kind`, which was selected during the Concept phase.
```bash
kind create cluster --name argo
kind get clusters
```

### Install ArgoCD
- ArgoCD is installed into a dedicated namespace using the official installation manifest.
```bash
kubectl create namespace argocd
kubectl get ns

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

kubectl get all -n argocd
kubectl get pods -n argocd
```

### Configure Access to ArgoCD UI
- To access the ArgoCD web interface locally, port forwarding is configured.
```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
- Retrieve the initial **admin password**:
```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```
- The ArgoCD web interface is available at:
    - https://localhost:8080

## Demo Example
The following demo shows successful access to the ArgoCD web interface after installation on a local Kubernetes cluster.
![demo](https://github.com/i-stanko/AsciiArtify/raw/main/assets/peek-argocd.gif)
