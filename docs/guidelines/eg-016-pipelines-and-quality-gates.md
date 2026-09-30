---
id: EG-016
title: "Pipelines and quality gates"
status: draft
owner: "Build and tooling lead"
version: 0.1.0
part: "Code and build"
related: [EG-003, EG-011, EG-013, EG-014, EG-017, EG-021, EG-022]
review-by: 2027-09-30
supersedes:
---

- **Owner:** Build and tooling lead
- **Applies to:** All build, test and release pipelines and their supporting infrastructure
- **Enforcement:** Branch protection, pipeline as code, CODEOWNERS
- **Related:** [EG-003](eg-003-quality-policy-and-attributes.md), [EG-011](eg-011-technology-and-third-party.md), [EG-013](eg-013-coding-standard.md), [EG-014](eg-014-version-control-and-versioning.md), [EG-017](eg-017-testing-principles-and-strategy.md), [EG-021](eg-021-release-update-and-production.md), [EG-022](eg-022-security-and-data-protection.md)

> **Note:** Rules marked *(core)* apply to every product and cannot be tailored. Other rules, and all numeric values, are proposed defaults that a product may tailor in its conformance profile ([EG-001](eg-001-guidelines-governance.md)).

## Purpose

Automate the enforcement of every other guideline in a pipeline that is fast, reproducible, trustworthy and owned.

## Rules

1. **PIP-01** *(core)* Pipelines MUST be defined as code in the repository. Logic MUST live in scripts and the build system, runnable locally with the same command. CI only orchestrates.
1. **PIP-02** *(core)* Toolchains MUST be pinned in versioned container images. Builds MUST be hermetic, with network access limited to declared package caches.
1. **PIP-03** Builds SHOULD be reproducible: the same commit and toolchain produce bit-identical artefacts (no embedded timestamps, `SOURCE_DATE_EPOCH` respected). Reproducibility MUST be verified periodically by rebuild and comparison.
1. **PIP-04** Stages MUST be ordered for fast feedback as in the stage table below. Stages 1 to 4 SHOULD complete within ten minutes.
1. **PIP-05** *(core)* Artefacts MUST be built once and promoted. The artefact that is tested MUST be the artefact that is released. It is stored immutably with metadata (commit, pipeline run, toolchain digest).
1. **PIP-06** Gates MUST be applied by branch type as in the gates table below.
1. **PIP-07** Mandatory gate content MUST include: warnings as errors, analyser thresholds, size and timing budget checks (AP-06), coverage that does not decrease, documentation build, requirement trace check, licence and SBOM check and secret scanning.
1. **PIP-08** *(core)* Gates MUST NOT be bypassed. An override needs a recorded exception (GOV-09) approved by the pipeline owner.
1. **PIP-09** A flaky test MUST be quarantined within one working day of detection, with an owner and a fix deadline (proposed ten working days). Quarantined tests are tracked and the flaky rate is reported.
1. **PIP-10** A broken `main` is the top priority. The policy is revert first, and `main` MUST be restored within one working day.
1. **PIP-11** The pipeline MUST have a named owner, a rotation for breakage response and service levels. Pipeline changes MUST go through PR with CODEOWNERS review.
1. **PIP-12** Each release build MUST produce supply chain outputs: SBOM, signed artefacts and provenance attestation, retained under the retention policy ([EG-021](eg-021-release-update-and-production.md)).
1. **PIP-13** *(core)* Repository settings, branch protection and required checks MUST be held as code and applied by tooling (policy as code).
1. **PIP-14** Shared HIL rigs MUST be accessed through the pipeline with booking or queueing, health checks and recorded results ([EG-017](eg-017-testing-principles-and-strategy.md)).
1. **PIP-15** Pipeline duration, queue time and failure reasons MUST be monitored, and used to keep feedback fast.
1. **PIP-16** Pipeline credentials MUST be least-privilege and short-lived. Release signing MUST use protected keys and follow the two-person rule ([EG-022](eg-022-security-and-data-protection.md)).

## Stages

```mermaid
flowchart LR
  A[Commit and format lint] --> B[Build all targets]
  B --> C[Host unit tests]
  C --> D[Static analysis]
  D --> E[Integration and simulation]
  E --> F[HIL tests]
  F --> G[System and soak nightly]
  G --> H[Package sign and evidence]
```

## Gates by branch type

| Branch type | Required stages |
|-------------|-----------------|
| Feature branch | Commit lint, build, unit tests, static analysis |
| `main` | All of the above, plus integration, simulation and HIL |
| Release candidate | All stages, plus system and soak, trace report, SBOM, signing and the evidence pack |

## Compliance

| Rule | Checked by |
|------|------------|
| PIP-01, PIP-02 | Review of pipeline definitions, container digests in repository |
| PIP-03 | Scheduled rebuild-and-compare job |
| PIP-07, PIP-08 | Branch protection required checks |
| PIP-09, PIP-15 | Pipeline metrics report |
| PIP-13 | Policy as code drift check |

## Checklist

Tick an item when it is true for your project. Rule IDs point to the detail above.

- [ ] The pipeline is defined as code, with logic in scripts that run locally by the same command (PIP-01)
- [ ] Toolchains are pinned in versioned container images and builds are hermetic (PIP-02)
- [ ] Reproducibility is verified periodically (PIP-03)
- [ ] Stages are ordered for fast feedback and stages 1 to 4 finish within ten minutes (PIP-04)
- [ ] Artefacts are built once, promoted and stored immutably with metadata (PIP-05)
- [ ] Gates are defined by branch type (PIP-06)
- [ ] Mandatory gate content is present: warnings, analysis, budgets, coverage, docs, trace, licence and SBOM, secrets (PIP-07)
- [ ] Gates cannot be bypassed without a recorded exception (PIP-08)
- [ ] Flaky tests are quarantined within one working day (PIP-09)
- [ ] The policy is revert first, and `main` is restored within one working day (PIP-10)
- [ ] The pipeline has an owner, a rotation and service levels (PIP-11)
- [ ] SBOM, signed artefacts and provenance are produced per release (PIP-12)
- [ ] Repository settings and required checks are held as code (PIP-13)
- [ ] Shared HIL rigs are accessed through the pipeline (PIP-14)
- [ ] Pipeline duration, queue time and failure reasons are monitored (PIP-15)
- [ ] Credentials are least-privilege and short-lived, and release signing uses the two-person rule (PIP-16)

## Applying to personal projects and AI agents

### Personal projects

Starts at the **Standard** profile (see [personal-projects.md](personal-projects.md)). Use one workflow that runs the same `make` targets as your machine: format check, build, tests, lint and secret scan. Pin the toolchain with a container or lockfile. Skip rotations, service levels and HIL queueing.

### AI agents

- Do not modify pipeline definitions, required checks or gates unless the task says so (AGT-05).
- Never skip, disable or loosen a check or test to make a pipeline pass (PIP-08, TST-15).
- Run the same commands CI runs before proposing a change (PIP-01).
- If a test is flaky, report it and do not delete it (PIP-09).
- If your change breaks `main`, revert first (PIP-10).
