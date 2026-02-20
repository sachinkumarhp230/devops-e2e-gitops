# DevOps E2E GitOps Repository (Continuous Delivery Layer)

This repository contains Kubernetes manifests used for GitOps-based deployments to AWS EKS.

It represents the desired state of the application.

ArgoCD continuously monitors this repository and automatically synchronizes changes to the Kubernetes cluster.

---

## 🎯 Responsibilities

This repository is responsible for:

- Kubernetes Deployment manifests
- Environment-specific configuration
- Image tag updates (performed by CI)
- Declarative workload state

This repository does NOT:

- Build Docker images
- Run CI pipelines
- Provision infrastructure
- Access Kubernetes directly via kubectl

---

## 🔁 GitOps Deployment Flow

1. Developer pushes code to the application repository.
2. Jenkins builds a Docker image.
3. Jenkins updates the image tag in this repository.
4. ArgoCD detects the Git change.
5. ArgoCD synchronizes the cluster automatically.
6. Kubernetes deploys the updated version.

Deployment is fully Git-driven.

No manual `kubectl apply` is used.

---

## ⚙️ ArgoCD Configuration

ArgoCD is configured with:

- Automatic Sync enabled
- Prune enabled
- Self-heal enabled

This ensures:

- New image tags are deployed automatically
- Deleted resources are cleaned up
- Drift between cluster and Git is corrected

---

## 📂 Repository Structure

```
devops-e2e-gitops/
└── dev/
    └── app.yaml
```

Future expansion may include:

```
staging/
prod/
```

Each environment will maintain its own declarative manifests.

---

## 🐳 Image Source

Application images are pulled from:

docker.io/sachinaws751/devops-e2e-app

Image tags are automatically updated by the CI pipeline.

---

## 🧠 Design Principles

- Git is the single source of truth.
- CI and CD responsibilities are strictly separated.
- Kubernetes state must always reflect repository state.
- Declarative deployment model.
- No manual cluster mutations.

---

## 🔐 Deployment Strategy

- ArgoCD continuously reconciles desired vs actual state.
- If drift occurs, ArgoCD restores the declared configuration.
- If image tag changes, rollout is triggered automatically.

---

## 🔗 Related Repositories

- Application (CI Layer): `devops-e2e-app`
- Infrastructure (IaC Layer): `devops-e2e-infra`

---

## 🚀 Project Goal

This repository is part of a production-style DevOps platform designed to demonstrate:

- GitOps-based Continuous Delivery
- Automated image promotion
- Clean separation of CI, CD, and infrastructure
- Reproducible Kubernetes deployments

## ArgoCD page

![Uploading image.png…]()

