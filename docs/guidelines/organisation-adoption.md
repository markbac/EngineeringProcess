---
title: "Adopting the guidelines across several products"
status: draft
owner: "Architecture group"
last-reviewed: 2026-09-29
---

## Purpose

This page explains how an R&D function with several products and a small architecture group can adopt the guidelines. It does not assume that products share code. Where they do, the components guideline ([EG-010](eg-010-components-reuse-and-variants.md)) adds the rules for it. Where they do not, the same rules apply within each product.

## Two layers

| Layer | What it contains | Who decides | How it changes |
|-------|------------------|-------------|----------------|
| Core | The 61 rules marked *(core)*, listed in [core-rules.md](core-rules.md) | Guideline owners, with the architecture forum | RFC, consulting every product's technical lead |
| Product | Everything else: applicability, thresholds, toolchain choices, exceptions | The product's technical lead | Change to the conformance profile, reported at the architecture forum |

The core layer keeps the products consistent where it matters most: anyone can move between products and find the same commit conventions, traceability, release evidence and AI agent controls. The product layer lets each product fit the rules to its hardware, certification needs and team size.

## Product conformance profile

Each product keeps a conformance profile in its repository (GOV-16), using [the template](../templates/product-conformance-profile.md). It records:

- which guidelines apply, and why any do not
- tailored rules and values, with the reason and who approved them
- approved exceptions with expiry dates
- the toolchain and the components the product uses and provides
- the top quality attributes and any change to the precedence order

The profile is checked in CI against the core list, so a profile cannot switch off a core rule.

## Sharing code is optional

Nothing here requires products to share code. The components guideline treats sharing as a spectrum, and its "How the rules scale" table says which rules apply when a component has one consumer, several, or is third party. A product that shares nothing keeps a register of its own components and complies with the same core rules. A product that starts to share a component then adopts the extra rules for that component, and not for the whole product.

## Owner roles

Owning a guideline means keeping it useful, answering questions and deciding on exceptions (GOV-14). Ownership is deliberately spread so that the architecture group is not a bottleneck. It owns the guidelines that set the direction of the design ([EG-001](eg-001-guidelines-governance.md), [EG-007](eg-007-architecture-principles.md), [EG-008](eg-008-decision-records.md), [EG-009](eg-009-interfaces-and-co-design.md), [EG-010](eg-010-components-reuse-and-variants.md), [EG-011](eg-011-technology-and-third-party.md)), and the rest sit with part-time leads drawn from the developers.

| Role | Guidelines owned | Typically drawn from | Time |
|------|------------------|----------------------|------|
| Architecture group | [EG-001](eg-001-guidelines-governance.md), [EG-007](eg-007-architecture-principles.md), [EG-008](eg-008-decision-records.md), [EG-009](eg-009-interfaces-and-co-design.md), [EG-010](eg-010-components-reuse-and-variants.md), [EG-011](eg-011-technology-and-third-party.md) | The architects, with a lead architect named per guideline | Core part of their work |
| Engineering manager | [EG-002](eg-002-values-and-ways-of-working.md), [EG-024](eg-024-planning-delivery-and-improvement.md), [EG-026](eg-026-competence-tooling-and-onboarding.md) | Line management | About 10 percent |
| Build and tooling lead | [EG-004](eg-004-documentation-as-code.md), [EG-005](eg-005-ai-agent-usage.md), [EG-014](eg-014-version-control-and-versioning.md), [EG-016](eg-016-pipelines-and-quality-gates.md) | Senior developer | 20 to 30 percent |
| Firmware lead | [EG-012](eg-012-coding-principles.md), [EG-013](eg-013-coding-standard.md), [EG-015](eg-015-pull-requests-and-review.md), [EG-019](eg-019-logging-debug-and-diagnostics.md) | Senior developer | 10 to 20 percent |
| Test and quality lead | [EG-003](eg-003-quality-policy-and-attributes.md), [EG-017](eg-017-testing-principles-and-strategy.md), [EG-018](eg-018-defects-and-technical-debt.md) | Senior developer or test engineer | About 20 percent |
| Systems engineering lead | [EG-006](eg-006-requirements-and-traceability.md) | An architect or a senior systems engineer | 10 to 20 percent |
| Platform lead | [EG-020](eg-020-observability-and-telemetry.md) | Senior developer (platform or backend) | 5 to 10 percent |
| Release manager | [EG-021](eg-021-release-update-and-production.md) | Senior developer or programme role | About 10 percent, more near releases |
| Security lead | [EG-005](eg-005-ai-agent-usage.md), [EG-022](eg-022-security-and-data-protection.md) | Senior developer with a security focus | About 10 percent |
| Regulatory lead | [EG-023](eg-023-safety-regulatory-and-certification.md) | May sit outside R&D | As the products require |
| Research lead | [EG-025](eg-025-research-and-prototyping.md) | Senior developer or architect | 5 to 10 percent |

