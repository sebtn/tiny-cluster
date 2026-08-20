
 
#  **Kubernetes orchestration** and **Flux-based GitOps**.

A lightweight, GitOps-native Kubernetes cluster designed for rapid deployment and automated lifecycle management. This repository serves as the single source of truth for infrastructure, leveraging **Flux** to synchronize cluster state with your codebase.

## 💈 A tiny-cluster approach 🏗️ architecture at a Glance

At its core, `tiny-cluster` demonstrates a modern, declarative approach to K8s management:

- **Flux Bootstrapping**: The entire cluster is driven by Flux, enabling **continuous delivery** where code changes automatically propagate to the live environment.
- **Kustomize & Helm Hybrid**: Combines the flexibility of **Kustomize** for base configurations with the package management of **Helm** for complex application stacks.
- **Environment Segregation**: Organized structure (e.g., `clusters/staging`) allows for isolated, repeatable deployments across different stages.
- **Persisted Storage**: Configured to handle stateful workloads with reliable, cluster-wide storage solutions.

## 🔄 The GitOps Workflow

This project eliminates manual `kubectl` commands for production changes. Instead:

1.  **Commit**: Developers push changes to the `main` branch (e.g., updating Helm values or Kustomize overlays).
2.  **Sync**: Flux detects the change and automatically syncs the cluster state to match the repository.
3.  **Verify**: Health checks and monitoring (Grafana) provide immediate visibility into the cluster's health.

## 🛠️ Tech Stack & Tooling

- **Orchestration**: Kubernetes (K8s)
- **GitOps Engine**: Flux (Bootstrap automated via `scripts`)
- **Package Manager**: Helm & Kustomize
- **Dependency Updates**: Mend Renovate (automated security scanning and dependency updates)
- **Local Dev**: `.devcontainer` support and `mise` for managing CLI dependencies (kubectl, helm, flux)
- **CI/CD**: GitHub Actions for Docker image builds and registry pushes

## 🚀 Quick Start

### 1. Bootstrap the Cluster
Initialize Flux within your target Kubernetes cluster:
```bash
./scripts/setup_flux.sh
```

### 2. Configure Environment
Update your environment-specific overlays in the `clusters/staging` directory.

### 3. Deploy
```bash
kustomize build clusters/staging | kubectl apply -f -
```
*Note: Once Flux is active, you can skip manual `kubectl apply` in favor of committing changes to Git.*

## 📂 Repository Structure

| Directory | Purpose |
| :--- | :--- |
| `apps/` | Application-specific Helm charts and configurations |
| `clusters/` | Environment-specific overlays (Staging, Production) |
| `monitoring/` | Observability stack definitions (Prometheus, Grafana) |
| `scripts/` | Automation for Flux bootstrapping and maintenance |
| `.devcontainer` | Pre-configured local development environment |
| `infrastructure/` | Core Kubernetes manifests and Kustomize overlays for cluster-wide resources and environment-specific configurations |

## 🧩 Why Kubernetes + Flux?

By decoupling infrastructure from manual operations, this setup ensures:
- **Auditability**: Every change is versioned and traceable in Git.
- **Resilience**: The cluster self-heals to match the desired state defined in code.
- **Scalability**: Easily replicate the `staging` setup to production with minimal configuration changes.

## 🤝 Contributing

This repository is a core infrastructure component. Changes should be made via Pull Requests to ensure peer review and automated testing before merging to `main`.
