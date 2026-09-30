---
title: "Combined checklists"
status: draft
owner: "Project owner"
last-reviewed: 2026-09-29
---

## How to use these checklists

Each guideline has its own checklist at the end of its file. This file combines them. Tick an item when it is true for your project.

- **Adoption:** the unticked items are what is left to set up.
- **Assessment:** the percentage ticked per guideline shows where you are strong or weak.
- **Review:** revisit before each release and at each guideline review.

For a personal project, use only the guidelines in your profile (see [personal-projects.md](personal-projects.md)). Copy a section into an issue or PR description to track it.

## [EG-001 Guidelines governance](eg-001-guidelines-governance.md)

Profile: Standard. Owner: Architecture group.

- [ ] Guidelines live in `docs/guidelines/`, one file per guideline, named `eg-nnn-short-title.md` (GOV-13)
- [ ] Every guideline has front matter with id, title, status, owner, version and review-by (GOV-01)
- [ ] Every guideline follows the standard template and states how compliance is checked (GOV-02, GOV-04)
- [ ] Rules have stable IDs and RFC 2119 keywords, with a rationale where it is not obvious (GOV-03)
- [ ] Each guideline is short enough to read in one sitting, with examples where they help (GOV-05, GOV-11)
- [ ] Changes are made by PR with owner and practitioner approval, and by RFC when material (GOV-06, GOV-07)
- [ ] Review-by dates are checked by CI and no guideline is overdue (GOV-08)
- [ ] Exceptions are recorded with owner, scope, reason and expiry (GOV-09)
- [ ] Deprecated guidelines are kept with a pointer to their replacement (GOV-10)
- [ ] Guideline versions follow semantic versioning (GOV-12)
- [ ] The index is generated from front matter (GOV-13)
- [ ] Each guideline has an accountable owner who handles questions and exception requests (GOV-14)
- [ ] Core rules are marked and applied identically across products, and all other rules are tailored only through the product profile (GOV-15)
- [ ] Each product has a conformance profile recording applicability, thresholds, exceptions, components and toolchain (GOV-16)

## [EG-002 Engineering values and ways of working](eg-002-values-and-ways-of-working.md)

Profile: Full. Owner: Engineering manager.

- [ ] Values are published and used as tie-breakers (VAL-01)
- [ ] Every component, pipeline, rig and tool has a named owner in CODEOWNERS or the ownership register (VAL-02)
- [ ] The decision rights table is current (VAL-03)
- [ ] Escalation steps and time limits are agreed, and decisions are committed to once made (VAL-04, VAL-05)
- [ ] Decisions, agreements and meeting outcomes are written down within one working day (VAL-06)
- [ ] Each component has an owning site and a deputy at another site (VAL-07)
- [ ] Cross-site agreements cover overlap hours, response time and the handover note (VAL-08)
- [ ] All sites use the same tools and conventions, and variants have an ADR (VAL-09)
- [ ] Work status is visible in the tracker and pipeline (VAL-10)
- [ ] Changes are small enough to review within one working day (VAL-11)
- [ ] Raising a risk, disagreement or mistake is treated as expected behaviour (VAL-12)

## [EG-003 Quality policy and quality attributes](eg-003-quality-policy-and-attributes.md)

Profile: Standard. Owner: Test and quality lead.

- [ ] A one-page quality policy is published (QUA-01)
- [ ] A quality attribute model exists with definitions and example measures (QUA-02)
- [ ] Each product has a ranked quality attribute profile, approved by the architecture lead and product owner (QUA-03)
- [ ] Quality attributes are stated as measurable scenarios in requirements (QUA-04)
- [ ] An NFR catalogue exists and requirements are selected from it (QUA-05)
- [ ] There is no separate quality phase, the gates are the quality controls (QUA-06)
- [ ] Each release has quality evidence in its evidence pack (QUA-07)
- [ ] The model and objectives are reviewed annually using field data (QUA-08)

