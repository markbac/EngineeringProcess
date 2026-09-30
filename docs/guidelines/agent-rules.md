---
title: "Agent rules (condensed)"
status: draft
owner: "Project owner"
last-reviewed: 2026-09-29
---

## How to use this file

Read this file at the start of every task, together with `AGENTS.md`. Rules cite IDs. Each section links to the full guideline, which is authoritative. If a rule conflicts with the task, stop and ask (GOV-09).

## Always

1. Follow `AGENTS.md` and the commands in it.
1. Make the smallest change that meets the requirement (CP-02, CP-16), and state assumptions and questions first (CP-20).
1. Write Conventional Commits with `Refs:` and `Assisted-by:` footers (VCS-03, VCS-05, AGT-06).
1. Work on a short-lived branch and open a PR. Never push to `main`, and never approve or merge your own work (AGT-04, PRR-06).
1. Add or update tests with the change. Never skip, delete or weaken a test or check to pass a gate (TST-15, PIP-08).
1. Run the full local check command before proposing a change and include the results (AGT-09).
1. Update documentation in the same change (DOC-04).
1. Propose significant or hard-to-reverse decisions as an ADR with status `proposed` (ADR-03).
1. Never put secrets or personal data in code, logs, commits or prompts (SEC-05, AGT-08).
1. Stay out of the agent boundaries unless the task says so: guidelines, `AGENTS.md`, pipeline definitions, CODEOWNERS, secrets and signing material, generated and vendored code, security-relevant code, shared history and certified items (AGT-05).
1. When a rule is silent or unclear, apply the principles in [principles.md](principles.md), starting with its start-here list. If principles conflict, or the answer is not clear, stop and ask.
1. Rules marked *(core)* cannot be tailored. Follow the product's conformance profile for the rest.

## [EG-001 Guidelines governance](eg-001-guidelines-governance.md)

- Do not edit anything in `docs/guidelines/` unless the task explicitly says so (AGT-05).
- Cite rules by ID.
- If a rule blocks the task, stop and ask rather than deviating (GOV-09).

## [EG-002 Engineering values and ways of working](eg-002-values-and-ways-of-working.md)

- Prefer small, reviewable changes (VAL-11).
- Record decisions and assumptions in the PR or an ADR, not only in chat (VAL-06).
- Raise risks and doubts early and do not hide uncertainty (VAL-12).

## [EG-003 Quality policy and quality attributes](eg-003-quality-policy-and-attributes.md)

- When a task involves a trade-off, use the project's ranked quality attributes and say which one you optimised (QUA-03).
- Write measurable acceptance criteria (environment, stimulus, response, measure) and not adjectives (QUA-04).

## [EG-004 Documentation as code and terminology](eg-004-documentation-as-code.md)

- Update docs in the same change as the behaviour they describe (DOC-04).
- Never hand-edit generated docs (DOC-09).
- Draw diagrams as Mermaid text and avoid semicolons in labels because they break rendering.
- Write plain British English with the conclusion first (DOC-11).
- Check every statement in a doc against the code before committing (AGT-15).

## [EG-005 AI agent usage](eg-005-ai-agent-usage.md)

- Read `AGENTS.md` first and follow it (AGT-01).
- You may not approve or merge your own work (AGT-04).
- Do not touch governance files, secrets or signing material, generated or vendored code, security-relevant code, quality controls, shared history or certified items unless the task says so (AGT-05).
- Add an `Assisted-by:` trailer to your commits (AGT-06).
- Run the build, tests and lint before proposing a change and include the results (AGT-09).
- Keep changes small and single-purpose, and summarise intent and risk for larger ones (AGT-10).
- Do not send data to a tool that is not approved for its classification (AGT-08).

## [EG-006 Requirements and traceability](eg-006-requirements-and-traceability.md)

- Before implementing, find the requirement ID or IDs the task serves and cite them in commits (`Refs: REQ-...`) and test names (REQ-06).
- If there is no requirement, say so and ask, or propose one for review (REQ-13).
- Never edit approved requirements without instruction, and flag the impact on tests and docs (REQ-09).

## [EG-007 Architecture principles](eg-007-architecture-principles.md)

