# TECH-DESIGN-MVP — `zs-iac-template-site`

> **Document:** Technical Design (MVP) | **Version:** 1.0.0-mvp
> **Repository:** [https://github.com/zarishsphere/zs-iac-template-site](https://github.com/zarishsphere/zs-iac-template-site)
> **Layer:** Layer 7C — Templates | **Catalog #:** 181
> **Language:** OpenTofu 1.9.1 / Helm 3.17 | **License:** Apache 2.0

---

## Technical Summary

**Site-level deployment template — fork to add a new health facility.**

This document defines the **technical architecture, implementation design, complete repository tree, and acceptance criteria** for the MVP of `zs-iac-template-site`.

---

## OpenTofu Backend (Cloudflare R2)

```hcl
# environments/prod/backend.tf
terraform {
  backend "s3" {
    bucket                      = "zarishsphere-tofu-state"
    key                         = "zs-iac-template-site/prod/terraform.tfstate"
    region                      = "auto"
    endpoint                    = "https://ACCOUNT_ID.r2.cloudflarestorage.com"
    skip_credentials_validation = true
    skip_metadata_api_check     = true
    skip_region_validation      = true
    force_path_style            = true
  }
}
```

## CI/CD Validation

```yaml
name: OpenTofu Validate
on: [push, pull_request]
jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: opentofu/setup-opentofu@v1
        with: {tofu_version: 1.9.1}
      - run: tofu init -backend=false
      - run: tofu validate
      - run: tofu fmt -check -recursive
  helm-lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: azure/setup-helm@v3
      - run: helm lint helm/
```

## Repository Tree

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
