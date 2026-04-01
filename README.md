# Kubernetes Project: Network Inspection + NGINX

This project includes:

- A `network-inspection` deployment and service for in-cluster network troubleshooting.
- An `nginx` deployment and service for a basic web workload.
- A `password-vault-manager` deployment and service using Vaultwarden.

## Structure

- `k8s/network-inspection-deployment.yaml`
- `k8s/network-inspection-service.yaml`
- `k8s/nginx-deployment.yaml`
- `k8s/nginx-service.yaml`
- `k8s/password-vault-secret.yaml`
- `k8s/password-vault-pvc.yaml`
- `k8s/password-vault-deployment.yaml`
- `k8s/password-vault-service.yaml`
- `argocd/network-tools-application.yaml`

## Prerequisites

- `kubectl` configured to your Kubernetes cluster

## Deploy

```bash
kubectl apply -f k8s/
```

## Verify

```bash
kubectl get all
```

## Useful checks

```bash
# Describe resources
kubectl describe deployment network-inspection
kubectl describe deployment nginx
kubectl describe deployment password-vault-manager

# Get service endpoints
kubectl get svc
```

### Access password vault locally

```bash
kubectl port-forward svc/password-vault-manager 8082:80
```

Then open [http://localhost:8082](http://localhost:8082)

## Cleanup

```bash
kubectl delete -f k8s/
```

## Argo CD

An Argo CD `Application` manifest is included at:

- `argocd/network-tools-application.yaml`

Before applying it, update these fields:

- `spec.source.repoURL`
- `spec.source.targetRevision`
- `spec.source.path` (if your manifests are not in `k8s`)

Apply with:

```bash
kubectl apply -f argocd/network-tools-application.yaml
```