## [EG-004 Documentation as code and terminology](eg-004-documentation-as-code.md)

Profile: Starter. Owner: Build and tooling lead.

- [ ] Documents are plain-text Markdown in the repository and linted (DOC-01, DOC-02)
- [ ] Documentation changes go through PR like code (DOC-03)
- [ ] Changes to behaviour, interfaces, configuration and build steps update docs in the same PR (DOC-04)
- [ ] Diagrams are Mermaid or PlantUML source (DOC-05)
- [ ] Every document has front matter with owner, status and review date (DOC-06)
- [ ] CI builds the docs, fails on broken links and lint errors, and publishes versioned docs with each release (DOC-07)
- [ ] The minimum document set exists: README, CONTRIBUTING, `AGENTS.md`, architecture overview, build and test instructions, `docs/adr/` (DOC-08)
- [ ] Generated docs are generated and never hand-edited (DOC-09)
- [ ] Documents state their question and audience, and are split by purpose (DOC-10)
- [ ] Writing is plain British English with the conclusion first (DOC-11)
- [ ] A single glossary exists and terms are used consistently (DOC-12)
- [ ] Naming conventions are followed for files, IDs and components (DOC-13)
- [ ] Approval is PR approval unless a regulation requires a signature record (DOC-14)
- [ ] Documents are structured with headings, front matter and IDs so people and agents can navigate them (DOC-15)

## [EG-005 AI agent usage](eg-005-ai-agent-usage.md)

Profile: Starter. Owner: Build and tooling lead and Security lead.

- [ ] `AGENTS.md` exists at the repository root with commands, conventions, boundaries and definition of done (AGT-01, AGT-02)
- [ ] Agent changes follow the same commit, PR, review and CI rules as human changes (AGT-03)
- [ ] A human approves every agent-authored change, and agents never approve or merge their own work (AGT-04)
- [ ] Agent boundaries are protected by CODEOWNERS or branch protection (AGT-05)
- [ ] AI-assisted commits carry an `Assisted-by:` trailer (AGT-06)
- [ ] The submitter understands and can explain every line submitted (AGT-07)
- [ ] An approved-tools register lists each tool and the data classes it may receive (AGT-08)
- [ ] Agents run local checks first and the PR includes the evidence (AGT-09)
- [ ] Large agent diffs are split or accompanied by a summary of intent and risk (AGT-10)
- [ ] Agent-generated tests are reviewed for whether they verify requirements (AGT-11)
- [ ] Shared prompts, agent configuration and skills are versioned and reviewed (AGT-12)
- [ ] Licence and provenance of generated code is handled under the technology guideline (AGT-13)
- [ ] `AGENTS.md` names CP-02, CP-16 and CP-20 (AGT-14)
- [ ] Agent-written documentation is checked by a human against the code or design (AGT-15)

## [EG-006 Requirements and traceability](eg-006-requirements-and-traceability.md)

Profile: Standard. Owner: Systems engineering lead.

- [ ] Requirement levels and allocation rules are defined (REQ-01)
- [ ] Each requirement is atomic, unambiguous, feasible, necessary, consistent and verifiable, with one verification method (REQ-02)
- [ ] Requirements are stored as text in the repository with stable `REQ-<AREA>-<nnnn>` IDs (REQ-03)
- [ ] Each requirement has a rationale, parent, owner and status (REQ-04)
- [ ] Requirements are baselined by tag at each release (REQ-05)
- [ ] IDs are referenced in commit footers, PRs and test names (REQ-06)
- [ ] Every approved requirement is allocated, implemented and verified, and every test traces to a requirement (REQ-07)
- [ ] The pipeline generates a trace report with gap gates (REQ-08)
- [ ] A requirement change triggers a change impact check (REQ-09)
- [ ] Requirements are reviewed by author, implementer and verifier before approval (REQ-10)
- [ ] Non-functional requirements are selected from the NFR catalogue (REQ-11)
- [ ] Regulatory and security requirements are captured as requirements (REQ-12)
- [ ] Work items link to a requirement or defect, or state their justification (REQ-13)

