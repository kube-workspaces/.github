<p align="center">
  <img src="https://raw.githubusercontent.com/kube-workspaces/.github/main/profile/logo.svg" width="80" height="80" alt="Kube Workspaces Logo"/>
</p>

<h1 align="center">Kube Workspaces</h1>

<p align="center">
  <strong>Cloud-native workspace platform for Kubernetes</strong>
</p>

---

Kube Workspaces provides browser-accessible development environments running as pods in your Kubernetes cluster. It manages the full lifecycle of workspaces including creation, proxying, authentication, and resource governance via Custom Resource Definitions.

## Repositories

| Repository | Description |
|-----------|-------------|
| [controller](https://github.com/kube-workspaces/controller) | Kubernetes controller (kubebuilder) — manages Workspace, Image, User, AuthConfig CRDs |
| [api](https://github.com/kube-workspaces/api) | REST API service (Go, Goa v3) — workspace CRUD, auth, image management |
| [proxy](https://github.com/kube-workspaces/proxy) | Reverse proxy (Go) — routes browser traffic to workspace pods |
| [frontend](https://github.com/kube-workspaces/frontend) | Web UI (Next.js, TypeScript) — workspace management dashboard |
| [deploy](https://github.com/kube-workspaces/deploy) | Deployment manifests (Helm, Kustomize, ArgoCD) and documentation |
| [image-catalog](https://github.com/kube-workspaces/image-catalog) | Catalog of `Image` CRs — source of truth for available workspace images |

## Architecture

```
Browser → Ingress → Frontend (Next.js)
                  → API (Goa) → Kubernetes API
                  → Proxy → Workspace Pods
                            Controller ← watches CRDs
```

## Container Images

All images are published to GitHub Container Registry:

- `ghcr.io/kube-workspaces/controller`
- `ghcr.io/kube-workspaces/api`
- `ghcr.io/kube-workspaces/proxy`
- `ghcr.io/kube-workspaces/frontend`

## Quick Start

```bash
# Install CRDs
kubectl apply --server-side -k https://github.com/kube-workspaces/deploy/kustomize/crds

# Deploy all components
kubectl apply --server-side -k https://github.com/kube-workspaces/deploy/kustomize/base

# Or use Helm
helm install kube-workspaces https://github.com/kube-workspaces/deploy/helm/kube-workspaces \
  --namespace kube-workspaces-system --create-namespace
```
