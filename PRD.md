# PRD — `zs-iac-template-site`

> **Document Class:** PRD | **Version:** 1.0.0 | **Status:** Bootstrapping
> **Repository:** [https://github.com/zarishsphere/zs-iac-template-site](https://github.com/zarishsphere/zs-iac-template-site)
> **Layer:** Layer 7 — Infrastructure as Code | **Catalog #:** 181
> **License:** Apache 2.0 | **Governance:** RFC-0001

---

## 1. Overview

Site-level deployment template — fork to provision a new health facility.

---

## 2. Repository Metadata

- **Name:** `zs-iac-template-site`
- **Organization:** [https://github.com/zarishsphere](https://github.com/zarishsphere)
- **Language / Runtime:** OpenTofu / Helm / YAML
- **Visibility:** Public
- **License:** Apache 2.0
- **Default Branch:** `main`
- **Branch Protection:** Required (2-owner review for critical paths)

---

## 3. Platform Context

This repository is part of the **ZarishSphere** sovereign digital health operating platform — a free, open-source, FHIR R5-native system for South and Southeast Asia.

**Non-negotiable constraints:**
- Zero cost — all tooling must use genuinely free tiers
- FHIR R5 native — all clinical data modelled as FHIR R5 resources
- Offline-first — must work without network connectivity
- No-coder friendly — GUI-first, template-driven
- Documentation as Code — all decisions in GitHub

---

## 4. Goals & Objectives

- Manage template-site infrastructure as code using OpenTofu and Helm
- Enable one-command environment provisioning
- Enforce GitOps: all changes via PR → Argo CD sync

## 5. Functional Requirements

| ID | Requirement | Priority |
|----|------------|---------|
| F-01 | OpenTofu modules for all infrastructure components | P0 |
| F-02 | Helm charts for all Kubernetes workloads | P0 |
| F-03 | Argo CD ApplicationSet for GitOps deployment | P0 |
| F-04 | Environment separation (dev/staging/prod) | P0 |
| F-05 | OpenTofu state stored in Cloudflare R2 | P1 |
| F-06 | Automated `tofu validate` on every PR | P0 |
| F-07 | Cost estimation in PR comments | P2 |

## 6. Repository Tree

```
zs-iac-template-site/
├── README.md
├── LICENSE
├── .gitignore
├── .github/
│   ├── CODEOWNERS
│   └── workflows/
│       └── tofu-validate.yml          # tofu init + validate + fmt check
├── modules/
│   └── (OpenTofu reusable modules)
├── environments/
│   ├── dev/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── terraform.tfvars
│   ├── staging/
│   │   ├── main.tf
│   │   └── variables.tf
│   └── prod/
│       ├── main.tf
│       └── variables.tf
├── helm/
│   └── (Helm chart overrides per environment)
├── argocd/
│   └── (Argo CD Application manifests)
└── docs/
    └── ARCHITECTURE.md                # Infrastructure diagram
```

## 9. Ownership & Governance

| Role | GitHub User |
|------|-------------|
| Platform Lead | `@arwa-zarish` |
| Technical Lead | `@code-and-brain` |
| DevOps Lead | `@DevOps-Ariful-Islam` |
| Health Programs | `@BGD-Health-Program` |

All changes go through Pull Request → 1+ owner review → CI pass → merge.
Breaking changes require RFC + ADR.

---

## 10. Definition of Done

- [ ] All listed files exist with content
- [ ] CI pipeline passes (test + lint + security)
- [ ] README.md reflects current state
- [ ] OpenAPI / AsyncAPI spec present (services only)
- [ ] At least 1 integration test using testcontainers-go (Go) or Playwright (UI)
- [ ] No secrets committed (GitGuardian verified)
- [ ] CODEOWNERS file present
- [ ] Linked to CATALOGS.md and TODO.md

---

*This PRD is the canonical source of truth for this repository's purpose, structure, and requirements.*
*Changes require a PR against this file with owner approval.*