## [EG-007 Architecture principles](eg-007-architecture-principles.md)

Profile: Standard. Owner: Architecture group.

- [ ] Principles are reviewed and adopted for the product, and changed only by RFC (PRN-05)
- [ ] ADRs and RFCs cite the principles that drove them (PRN-01)
- [ ] Decisions that go against a principle say so and record the consequences (PRN-02)
- [ ] The precedence order is applied, and tailored per quality profile where needed (PRN-03, PRN-06)
- [ ] Dependency direction, budgets and interface compatibility are checked in CI (PRN-04)
- [ ] Layers are defined and no application code touches hardware directly (AP-02)
- [ ] Silicon, SDKs and protocols sit behind interfaces we own (AP-03)
- [ ] Flash, RAM, CPU, power and latency budgets are allocated and tracked (AP-06)
- [ ] Diagnosis, security, fail-safe behaviour and lifecycle are designed in from the start (AP-08 to AP-11)

## [EG-008 Decision records: RFCs and ADRs](eg-008-decision-records.md)

Profile: Standard. Owner: Architecture group.

- [ ] ADRs live in `docs/adr/`, are numbered and use the template (ADR-01, ADR-02)
- [ ] ADRs are proposed by PR and merged as `accepted` (ADR-03)
- [ ] Accepted ADRs are immutable apart from status and links, and superseding ADRs point back (ADR-04)
- [ ] At least two options and the reasons for rejection are recorded (ADR-05)
- [ ] Consequences and verification are stated (ADR-06)
- [ ] ADRs link to requirements, principles, RFCs and PRs, and commits use the `ADR:` footer (ADR-07)
- [ ] ADRs are written before or during implementation, and retrospective ones are marked (ADR-08)
- [ ] A decision log index is generated (ADR-09)
- [ ] RFCs are used for guideline changes, cross-team interfaces, major tools and release changes (RFC-01)
- [ ] RFCs are stored in `docs/rfc/`, proposed by PR, short, and discussed in writing by default (RFC-02, RFC-09, RFC-10)
- [ ] Each RFC names an author, sponsor, affected teams, comment period and decision date (RFC-03, RFC-04)
- [ ] Affected teams are notified explicitly (RFC-05)
- [ ] Each RFC covers problem, goals, proposal, alternatives, impact, risks and open questions (RFC-06)
- [ ] Outcome and rationale are recorded and ADRs created (RFC-07, RFC-08)
- [ ] An architecture forum meets on a fixed cadence and every RFC is decided, or deferred with a reason, by its decision date (RFC-11)
- [ ] Architecture review is limited to architecturally significant changes, and other decisions belong to component owners (RFC-12)

## [EG-009 Interfaces and hardware and software co-design](eg-009-interfaces-and-co-design.md)

Profile: Standard. Owner: Architecture group.

- [ ] Every interface has an owner and a specification in the repository (INT-01, INT-02)
- [ ] Machine-readable definitions generate code and docs, with no hand-maintained copies (INT-03)
- [ ] Interfaces are versioned, a compatibility matrix is kept, and breaking changes go through RFC (INT-04)
- [ ] Contract tests run on both sides in CI (INT-05)
- [ ] The hardware interface agreement is versioned and firmware headers are generated where possible (INT-06)
- [ ] Hardware changes are reviewed for firmware impact and recorded in the bill of materials (INT-07)
- [ ] An errata register is maintained (INT-08)
- [ ] A bring-up plan and emulation exist for new hardware (INT-09)
- [ ] Cross-site interface changes are announced with lead time (INT-10)
- [ ] Vendor documents are version-controlled or cited by exact version (INT-11)

## [EG-010 Components, reuse and variants](eg-010-components-reuse-and-variants.md)

Profile: Full. Owner: Architecture group.