> **Note:** Roles are proposals to be confirmed. One person may hold several roles, and a role may be shared. Each owner has a named deputy.

## Governance cadence

| Activity | Proposed cadence | Owner |
|----------|------------------|-------|
| Architecture forum: decide or defer open RFCs (RFC-11) | Fortnightly | Architecture group |
| Owners' check-in: exceptions, tailoring reports and open questions | Monthly | Architecture group |
| Exception register review (GOV-09) | Quarterly | Guideline owners |
| Guideline review (GOV-08) | Each guideline yearly, spread across the year | Guideline owners |
| Adoption assessment using the checklists | Twice a year per product | Product technical lead |

Keep architecture review for architecturally significant changes (RFC-12), and do not make it a routine step in every pull request (PRR-15). With three architects this is what keeps the workload manageable.

## Rollout

Adopt in the order of the sequence in the [guideline index](README.md). These phases group the steps. Durations are proposals and depend on the number of products and the starting point.

| Phase | Guidelines | Outcome | Proposed duration |
|-------|------------|---------|-------------------|
| 0. Decide | [EG-001](eg-001-guidelines-governance.md), [EG-002](eg-002-values-and-ways-of-working.md) | Owners named, core set agreed, conformance profile template agreed | 1 month |
| 1. Mechanics | [EG-014](eg-014-version-control-and-versioning.md), [EG-016](eg-016-pipelines-and-quality-gates.md), [EG-015](eg-015-pull-requests-and-review.md) | Commit and version conventions, reproducible pipeline and PR template in every product | 2 to 3 months |
| 2. Shared thinking | [EG-003](eg-003-quality-policy-and-attributes.md), [EG-007](eg-007-architecture-principles.md), [EG-012](eg-012-coding-principles.md) | Quality attributes, architecture and coding principles agreed and cited in reviews | 2 months |
| 3. Recording | [EG-004](eg-004-documentation-as-code.md), [EG-008](eg-008-decision-records.md), [EG-005](eg-005-ai-agent-usage.md) | Docs as code, ADRs and RFCs, AI agent controls in place | 2 to 3 months |
| 4. Traceable engineering | [EG-006](eg-006-requirements-and-traceability.md), [EG-013](eg-013-coding-standard.md), [EG-009](eg-009-interfaces-and-co-design.md), [EG-010](eg-010-components-reuse-and-variants.md), [EG-011](eg-011-technology-and-third-party.md) | Requirements traced, coding standard, interfaces and components registered | 3 to 6 months |
| 5. Evidence and insight | [EG-017](eg-017-testing-principles-and-strategy.md) to [EG-020](eg-020-observability-and-telemetry.md) | Test strategy, defect management, diagnostics and observability | 3 to 6 months |
| 6. Assurance and delivery | [EG-021](eg-021-release-update-and-production.md) to [EG-024](eg-024-planning-delivery-and-improvement.md) | Release and update safety, security, regulatory evidence, planning | Ongoing |
| 7. Growth | [EG-025](eg-025-research-and-prototyping.md), [EG-026](eg-026-competence-tooling-and-onboarding.md) | Research routes and onboarding | Ongoing |

Start each product with its core rules and the guidelines its risks demand, not with all of them. Use the [checklists](checklists.md) to see where a product is, and tick items only when they are true.

## Scaling notes

- **When a product joins:** create its conformance profile, register its components and run the checklists to set a baseline.
- **When a component gains a consumer:** move it down the scaling table in [EG-010](eg-010-components-reuse-and-variants.md) and agree the extra rules with the new consumer.
- **When the architecture group is overloaded:** narrow the scope of architecture review (RFC-12), delegate more decisions to component owners (VAL-02) and check that owners have time for the role.
- **When a core rule is disputed by several products:** treat it as a signal and open an RFC rather than granting exceptions one by one.
