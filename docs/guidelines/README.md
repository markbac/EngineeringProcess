---
title: "Engineering guidelines index"
status: draft
owner: "Architecture group"
last-reviewed: 2026-09-29
---

## About these guidelines

These are 26 engineering guidelines for an embedded R&D function, one guideline per file. They work for one product or many, and do not assume that products share code. They describe the practices a mature team follows and, for each one, what the guideline must contain and how compliance is checked. They are not coding rules: those belong in the coding standard that [EG-013](eg-013-coding-standard.md) requires.

Each guideline has rules with stable IDs, a compliance table, a checklist, and notes for applying it to personal projects and to AI agents. Cite rules by ID (for example `VCS-03`) in reviews, commits and agent instructions.

> **Note:** All guidelines are `draft` at version 0.1.0. Numeric thresholds (review turnaround, patch times, coverage targets, size limits) are proposed starting points. Set `status: active` when you adopt a guideline.

## Using these guidelines

- **In an organisation with several products:** read [organisation-adoption.md](organisation-adoption.md). Core rules apply everywhere, and each product records its tailoring in a conformance profile.
- **In a single team:** copy `docs/guidelines/` and `docs/templates-reference/` into the repository, confirm the owner roles, and adopt in the order given below.
- **In a personal project:** read [personal-projects.md](personal-projects.md), pick a profile (Starter, Standard or Full) and follow the bootstrap steps.
- **With AI agents:** put `AGENTS.md` at the repository root and keep [agent-rules.md](agent-rules.md) in the repository. Each guideline also has an AI agents section.
- **To assess adoption:** use the checklist at the end of each guideline, or the combined [checklists.md](checklists.md).

## How to read the rules

The keywords MUST, MUST NOT, SHOULD, SHOULD NOT and MAY are used as defined in RFC 2119.

- **MUST**: mandatory. Deviation needs a recorded, approved exception.
- **SHOULD**: expected. Deviation needs a stated reason in the PR or ADR.
- **MAY**: optional and left to judgement.

Every rule has a stable ID (for example `DOC-03`). IDs are never reused. Reviews, commits, tooling output and AI agents cite rules by ID.

## Guiding principles for consistency

1. **GP-01 One way to do each thing.** Where two approaches exist, the guideline picks one and records why.
1. **GP-02 If a tool can check it, a tool checks it.** Reviewers spend attention on design, not formatting.
1. **GP-03 Conventions drive outcomes.** A convention that does not feed an automated result (version, changelog, trace report, release) is etiquette and will decay. Prefer conventions that machines can read.
1. **GP-04 Everything is text in version control.** Requirements, decisions, diagrams, pipelines, repository settings and guidelines are reviewed, versioned and diffable.
1. **GP-05 Record decisions once, at the right level.** Context in an RFC, outcome in an ADR, rules in a guideline, enforcement in tooling.
1. **GP-06 Local equals CI.** Any check that runs in the pipeline runs identically on a developer machine with one command.
1. **GP-07 Guidelines are short and owned.** A few pages each, one named owner, a review date, and a stated way of checking compliance.
1. **GP-08 Understand the tool.** Using a tool without knowing how it works (git, the linker, the RTOS, the debug probe) is a risk. Each guideline names the competence expected.
1. **GP-09 Explain the why.** Rules carry a rationale where it is not obvious, so that people and agents can apply them sensibly at the edges.
1. **GP-10 Sequence adoption.** Start with what other practices depend on: commit conventions, a single version source and a reproducible pipeline.

## Designing for AI agents

AI coding agents and assistants are treated as team members with no tribal knowledge, no memory between sessions, and perfect literalism. Every guideline is therefore written with explicit, numbered, testable rules and stable IDs, so that an agent can follow and cite them. Enforcement never depends on the agent complying: hooks, gates, branch protection and CODEOWNERS apply equally to agent-authored changes. The specific rules are in [EG-005](eg-005-ai-agent-usage.md). The coding principles CP-02 (simplicity), CP-16 (surgical changes) and CP-20 (surface assumptions) in [EG-012](eg-012-coding-principles.md) are the most important for agents.

## Guideline index