- [ ] A component register lists every component with owner, repository, version, status and consumers (COM-01)
- [ ] Every component has a named owner and deputy (COM-02)
- [ ] Consumers depend on released, pinned versions and never on branches or unreleased commits (COM-03)
- [ ] Interfaces follow the interface guideline and versions follow semantic versioning (COM-04)
- [ ] The register is checked before building or copying, and forks are recorded in an ADR (COM-05)
- [ ] Consumers do not patch components locally, and contribute changes through the owner (COM-06)
- [ ] Changes affecting several consumers are assessed for impact, with migration guidance and deprecation notice (COM-07)
- [ ] Each component builds and tests on its own and publishes versioned artefacts (COM-08)
- [ ] Variation is expressed through documented variation points, and supported variants are recorded (COM-09)
- [ ] Each product's bill of materials lists component versions (COM-10)
- [ ] Supported combinations are tested and recorded in the compatibility matrix, and kept few (COM-11)
- [ ] Transfer, deprecation and retirement are recorded and communicated (COM-12)
- [ ] Consumers report through the owner's tracker and severity 1 and 2 defects are visible to all consumers (COM-13)

## [EG-011 Technology selection and third-party components](eg-011-technology-and-third-party.md)

Profile: Standard. Owner: Architecture group.

- [ ] A technology radar exists with adopt, trial, assess and hold (TEC-01)
- [ ] New dependencies and tools have an evaluation recorded in an ADR (TEC-02)
- [ ] A licence policy lists approved and prohibited licences (TEC-03)
- [ ] A manifest of third-party components exists and an SBOM is produced per release (TEC-04)
- [ ] Versions are pinned and checksums verified (TEC-05)
- [ ] Vendor SDKs are wrapped behind our interfaces and patches are tracked (TEC-06)
- [ ] Dependency updates are proposed automatically, with security patch times (TEC-07)
- [ ] Each dependency has an owner, and critical ones have an exit strategy (TEC-08)
- [ ] AI-generated code is checked for licence and provenance (TEC-09)
- [ ] Toolchain versions are pinned in containers and listed in the radar (TEC-10)
- [ ] End-of-life dates are monitored (TEC-11)

## [EG-012 Coding principles](eg-012-coding-principles.md)

Profile: Starter. Owner: Firmware lead.

- [ ] The coding standard derives from the principles and cites them (CPR-01)
- [ ] Review comments cite principle or rule IDs (CPR-02)
- [ ] Deviations are recorded in the code and in the deviation log (CPR-03)
- [ ] Principles that a tool can check are enforced in CI (CPR-04)
- [ ] Changes are the minimum needed and every changed line traces to the request (CP-02, CP-16)
- [ ] Wrong code is hard to write: distinct types, `const`, narrow interfaces (CP-04)
- [ ] Input is validated at boundaries and invariants are asserted (CP-05)
- [ ] There is no silent failure and every error path is defined (CP-06)
- [ ] Resource use is bounded and undefined behaviour is avoided (CP-07, CP-08)
- [ ] Warnings are treated as errors (CP-15)
- [ ] Assumptions are stated and questions raised before implementing (CP-20)

## [EG-013 Coding standard](eg-013-coding-standard.md)

Profile: Standard. Owner: Firmware lead.

- [ ] There is one coding standard per language in use, with rule IDs that cite principles (COD-01)
- [ ] Language version, subset and compiler are specified (COD-02)
- [ ] The standard covers every required topic or says why not (COD-03)
- [ ] The formatter is configured in the repository and checked in CI (COD-04)
- [ ] Static analysis is configured and pinned, warnings are errors, and suppressions are justified and audited (COD-05)
- [ ] Rules are classified mandatory, required or advisory, with a deviation log (COD-06)
- [ ] Each rule has a rationale, examples and a checking tool (COD-07)
- [ ] Compiler flags are standardised and identical locally and in CI (COD-08)
- [ ] A legacy baseline is tracked and there is no drive-by reformatting (COD-09)
- [ ] The standard is reviewed annually through RFC (COD-10)
- [ ] A quick reference, review checklist and agent rule list exist (COD-11)
- [ ] Scripts and tooling code also have a proportionate standard (COD-12)