- Respect layering and dependency direction (AP-02) and keep third-party and hardware code behind our interfaces (AP-03).
- Choose the simplest design that meets the requirement (AP-05).
- When a design choice is significant or hard to reverse, propose an ADR instead of just implementing it (AP-13).
- Cite principle IDs in design notes (PRN-01).

## [EG-008 Decision records: RFCs and ADRs](eg-008-decision-records.md)

- When a decision is significant, hard to reverse or crosses component boundaries, draft an ADR with status `proposed` from `docs/templates/adr.md` instead of implementing silently (ADR-03).
- Do not edit accepted ADRs, supersede them (ADR-04).
- Read `docs/adr/` before changing behaviour it governs.
- Record at least two options (ADR-05).

## [EG-009 Interfaces and hardware and software co-design](eg-009-interfaces-and-co-design.md)

- Do not change a documented interface without an ADR or RFC and a version bump (INT-04).
- Regenerate generated interface files instead of editing them (INT-03).
- Add or update contract tests on both sides when touching an interface (INT-05).
- Cite datasheets and errata by ID and version (INT-11).

## [EG-010 Components, reuse and variants](eg-010-components-reuse-and-variants.md)

- Do not copy code from another component or repository into this one, depend on a pinned released version instead (COM-05, COM-03).
- Do not patch a component you consume, propose the change to its owner (COM-06).
- Do not depend on a branch or an unreleased commit (COM-03).
- When you change a component that has other consumers, state the consumer impact and compatibility (COM-07).

## [EG-011 Technology selection and third-party components](eg-011-technology-and-third-party.md)

- Do not add a dependency or tool without asking or drafting an ADR (TEC-02).
- Pin exact versions and update the manifest (TEC-04, TEC-05).
- Check licences against the approved list (TEC-03).
- Do not paste code of unknown provenance (TEC-09).
- Wrap vendor code behind an interface (TEC-06) and never edit vendored code directly.

## [EG-012 Coding principles](eg-012-coding-principles.md)

- Apply CP-02: write the minimum code, with no speculative features.
- Apply CP-16: change only what is needed and report unrelated problems instead of fixing them.
- Apply CP-20: state assumptions, ask when unclear and present alternatives.
- Handle every error path (CP-06), validate inputs at boundaries (CP-05) and keep warnings at zero (CP-15).
- Mark any deviation with the rule ID and a reason (CP-21).

## [EG-013 Coding standard](eg-013-coding-standard.md)

- Run the formatter and linter before every commit and do not hand-format (COD-04).
- Do not add suppressions without a rule ID and justification (COD-05).
- Use the flags in the build configuration unchanged (COD-08).
- Do not reformat unrelated code (COD-09).
- Follow the condensed rule list in the repository (COD-11).

## [EG-014 Version control, commits and versioning](eg-014-version-control-and-versioning.md)

- Write Conventional Commits with type, scope and the footers `Refs:` and `Assisted-by:` (VCS-03, VCS-05).
- Mark breaking changes with `!` and `BREAKING CHANGE:` (VCS-04).
- Keep commits atomic and buildable (VCS-06).
- Work on a short-lived branch and never push to `main` directly (VCS-02).
- Never force-push shared branches or rewrite history you did not create (VCS-08).
- Never edit version strings by hand (VCS-10).
- Never commit secrets, build outputs or large binaries (VCS-01).

## [EG-015 Pull requests and code review](eg-015-pull-requests-and-review.md)

- Open a PR with a Conventional Commit title and the filled template: what and why, links, evidence, risk and checklist (PRR-02, PRR-03).
- Keep to one purpose per PR and roughly under 400 lines excluding generated files (PRR-04).
- Label your review comments blocking, suggestion, question or nit (PRR-10).
- Never approve or merge your own PR (PRR-06).
- Wait for required checks and fix failures instead of bypassing them (PRR-07).

## [EG-016 Pipelines and quality gates](eg-016-pipelines-and-quality-gates.md)

- Do not modify pipeline definitions, required checks or gates unless the task says so (AGT-05).
- Never skip, disable or loosen a check or test to make a pipeline pass (PIP-08, TST-15).
- Run the same commands CI runs before proposing a change (PIP-01).
- If a test is flaky, report it and do not delete it (PIP-09).
- If your change breaks `main`, revert first (PIP-10).

