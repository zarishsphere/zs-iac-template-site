# zs-iac-template-site

> **Part of:** [ZarishSphere Platform](https://github.com/zarishsphere) | **Layer:** Infrastructure as Code
> **Tools:** OpenTofu 1.11.x · Helm 3.17+ · Kubernetes 1.35 · Argo CD 3.3.x
> **Status:** 🔴 Bootstrap

Site-level deployment template

## ⚠️ Important

**You do not need to run any commands in this repository manually.**
All infrastructure changes are applied automatically via Argo CD 3.3.x (GitOps).
Simply merge a pull request to `main` and the changes deploy automatically.

## Repository Structure

```
zs-iac-template-site/
├── terraform/           # OpenTofu 1.11.x modules
├── helm/                # Helm 3.17+ charts
├── k8s/                 # Raw Kubernetes 1.35 manifests
├── scripts/             # Helper scripts
├── .github/
│   └── workflows/       # OpenTofu plan on PR, apply on merge
└── README.md
```

## GitOps Flow

```
You edit a file here → Open PR → CI validates → You merge → Argo CD 3.3.x applies automatically
```

---

*Part of the [ZarishSphere Platform](https://zarishsphere.com) — Infrastructure as Code, zero manual deploys.*