## [EG-014 Version control, commits and versioning](eg-014-version-control-and-versioning.md)

Profile: Starter. Owner: Build and tooling lead.

- [ ] Git is the single source of truth, the structure is documented, and no secrets or build outputs are committed (VCS-01)
- [ ] Branching is trunk-based with short-lived, correctly named branches (VCS-02)
- [ ] Commits follow Conventional Commits with scopes mapped to components (VCS-03)
- [ ] Breaking changes use `!` and a `BREAKING CHANGE:` footer (VCS-04)
- [ ] Footers carry `Refs:`, `ADR:` and `Assisted-by:` where relevant (VCS-05)
- [ ] Commits are atomic and buildable (VCS-06)
- [ ] A commit-msg hook and a CI lint enforce the format (VCS-07)
- [ ] `main` has linear history and shared branches are never force-pushed (VCS-08)
- [ ] Semantic versioning is defined for the product (VCS-09)
- [ ] The version comes from the tag, is injected by the build and is never hand-edited (VCS-10)
- [ ] Release tags are annotated, signed and immutable (VCS-11)
- [ ] Version bump, changelog and release notes are generated from commits (VCS-12)
- [ ] Back-ports use `cherry-pick -x` onto supported release branches (VCS-13)
- [ ] The team understands git well enough to use it safely (VCS-14)

## [EG-015 Pull requests and code review](eg-015-pull-requests-and-review.md)

Profile: Standard. Owner: Firmware lead.

- [ ] All changes to protected branches go through PR with no direct pushes (PRR-01)
- [ ] PR titles follow Conventional Commits (PRR-02)
- [ ] PR descriptions follow the template (PRR-03)
- [ ] PRs have one purpose and stay around 400 changed lines or fewer, excluding generated files (PRR-04)
- [ ] CODEOWNERS define required reviewers, with two for safety, security and certified areas (PRR-05)
- [ ] Reviewers are not the author and understand the area, and agents do not approve (PRR-06)
- [ ] Required checks pass before human review (PRR-07)
- [ ] Reviewers use the review focus for the change type (PRR-08)
- [ ] First response is within one working day and stale PRs are escalated (PRR-09)
- [ ] Comments are labelled and cite rule IDs (PRR-10)
- [ ] Blocking comments are resolved and stale approvals dismissed (PRR-11)
- [ ] Draft and stacked PRs are used where helpful, with documented order (PRR-12)
- [ ] PRs merge by squash and branches are deleted (PRR-13)
- [ ] PR links are kept as review evidence (PRR-14)
- [ ] Architecture review is not a routine PR requirement, and other PRs are reviewed by component owners (PRR-15)

## [EG-016 Pipelines and quality gates](eg-016-pipelines-and-quality-gates.md)

Profile: Standard. Owner: Build and tooling lead.

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

## [EG-017 Testing principles and strategy](eg-017-testing-principles-and-strategy.md)

Profile: Standard. Owner: Test and quality lead.

- [ ] A test strategy exists per product with levels, entry and exit criteria, tools and environments (TST-01)
- [ ] Testing is weighted towards host-level tests (TST-02)
- [ ] Test names or metadata carry requirement IDs (TST-03)
- [ ] Coverage is measured with thresholds and a ratchet, and requirement coverage is reported (TST-04)
- [ ] Simulators and test doubles are maintained and validated against hardware (TST-05)
- [ ] Negative tests and fault injection cover parsers, comms, update, storage and security (TST-06)
- [ ] Every fixed defect has a regression test and the suite runs on every merge to `main` (TST-07)
- [ ] Test data and fixtures are versioned (TST-08)
- [ ] Rigs are managed as products (TST-09)
- [ ] Results are archived per release and linked to requirements (TST-10)
- [ ] Non-functional tests run nightly or continuously (TST-11)
- [ ] Verification of high-risk requirements is independent of the author (TST-12)
- [ ] Upgrade and rollback are tested from all supported versions (TST-13)
- [ ] Exploratory testing is planned and time-boxed, with findings recorded (TST-14)
- [ ] No failing test is skipped or deleted to pass a gate (TST-15)

