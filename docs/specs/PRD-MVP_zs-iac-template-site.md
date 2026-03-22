# PRD-MVP — `zs-iac-template-site`

> **Document:** Product Requirements (MVP) | **Version:** 1.0.0-mvp
> **Repository:** [https://github.com/zarishsphere/zs-iac-template-site](https://github.com/zarishsphere/zs-iac-template-site)
> **Layer:** Layer 7C — Templates | **Catalog #:** 181
> **Language:** OpenTofu 1.9.1 / Helm 3.17 / YAML | **License:** Apache 2.0

---

## Executive Summary

**Site-level deployment template — fork to add a new health facility.**

This document defines the **Minimum Viable Product (MVP)** scope for `zs-iac-template-site` within the ZarishSphere sovereign digital health platform. It covers what must be built first, acceptance criteria, user stories, and the complete repository file structure.


### Platform Non-Negotiables (apply to every repository)

| Constraint | Rule |
|-----------|------|
| **Zero Cost** | All tooling, hosting, and services must use genuinely free tiers |
| **Open Source** | Apache 2.0 license; all code public |
| **FHIR R5 Native** | All clinical data modelled as FHIR R5 resources |
| **Offline-First** | Must function without network connectivity |
| **No-Coder Friendly** | GUI-first, template-driven, automatable |
| **Documentation as Code** | All decisions in GitHub via RFC/ADR |
| **Multi-tenant** | tenant_id scoping on all data operations |
| **HIPAA/GDPR** | AuditEvent on all PHI access; field-level encryption |

---

## Problem Statement

Adding a new health post requires a repeatable, documented template that non-DevOps staff can follow.

## MVP Goals

1. All infrastructure defined as code; no manual cloud console changes
2. `tofu apply` provisions a working environment from scratch
3. Helm charts deploy all services to Kubernetes
4. Argo CD syncs on every merge to main

## MVP Functional Requirements

| ID | Requirement | Acceptance Criteria | Priority |
|----|------------|---------------------|---------|
| M-01 | `tofu validate` passes on all .tf files | CI validation job passes | P0 |
| M-02 | `tofu fmt -check` passes | No formatting violations | P0 |
| M-03 | Helm lint passes for all charts | `helm lint` exits 0 | P0 |
| M-04 | State stored in Cloudflare R2 | State file visible in R2 bucket | P1 |
| M-05 | Argo CD ApplicationSet defined | App visible in Argo CD UI | P1 |

## MVP OpenTofu Modules

- `module/main`
- `module/variables`
- `module/outputs`

## MVP Complete Repository Tree

```
zs-iac-template-site/
├── README.md
├── LICENSE
├── .gitignore
├── .github/CODEOWNERS
├── .github/workflows/tofu-validate.yml
├── modules/
│   └── (OpenTofu modules)
├── environments/
│   ├── dev/
│   │   ├── main.tf
│   │   └── variables.tf
│   └── prod/
│       ├── main.tf
│       └── variables.tf
└── helm/
    └── (Helm chart overrides)
```

---


## Owners & Governance

| Role | GitHub Handle | Responsibility |
|------|--------------|----------------|
| Platform Lead | `@arwa-zarish` | Final approval, RFC votes |
| Technical Lead | `@code-and-brain` | Architecture, Go/TS review |
| DevOps Lead | `@DevOps-Ariful-Islam` | CI/CD, infra, deployment |
| Health Programs | `@BGD-Health-Program` | Clinical content, country programs |

**PR Policy:** All changes via Pull Request. Minimum 1 owner review. CI must pass. No direct commits to `main`.


---

## MVP Acceptance Checklist

- [ ] All MVP files exist in repository with real content (not placeholders)
- [ ] CI pipeline passes on `main` branch
- [ ] No secrets, credentials, or PHI committed
- [ ] README.md reflects current state with setup instructions
- [ ] CODEOWNERS file present
- [ ] All MVP functional requirements verified manually or via automated tests
- [ ] Linked to `CATALOGS.md` and `TODO.md` in `zs-docs-platform`

---

*This document is the authoritative MVP specification for `zs-iac-template-site`.*
*Changes require a Pull Request with at least 1 owner approval.*
