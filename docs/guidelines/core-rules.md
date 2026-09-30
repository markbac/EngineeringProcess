---
title: "Core rules"
status: draft
owner: "Architecture group"
last-reviewed: 2026-09-29
---

## Purpose

Core rules apply to every product without tailoring. They are the small set of rules whose value comes from being the same everywhere: traceability, commit and version conventions, secrets, supply chain and AI agent controls. Everything else is a default that a product may tailor through its conformance profile (GOV-15, GOV-16).

There are 61 core rules out of 347 in total. The full wording, rationale and compliance checks are in each guideline. Core rules are marked *(core)* there.

## How core rules change

- A new core rule or a change to one needs an RFC ([EG-008](eg-008-decision-records.md)) with every product's technical lead consulted, and a MAJOR or MINOR version change to the guideline (GOV-12).
- A product cannot tailor a core rule. A time-limited exception needs the guideline owner's approval (GOV-09).
- If products keep asking for exceptions to a core rule, the rule is probably wrong. Review it.

## Core rules by guideline

### [EG-001 Guidelines governance](eg-001-guidelines-governance.md)

- **GOV-01** Every guideline MUST have a unique ID (`EG-nnn`), a named owner, a status (`draft`, `active`, `deprecated`), a version and a review-by date in its front matter.
- **GOV-06** New guidelines and material changes MUST go through an RFC ([EG-008](eg-008-decision-records.md)), unless the change is editorial.
- **GOV-07** Changes MUST be made by pull request, approved by the owner and by at least one practitioner subject to the rule.
- **GOV-09** A deviation MUST be recorded as an exception with owner approval, scope, reason and expiry date. A permanent deviation means the rule is wrong and SHOULD be changed.
- **GOV-15** Rules MUST be classified as core or tailorable. Core rules apply to every product without tailoring and are marked *(core)*. All other rules, and all numeric values, are defaults that a product MAY tailor through its conformance profile (GOV-16). The core set is kept small so that products stay consistent where it matters and free elsewhere.
- **GOV-16** Each product MUST have a conformance profile recording which guidelines apply, any tailored rules and values with the reason, approved exceptions, the components it uses and provides (COM-01), and its toolchain. The product's technical lead owns the profile and approves tailoring of non-core rules, and the architecture group is informed at its forum (RFC-11). Exceptions to core rules need the guideline owner's approval (GOV-09).

### [EG-004 Documentation as code and terminology](eg-004-documentation-as-code.md)

- **DOC-01** Documentation MUST be stored as plain text in the same repository as the thing it describes, or in a designated documentation repository referenced from it.
- **DOC-03** Changes to documentation MUST go through the same PR and review process as code.
- **DOC-04** A change that alters behaviour, an interface, a configuration option or a build step MUST update the affected documentation in the same PR.
- **DOC-08** Each repository MUST provide the minimum document set: `README`, `CONTRIBUTING`, `AGENTS.md`, architecture overview, build and test instructions, and `docs/adr/`.

### [EG-005 AI agent usage](eg-005-ai-agent-usage.md)

- **AGT-01** Every repository MUST have an `AGENTS.md` at its root, reviewed and owned like code.
- **AGT-03** Agent-authored changes MUST follow the same commit, PR, review and CI rules as human changes. There is no fast lane.
- **AGT-04** An agent MUST NOT approve or merge its own changes. At least one human reviewer who understands the change MUST approve.
- **AGT-05** Agents MUST NOT act in the areas listed in the boundaries table (below) without explicit human instruction in the task.
- **AGT-06** AI-assisted commits MUST carry a trailer, for example `Assisted-by: <tool>`, so that the extent of assistance is auditable.
- **AGT-07** Humans are accountable for all code they submit, whoever or whatever wrote it. The submitter MUST understand and be able to explain the change.
- **AGT-08** Data MUST NOT be sent to an agent service that is not approved for its classification ([EG-022](eg-022-security-and-data-protection.md)). The approved tools and their permitted data classes are held in one place, owned by the security lead.