## [EG-018 Defect and technical debt management](eg-018-defects-and-technical-debt.md)

Profile: Standard. Owner: Test and quality lead.

- [ ] All defects are in the tracker with the required fields (DEF-01)
- [ ] Severity uses the agreed definitions, with priority set separately (DEF-02)
- [ ] New defects are triaged within two working days (DEF-03)
- [ ] The lifecycle is followed, verification is by someone else and closure needs a regression test (DEF-04)
- [ ] Root cause analysis is done for severity 1 and 2 defects and escapes (DEF-05)
- [ ] Each escape asks which gate should have caught it (DEF-06)
- [ ] Commits reference defects and release notes list fixes and known issues (DEF-07)
- [ ] A field defect route exists, with reproduction and release manager notification (DEF-08)
- [ ] Technical debt is recorded with label, impact, estimate and owner (DEF-09)
- [ ] Capacity is reserved for debt and old debt is reviewed (DEF-10)
- [ ] Deliberate debt has a repayment plan and expiry (DEF-11)
- [ ] Suppressions and deviations are tracked as debt (DEF-12)
- [ ] Metrics are used for improvement and not for ranking individuals (DEF-13)

## [EG-019 Logging, debug and fault diagnostics](eg-019-logging-debug-and-diagnostics.md)

Profile: Standard. Owner: Firmware lead.

- [ ] Logging purposes are separated, each with its own levels and retention (LOG-01)
- [ ] Log levels are defined and DEBUG and TRACE are off in production (LOG-02)
- [ ] There is one logging facility, no ad-hoc printf, and every record has a module ID and severity (LOG-03)
- [ ] The format is compact, structured and machine-parseable, with an off-target decoder if needed (LOG-04)
- [ ] A versioned event and fault code registry has an owner (LOG-05)
- [ ] Logging cost is budgeted, non-blocking and rate-limited (LOG-06)
- [ ] Persistent logs are wear-aware (LOG-07)
- [ ] Logs contain no secrets or personal data (LOG-08)
- [ ] Messages say what happened with context, and there is no logging in tight loops (LOG-09)
- [ ] Log decoding tools are versioned with the firmware (LOG-10)
- [ ] A standard debug setup is documented per platform and starts with one command (DBG-01)
- [ ] Debug and production builds are defined, debug builds are never released, and production interfaces are locked (DBG-02)
- [ ] Every fault path has defined behaviour, recorded in an ADR (DBG-03)
- [ ] Assertions guard invariants, have defined production behaviour and no side effects (DBG-04)
- [ ] The reset reason is captured at every boot (DBG-05)
- [ ] The crash dump format is defined, a build ID is embedded and symbols are archived per release (DBG-06, DBG-07)
- [ ] Runtime diagnostics exist and the watchdog design is reviewed (DBG-08, DBG-09)
- [ ] A procedure turns a field dump into a local reproduction, which becomes a test (DBG-10)
- [ ] Trace and timing tools are approved and the cost of instrumentation is documented (DBG-11)

## [EG-020 Observability and telemetry](eg-020-observability-and-telemetry.md)

Profile: Full. Owner: Platform lead.

