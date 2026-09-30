# Engineering Process & Guidelines

A comprehensive set of 26 engineering guidelines, core rules, checklists, and templates for embedded systems R&D, product teams, and AI coding agents.

## Overview

This repository establishes standard ways of working, quality gates, architectural principles, and traceability requirements across hardware and software engineering functions.

Each guideline includes:
- **Stable Rule IDs** (e.g. `VCS-03`, `DOC-01`, `CP-02`) for easy reference in pull requests, commits, and AI agent instructions.
- **Compliance Matrix** with unambiguous RFC 2119 keyword requirements (`MUST`, `SHOULD`, `MAY`).
- **Checklists** for peer reviews, release readiness, and compliance auditing.
- **Personal Projects & AI Agent Notes** to adapt standards for solo development or AI pair-programming.

---

## Directory Structure

```text
.
├── AGENTS.md                   # AI agent rules and standard commands repository root
├── CLAUDE.md                   # Agent configuration file importing AGENTS.md
├── README.md                   # Root repository index
├── docs/
│   ├── guidelines/             # Detailed engineering guidelines (EG-001 to EG-026)
│   │   ├── README.md           # Index, principles, and adoption sequence
│   │   ├── agent-rules.md      # Condensed guidelines for AI agents
│   │   ├── checklists.md       # Consolidated checklists for reviews and audits
│   │   ├── core-rules.md       # Mandatory rules for all projects
│   │   ├── organisation-adoption.md # Rollout, governance, and two-layer adoption model
│   │   ├── personal-projects.md     # Starter, Standard, and Full scaling profiles
│   │   └── principles.md       # Architectural, coding, and quality principles
│   └── templates-reference/              # Standard templates (ADR, RFC, PR, specifications)
```

---

## Engineering Guidelines Index

| ID | Guideline | Category | Owner | Core Rules |
|---|---|---|---|---|
| [EG-001](docs/guidelines/eg-001-guidelines-governance.md) | Guidelines Governance | Foundations | Architecture Group | 6 / 16 |
| [EG-002](docs/guidelines/eg-002-values-and-ways-of-working.md) | Engineering Values & Ways of Working | Foundations | Engineering Manager | 0 / 12 |
| [EG-003](docs/guidelines/eg-003-quality-policy-and-attributes.md) | Quality Policy & Attributes | Foundations | Test & Quality Lead | 0 / 8 |
| [EG-004](docs/guidelines/eg-004-documentation-as-code.md) | Documentation as Code & Terminology | Foundations | Build & Tooling Lead | 4 / 15 |
| [EG-005](docs/guidelines/eg-005-ai-agent-usage.md) | AI Agent Usage | Foundations | Build & Tooling / Security Lead | 7 / 15 |
| [EG-006](docs/guidelines/eg-006-requirements-and-traceability.md) | Requirements & Traceability | Requirements & Architecture | Systems Engineering Lead | 2 / 13 |
| [EG-007](docs/guidelines/eg-007-architecture-principles.md) | Architecture Principles | Requirements & Architecture | Architecture Group | 0 / 6 |
| [EG-008](docs/guidelines/eg-008-decision-records.md) | Decision Records: RFCs & ADRs | Requirements & Architecture | Architecture Group | 4 / 21 |
| [EG-009](docs/guidelines/eg-009-interfaces-and-co-design.md) | Interfaces & HW/SW Co-design | Requirements & Architecture | Architecture Group | 0 / 11 |
| [EG-010](docs/guidelines/eg-010-components-reuse-and-variants.md) | Components, Reuse & Variants | Requirements & Architecture | Architecture Group | 3 / 13 |
| [EG-011](docs/guidelines/eg-011-technology-and-third-party.md) | Tech Selection & 3rd Party Components | Requirements & Architecture | Architecture Group | 3 / 11 |
| [EG-012](docs/guidelines/eg-012-coding-principles.md) | Coding Principles | Code & Build | Firmware Lead | 1 / 4 |
| [EG-013](docs/guidelines/eg-013-coding-standard.md) | Coding Standard | Code & Build | Firmware Lead | 3 / 12 |
| [EG-014](docs/guidelines/eg-014-version-control-and-versioning.md) | Version Control, Commits & Versioning | Code & Build | Build & Tooling Lead | 9 / 14 |
| [EG-015](docs/guidelines/eg-015-pull-requests-and-review.md) | Pull Requests & Code Review | Code & Build | Firmware Lead | 4 / 15 |
| [EG-016](docs/guidelines/eg-016-pipelines-and-quality-gates.md) | Pipelines & Quality Gates | Code & Build | Build & Tooling Lead | 5 / 16 |
| [EG-017](docs/guidelines/eg-017-testing-principles-and-strategy.md) | Testing Principles & Strategy | Verification | Test & Quality Lead | 2 / 15 |
| [EG-018](docs/guidelines/eg-018-defects-and-technical-debt.md) | Defect & Technical Debt Management | Verification | Test & Quality Lead | 2 / 13 |
| [EG-019](docs/guidelines/eg-019-logging-debug-and-diagnostics.md) | Logging, Debug & Diagnostics | Diagnostics & Insight | Firmware Lead | 0 / 21 |
| [EG-020](docs/guidelines/eg-020-observability-and-telemetry.md) | Observability & Telemetry | Diagnostics & Insight | Platform Lead | 0 / 13 |
| [EG-021](docs/guidelines/eg-021-release-update-and-production.md) | Release, Update & Production | Release & Compliance | Release Manager | 2 / 17 |
| [EG-022](docs/guidelines/eg-022-security-and-data-protection.md) | Security & Data Protection | Release & Compliance | Security Lead | 4 / 14 |
| [EG-023](docs/guidelines/eg-023-safety-regulatory-and-certification.md) | Safety & Regulatory Certification | Release & Compliance | Regulatory Lead | 0 / 13 |
| [EG-024](docs/guidelines/eg-024-planning-delivery-and-improvement.md) | Planning, Delivery & Improvement | Delivery & People | Engineering Manager | 0 / 14 |
| [EG-025](docs/guidelines/eg-025-research-and-prototyping.md) | Research & Prototyping | Delivery & People | Research Lead | 0 / 12 |
| [EG-026](docs/guidelines/eg-026-competence-tooling-and-onboarding.md) | Competence, Tooling & Onboarding | Delivery & People | Engineering Manager | 0 / 13 |

---

## Quick Start & Adoption Sequence

1. **Mechanics & Versioning:** Start with [EG-001 Governance](docs/guidelines/eg-001-guidelines-governance.md), [EG-014 Version Control](docs/guidelines/eg-014-version-control-and-versioning.md), and [EG-016 Pipelines](docs/guidelines/eg-016-pipelines-and-quality-gates.md).
2. **Core Principles:** Review [Principles](docs/guidelines/principles.md) and adopt mandatory [Core Rules](docs/guidelines/core-rules.md).
3. **AI Agent Setup:** Place [AGENTS.md](AGENTS.md) at your project root and refer to [EG-005 AI Agent Usage](docs/guidelines/eg-005-ai-agent-usage.md) and [Agent Rules](docs/guidelines/agent-rules.md).
4. **Documentation & Review:** Use templates in [`docs/templates-reference/`](docs/templates-reference/) for ADRs, RFCs, and Pull Requests.

---

## Documentation Site

This repository is published to **GitHub Pages** via MkDocs. View the interactive documentation at the GitHub Pages site configured for `markbac/EngineeringProcess`.