### [EG-006 Requirements and traceability](eg-006-requirements-and-traceability.md)

- **REQ-03** Requirements MUST be stored as text in the repository beside the design, with stable IDs of the form `REQ-<AREA>-<nnnn>`. IDs are never reused.
- **REQ-06** Requirement IDs MUST be referenced in commit footers, PR descriptions, test names and, where non-obvious, code comments and ADRs.

### [EG-008 Decision records: RFCs and ADRs](eg-008-decision-records.md)

- **ADR-01** ADRs MUST be stored in `docs/adr/` in the repository they affect, numbered sequentially and named `NNNN-short-title.md`.
- **ADR-03** An ADR MUST be proposed by PR. Merging with status `accepted` is the record of approval.
- **ADR-04** An accepted ADR MUST be immutable apart from status and links. A changed decision is a new ADR that supersedes the old one, and the old ADR MUST be updated to point to it.
- **RFC-01** An RFC MUST be used for new or changed guidelines, cross-team interface changes, adoption of major tools or dependencies, and changes to the release or update process.

### [EG-010 Components, reuse and variants](eg-010-components-reuse-and-variants.md)

- **COM-01** Every component MUST be listed in a component register recording its owner, deputy, repository, current version, status (`active`, `maintenance`, `deprecated`, `retired`) and consumers. Third-party components are listed with the same fields ([EG-011](eg-011-technology-and-third-party.md)). A product keeps its own register, or uses a shared register where products share components.
- **COM-02** Every component MUST have a named owner and a deputy. A component with no owner MUST be escalated to the architecture group within one month.
- **COM-03** Consumers MUST depend on released, versioned artefacts. They MUST NOT depend on a branch, an unreleased commit or a copy of the source.

### [EG-011 Technology selection and third-party components](eg-011-technology-and-third-party.md)

- **TEC-03** A licence policy MUST list approved licences and prohibited ones. Any other licence needs legal review before use.
- **TEC-04** All third-party components MUST be recorded in a manifest (name, version, source, licence, checksum, owner). An SBOM MUST be generated for each release.
- **TEC-05** Versions MUST be pinned and checksums verified. Floating versions and unpinned downloads in builds MUST NOT be used.

### [EG-012 Coding principles](eg-012-coding-principles.md)

- **CPR-01** The coding standard MUST derive from these principles, and each of its rules SHOULD cite the principle it serves.

### [EG-013 Coding standard](eg-013-coding-standard.md)

- **COD-01** The team MUST maintain one coding standard per language in use (for example C, C++, Python, shell, build scripts). Each MUST derive from the coding principles ([EG-012](eg-012-coding-principles.md)), and each rule MUST have an ID and cite the principle it serves.
- **COD-04** Formatting MUST be applied by a formatter, not by hand. Its configuration lives in the repository, and CI checks it.
- **COD-05** Static analysis tools, rule sets and severities MUST be configured in the repository and pinned. Warnings MUST be errors. Suppressions MUST be inline, carry the rule ID and a justification, and be audited.

### [EG-014 Version control, commits and versioning](eg-014-version-control-and-versioning.md)