- [ ] Observability requirements are defined per product (OBS-01)
- [ ] The telemetry schema is versioned, owned and follows naming conventions (OBS-02)
- [ ] Every record carries device, firmware, hardware, configuration and time context (OBS-03)
- [ ] Bandwidth, battery, storage and cost budgets exist with a sampling policy (OBS-04)
- [ ] Data minimisation, classification and retention are applied (OBS-05)
- [ ] Transport handles offline buffering, ordering, de-duplication and loss detection (OBS-06)
- [ ] Backend, dashboards and alerts are defined as code (OBS-07)
- [ ] Health indicators and objectives are defined, and every alert has an owner, runbook and action (OBS-08, OBS-13)
- [ ] Rollouts are gated by telemetry with automatic halt criteria (OBS-09)
- [ ] Field insights are reviewed monthly and fed into triage and tests (OBS-10)
- [ ] Lab and HIL environments emit the same telemetry (OBS-11)
- [ ] Data quality checks are in place (OBS-12)

## [EG-021 Release, update and production](eg-021-release-update-and-production.md)

Profile: Standard. Owner: Release manager.

- [ ] Release stages, roles and a checklist are defined in the repository (REL-01)
- [ ] The candidate is a tagged commit built once, and that artefact is promoted (REL-02)
- [ ] Release criteria are met: gates, no open severity 1 or 2, trace, NFRs, budgets, docs, SBOM, security, regulatory (REL-03)
- [ ] The evidence pack is generated automatically and retained (REL-04)
- [ ] Release notes are generated from commits and defects (REL-05)
- [ ] A bill of materials defines each baseline (REL-06)
- [ ] A compatibility matrix and supported upgrade paths are maintained (REL-07)
- [ ] The update mechanism is recorded in an ADR: authenticated, atomic, power-fail safe, with rollback and a downgrade policy (REL-08)
- [ ] Rollouts are staged with health gates and the ability to halt (REL-09)
- [ ] Upgrade and rollback are tested from supported versions (REL-10)
- [ ] A hotfix process is defined (REL-11)
- [ ] A support and end-of-life policy is published (REL-12)
- [ ] Production programming and provisioning are controlled, with feedback, unit traceability and secure key injection (REL-13, REL-14, REL-15)
- [ ] Artefacts, symbols and toolchains are retained for the supported life (REL-16)
- [ ] A post-release review is held (REL-17)

## [EG-022 Security and data protection](eg-022-security-and-data-protection.md)

Profile: Starter. Owner: Security lead.

- [ ] Security requirements and a threat model exist and are updated on architecture change (SEC-01)
- [ ] The security architecture covers trust boundaries, secure boot, encrypted comms, secure update, protected storage and debug protection (SEC-02)
- [ ] Only approved cryptography and vetted libraries are used (SEC-03)
- [ ] Key hierarchy, protected signing, provisioning, rotation and revocation are documented (SEC-04)
- [ ] No secrets are in source, and scanning runs pre-commit and in CI (SEC-05)
- [ ] Secure coding rules and security-focused review apply, and parsers are fuzzed (SEC-06)
- [ ] Security testing is performed and findings are tracked (SEC-07)
- [ ] Vulnerability intake, disclosure policy, patch times and SBOM monitoring exist (SEC-08)
- [ ] Supply chain controls are in place (SEC-09)
- [ ] A data classification scheme has handling rules, including for AI tools (SEC-10)
- [ ] Privacy by design, retention and impact assessment are applied where needed (SEC-11)
- [ ] Access is least-privilege with multi-factor authentication and quarterly review (SEC-12)
- [ ] Debug and manufacturing interfaces are protected in production (SEC-13)
- [ ] A security incident procedure is defined (SEC-14)

## [EG-023 Safety, regulatory and certification](eg-023-safety-regulatory-and-certification.md)

Profile: Full. Owner: Regulatory lead.

- [ ] Applicable standards and regulations are identified in a compliance register (REG-01)
- [ ] The register maps obligations to requirements, evidence, owner and status (REG-02)
- [ ] Regulatory obligations are captured as requirements and traced (REG-03)
- [ ] Evidence is produced by the pipeline into the evidence pack (REG-04)
- [ ] Changes to certified items have a change impact assessment (REG-05)
- [ ] The certified baseline is recorded and regulated software is separated where applicable (REG-06)
- [ ] The safety lifecycle is followed where an integrity level applies (REG-07)
- [ ] Tools for certified builds are qualified or validated and frozen (REG-08)
- [ ] Records are retained, audits held annually and findings tracked (REG-09)
- [ ] Test house and notified body contact is owned by a named person (REG-10)
- [ ] Regulatory changes are reviewed quarterly (REG-11)
- [ ] Technical files are maintained as docs as code (REG-12)
- [ ] Compliance training is recorded (REG-13)