| ID | Guideline | Part | Owner | Core rules | Personal projects start at |
|----|-----------|------|-------|------------|----------------------------|
| [EG-001](eg-001-guidelines-governance.md) | Guidelines governance | Foundations | Architecture group | 6 of 16 | Standard |
| [EG-002](eg-002-values-and-ways-of-working.md) | Engineering values and ways of working | Foundations | Engineering manager | 0 of 12 | Full |
| [EG-003](eg-003-quality-policy-and-attributes.md) | Quality policy and quality attributes | Foundations | Test and quality lead | 0 of 8 | Standard |
| [EG-004](eg-004-documentation-as-code.md) | Documentation as code and terminology | Foundations | Build and tooling lead | 4 of 15 | Starter |
| [EG-005](eg-005-ai-agent-usage.md) | AI agent usage | Foundations | Build and tooling lead and Security lead | 7 of 15 | Starter |
| [EG-006](eg-006-requirements-and-traceability.md) | Requirements and traceability | Requirements, architecture and design | Systems engineering lead | 2 of 13 | Standard |
| [EG-007](eg-007-architecture-principles.md) | Architecture principles | Requirements, architecture and design | Architecture group | 0 of 6 | Standard |
| [EG-008](eg-008-decision-records.md) | Decision records: RFCs and ADRs | Requirements, architecture and design | Architecture group | 4 of 21 | Standard |
| [EG-009](eg-009-interfaces-and-co-design.md) | Interfaces and hardware and software co-design | Requirements, architecture and design | Architecture group | 0 of 11 | Standard |
| [EG-010](eg-010-components-reuse-and-variants.md) | Components, reuse and variants | Requirements, architecture and design | Architecture group | 3 of 13 | Full |
| [EG-011](eg-011-technology-and-third-party.md) | Technology selection and third-party components | Requirements, architecture and design | Architecture group | 3 of 11 | Standard |
| [EG-012](eg-012-coding-principles.md) | Coding principles | Code and build | Firmware lead | 1 of 4 | Starter |
| [EG-013](eg-013-coding-standard.md) | Coding standard | Code and build | Firmware lead | 3 of 12 | Standard |
| [EG-014](eg-014-version-control-and-versioning.md) | Version control, commits and versioning | Code and build | Build and tooling lead | 9 of 14 | Starter |
| [EG-015](eg-015-pull-requests-and-review.md) | Pull requests and code review | Code and build | Firmware lead | 4 of 15 | Standard |
| [EG-016](eg-016-pipelines-and-quality-gates.md) | Pipelines and quality gates | Code and build | Build and tooling lead | 5 of 16 | Standard |
| [EG-017](eg-017-testing-principles-and-strategy.md) | Testing principles and strategy | Verification | Test and quality lead | 2 of 15 | Standard |
| [EG-018](eg-018-defects-and-technical-debt.md) | Defect and technical debt management | Verification | Test and quality lead | 2 of 13 | Standard |
| [EG-019](eg-019-logging-debug-and-diagnostics.md) | Logging, debug and fault diagnostics | Diagnostics and field insight | Firmware lead | 0 of 21 | Standard |
| [EG-020](eg-020-observability-and-telemetry.md) | Observability and telemetry | Diagnostics and field insight | Platform lead | 0 of 13 | Full |
| [EG-021](eg-021-release-update-and-production.md) | Release, update and production | Release, risk and compliance | Release manager | 2 of 17 | Standard |
| [EG-022](eg-022-security-and-data-protection.md) | Security and data protection | Release, risk and compliance | Security lead | 4 of 14 | Starter |
| [EG-023](eg-023-safety-regulatory-and-certification.md) | Safety, regulatory and certification | Release, risk and compliance | Regulatory lead | 0 of 13 | Full |
| [EG-024](eg-024-planning-delivery-and-improvement.md) | Planning, delivery and improvement | Delivery, research and people | Engineering manager | 0 of 14 | Full |
| [EG-025](eg-025-research-and-prototyping.md) | Research, prototyping and experiments | Delivery, research and people | Research lead | 0 of 12 | Standard |
| [EG-026](eg-026-competence-tooling-and-onboarding.md) | Competence, tooling and onboarding | Delivery, research and people | Engineering manager | 0 of 13 | Full |

## Supporting files

- [principles.md](../business-principles/principles.md): the principle sets (guiding, values, requirements, architecture, coding, testing, security, diagnostics, lifecycle, documentation, AI agents) and a start-here list
- [core-rules.md](core-rules.md): the rules that apply to every product without tailoring
- [organisation-adoption.md](organisation-adoption.md): two-layer model, conformance profile, owner roles, governance cadence and rollout
- [checklists.md](checklists.md): all checklists in one file
- [personal-projects.md](personal-projects.md): profiles, what to scale down, what never scales down, bootstrap steps
- [agent-rules.md](agent-rules.md): condensed rules for AI agents
- `../templates-reference/`: ADR, RFC, requirement, interface specification, NFR scenario, experiment record, postmortem, pull request, agent task brief, product conformance profile and component register templates
- `../../AGENTS.md`: agent instructions to place at the repository root

## Suggested adoption sequence

1. **Mechanics first:** [EG-001](eg-001-guidelines-governance.md) governance, [EG-014](eg-014-version-control-and-versioning.md) commits and versioning, [EG-016](eg-016-pipelines-and-quality-gates.md) reproducible pipeline
1. **Shared thinking:** [EG-002](eg-002-values-and-ways-of-working.md) values, [EG-003](eg-003-quality-policy-and-attributes.md) quality attributes, [EG-007](eg-007-architecture-principles.md) architecture principles, [EG-012](eg-012-coding-principles.md) coding principles
1. **Recording and communicating:** [EG-004](eg-004-documentation-as-code.md) docs as code, [EG-008](eg-008-decision-records.md) RFCs and ADRs, [EG-005](eg-005-ai-agent-usage.md) AI agent usage, [EG-015](eg-015-pull-requests-and-review.md) PR conventions
1. **Traceable engineering:** [EG-006](eg-006-requirements-and-traceability.md) requirements, [EG-013](eg-013-coding-standard.md) coding standard, [EG-009](eg-009-interfaces-and-co-design.md) interfaces, [EG-010](eg-010-components-reuse-and-variants.md) components and reuse, [EG-011](eg-011-technology-and-third-party.md) technology and third-party
1. **Evidence and insight:** [EG-017](eg-017-testing-principles-and-strategy.md) testing, [EG-018](eg-018-defects-and-technical-debt.md) defects and debt, [EG-019](eg-019-logging-debug-and-diagnostics.md) logging and debug, [EG-020](eg-020-observability-and-telemetry.md) observability
1. **Assurance and delivery:** [EG-021](eg-021-release-update-and-production.md) release, [EG-022](eg-022-security-and-data-protection.md) security, [EG-023](eg-023-safety-regulatory-and-certification.md) regulatory, [EG-024](eg-024-planning-delivery-and-improvement.md) planning
1. **Growth:** [EG-025](eg-025-research-and-prototyping.md) research and prototyping, [EG-026](eg-026-competence-tooling-and-onboarding.md) competence and onboarding