- **VCS-01** Git MUST be the single source of truth. The repository structure MUST be documented, and the choice of monorepo or multi-repo (with its multi-repo tool) recorded in an ADR. Large binaries MUST use LFS or an artefact store. Secrets and build outputs MUST NOT be committed.
- **VCS-03** Commit messages MUST follow Conventional Commits, using the allowed types (below) and scopes mapped to components in a scope file.
- **VCS-04** A breaking change MUST be marked with `!` and a `BREAKING CHANGE:` footer.
- **VCS-05** Footers MUST include `Refs:` for requirement or ticket IDs. They SHOULD include `ADR:` where relevant, and MUST include `Assisted-by:` where AI assisted (AGT-06).
- **VCS-07** Commit format MUST be enforced by a commit-msg hook (installed by one command) and by a CI lint.
- **VCS-08** `main` MUST have linear history through squash or rebase merging. Force-push to shared branches MUST NOT be used. History rewriting is allowed only on your own unmerged branches.
- **VCS-09** Firmware versions MUST follow semantic versioning as defined below.
- **VCS-10** The version MUST have a single source, derived from the Git tag by the build and injected into the artefact. Version strings MUST NOT be edited by hand. Builds MUST embed the commit hash and a dirty flag, and the device MUST report its version.
- **VCS-11** Release tags MUST be annotated, signed, immutable, and named `vX.Y.Z` (pre-releases `vX.Y.Z-rc.N`). Tags trigger the release pipeline.

### [EG-015 Pull requests and code review](eg-015-pull-requests-and-review.md)

- **PRR-01** All changes to protected branches MUST be made by PR. Direct pushes MUST NOT be allowed, including for owners.
- **PRR-02** The PR title MUST follow Conventional Commits and becomes the squash commit message.
- **PRR-05** CODEOWNERS MUST define required reviewers for each path. At least one owner approves every PR, and safety, security and certified areas need two.
- **PRR-06** Reviewers MUST be someone other than the author who understands the area. An agent MUST NOT count as an approver (AGT-04).

### [EG-016 Pipelines and quality gates](eg-016-pipelines-and-quality-gates.md)

- **PIP-01** Pipelines MUST be defined as code in the repository. Logic MUST live in scripts and the build system, runnable locally with the same command. CI only orchestrates.
- **PIP-02** Toolchains MUST be pinned in versioned container images. Builds MUST be hermetic, with network access limited to declared package caches.
- **PIP-05** Artefacts MUST be built once and promoted. The artefact that is tested MUST be the artefact that is released. It is stored immutably with metadata (commit, pipeline run, toolchain digest).
- **PIP-08** Gates MUST NOT be bypassed. An override needs a recorded exception (GOV-09) approved by the pipeline owner.
- **PIP-13** Repository settings, branch protection and required checks MUST be held as code and applied by tooling (policy as code).

### [EG-017 Testing principles and strategy](eg-017-testing-principles-and-strategy.md)

- **TST-03** Test names or metadata MUST include the requirement IDs they verify (REQ-06). The verification method recorded for each requirement MUST be executed.
- **TST-07** Every fixed defect MUST have a regression test (DEF-04). The regression suite MUST run on every merge to `main`.

### [EG-018 Defect and technical debt management](eg-018-defects-and-technical-debt.md)

- **DEF-01** All defects MUST be recorded in the tracker. Private lists MUST NOT be used. A record includes version found, environment, steps, expected and actual results, severity, component, linked requirement and logs or dumps.
- **DEF-02** Severity MUST follow the definitions below. Priority is set separately by the product owner.

### [EG-021 Release, update and production](eg-021-release-update-and-production.md)

- **REL-02** A release candidate MUST be a tagged commit built once by the pipeline. Only that artefact is promoted (PIP-05).
- **REL-05** Release notes MUST be generated from conventional commits and closed defects, and MUST include breaking changes, upgrade notes and known issues.

### [EG-022 Security and data protection](eg-022-security-and-data-protection.md)

- **SEC-03** Only approved cryptographic algorithms and vetted libraries MUST be used, from a list owned by the security lead. Home-grown cryptography MUST NOT be used.
- **SEC-05** Secrets MUST NOT be in source. Secret scanning MUST run pre-commit and in CI. A leaked secret is an incident and MUST be rotated.
- **SEC-08** Vulnerability management MUST have an intake channel, a coordinated disclosure policy, severity assessment and patch times by severity (below). The SBOM MUST be monitored against vulnerability feeds.
- **SEC-10** A data classification scheme MUST be in place (below), with handling rules for storage, logs, telemetry, sharing and AI tools.