## [EG-024 Planning, delivery and improvement](eg-024-planning-delivery-and-improvement.md)

Profile: Full. Owner: Engineering manager.

- [ ] Work is planned in time-boxed iterations or flow with a visible backlog, and every item is traceable (PLN-01)
- [ ] A Definition of Ready exists per work item type (PLN-02)
- [ ] A Definition of Done exists per type and the PR template reflects it (PLN-03)
- [ ] Estimates are ranges and forecasts state confidence (PLN-04)
- [ ] A risk register is maintained and reviewed fortnightly (PLN-05)
- [ ] Dependencies are recorded with an owner and need-by date (PLN-06)
- [ ] Escalation thresholds are defined (PLN-07)
- [ ] Capacity is reserved for support, debt and improvement (PLN-08)
- [ ] A small metric set is tracked and not used to rank individuals (PLN-09)
- [ ] Retrospectives are held and actions are tracked (PLN-10)
- [ ] Blameless postmortems follow severity 1 and 2 escapes, failed releases, outages and security incidents (PLN-11)
- [ ] Improvements are first-class backlog items (PLN-12)
- [ ] Friction with a guideline is raised as an issue or RFC (PLN-13)
- [ ] Status is derived from tracker and pipeline data (PLN-14)

## [EG-025 Research, prototyping and experiments](eg-025-research-and-prototyping.md)

Profile: Standard. Owner: Research lead.

- [ ] Work is classified as exploratory or production, with a question and a time-box (RSH-01)
- [ ] Exploratory code lives in designated locations and is excluded from release builds (RSH-02)
- [ ] Exemptions are understood and the non-negotiables are kept: no secrets, licences, data rules, version control, a working build (RSH-03)
- [ ] Prototype code is never copied into the product and the graduation checklist is used (RSH-04)
- [ ] An experiment record captures question, method, setup, results, conclusion and next step (RSH-05)
- [ ] Experiments are reproducible (RSH-06)
- [ ] Each exploration ends with a decision to stop, extend or graduate (RSH-07)
- [ ] The maturity level is stated (RSH-08)
- [ ] Prototypes are reviewed at the end of the time-box and unowned ones archived after 90 days (RSH-09)
- [ ] Lab equipment and boards are recorded with an owner (RSH-10)
- [ ] Findings are shared with the team (RSH-11)
- [ ] Agent use in prototypes follows the same boundaries (RSH-12)

## [EG-026 Competence, tooling and onboarding](eg-026-competence-tooling-and-onboarding.md)

Profile: Full. Owner: Engineering manager.

- [ ] A competence matrix covers languages, RTOS, platforms, protocols, tools, domains, security and test (CMP-01)
- [ ] Single-person areas are tracked as risks (CMP-02)
- [ ] Expected depth per tool is defined and used in training (CMP-03)
- [ ] Each tool and domain area has a champion and a how-to page (CMP-04)
- [ ] Domain experts and deputies are named and primers written (CMP-05)
- [ ] An onboarding path is documented and the environment is set up in under one day (CMP-06)
- [ ] Environment setup is tested in CI (CMP-07)
- [ ] An annual training plan has protected learning time (CMP-08)
- [ ] Knowledge sharing is regular and sessions are recorded (CMP-09)
- [ ] Rationale is captured in ADRs and docs, and a handover checklist exists for leavers (CMP-10)
- [ ] Key areas are known at two or more sites (CMP-11)
- [ ] The team is trained in safe and effective use of AI agents (CMP-12)
- [ ] New tools are introduced with training and a radar update (CMP-13)