## [EG-017 Testing principles and strategy](eg-017-testing-principles-and-strategy.md)

- Write a failing test that reproduces a bug before fixing it (TP-08).
- Add tests in the same change as the code, named with requirement IDs (TST-03).
- Test behaviour and not implementation, and include negative and boundary cases (TP-04, TP-09).
- Never skip, delete or weaken a test to make a gate pass (TST-15).
- Check that generated tests verify the requirement and would fail if the code were wrong (AGT-11).

## [EG-018 Defect and technical debt management](eg-018-defects-and-technical-debt.md)

- When fixing a defect, reproduce it with a test first, fix it, reference it in the commit (`Refs:`) and record the root cause category in the PR (DEF-05).
- Log unrelated problems you notice as tech-debt items instead of fixing them in passing (CP-16, DEF-09).
- Never close a defect without a regression test (DEF-04).

## [EG-019 Logging, debug and fault diagnostics](eg-019-logging-debug-and-diagnostics.md)

- Use the project's logging facility with the correct level and module, and never `printf` or ad-hoc prints (LOG-03).
- Never log secrets, keys or personal data (LOG-08).
- Handle every fault path explicitly (DBG-03).
- Do not put side effects in assertions (DBG-04).
- Add event and fault codes to the registry and never invent them inline (LOG-05).

## [EG-020 Observability and telemetry](eg-020-observability-and-telemetry.md)

- Do not add telemetry fields without updating the versioned schema and classification (OBS-02, OBS-05).
- Give every metric a name, unit and type per the convention (OBS-02).
- Never add personal data to telemetry (OBS-05).
- Do not add alerts without an owner, runbook and action (OBS-08).

## [EG-021 Release, update and production](eg-021-release-update-and-production.md)

- Never create or move release tags, edit changelogs by hand or change version strings unless the task says so (VCS-10, VCS-11).
- Do not rebuild artefacts for release (REL-02).
- Put upgrade notes and breaking changes in commit footers so that release notes generate correctly (REL-05).

## [EG-022 Security and data protection](eg-022-security-and-data-protection.md)

- Never write secrets, keys or tokens into code, config, logs, commits or prompts (SEC-05).
- If you find one, stop and report it.
- Never send Confidential or Restricted data to an unapproved tool (AGT-08, SEC-10).
- Do not use home-grown cryptography (SEC-03).
- Do not touch security-relevant code, authentication, key handling or debug protection without explicit instruction (AGT-05).
- Validate all input (CP-17).

## [EG-023 Safety, regulatory and certification](eg-023-safety-regulatory-and-certification.md)

- Do not modify code, data or configuration in certified or regulated areas unless the task says so, and flag the change impact class in the PR (REG-05).
- Do not change tools or toolchain versions for certified builds (REG-08).

## [EG-024 Planning, delivery and improvement](eg-024-planning-delivery-and-improvement.md)

- Treat the Definition of Done for the work item type as the finish line: reviewed, tested, documented, traced, with diagnostics and budgets checked (PLN-03).
- State uncertainty as a range and not a single date (PLN-04).
- Report blockers and risks in the PR or task summary and do not work around them silently (PLN-05, PLN-06).
- Draft postmortems from the template when asked (PLN-11).

## [EG-025 Research, prototyping and experiments](eg-025-research-and-prototyping.md)

- State the question and time-box before starting a spike (RSH-01).
- Put spike code only under `prototypes/` or a `proto/` branch (RSH-02).
- Record results, including negative ones, in `docs/research/` using the experiment record template (RSH-05).
- Do not promote prototype code into the product by copying it, propose a graduation task instead (RSH-04).
- Prototype status does not relax agent boundaries (RSH-12).

## [EG-026 Competence, tooling and onboarding](eg-026-competence-tooling-and-onboarding.md)

- Write or update a `docs/how-to/` page when you discover a non-obvious procedure (CMP-04, CMP-10).
- Keep the environment setup script working and tested (CMP-07).
- Point to ADRs and docs for rationale and do not rely on chat history (CMP-10).
