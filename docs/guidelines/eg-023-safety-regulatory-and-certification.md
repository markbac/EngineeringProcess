---
id: EG-023
title: "Safety, regulatory and certification"
status: draft
owner: "Regulatory lead"
version: 0.1.0
part: "Release, risk and compliance"
related: [EG-003, EG-006, EG-021, EG-022]
review-by: 2027-09-30
supersedes:
---

- **Owner:** Regulatory lead
- **Applies to:** All products and changes subject to safety, legal or certification requirements
- **Enforcement:** Change impact assessment, release criteria, audits
- **Related:** [EG-003](eg-003-quality-policy-and-attributes.md), [EG-006](eg-006-requirements-and-traceability.md), [EG-021](eg-021-release-update-and-production.md), [EG-022](eg-022-security-and-data-protection.md)

> **Note:** Rules marked *(core)* apply to every product and cannot be tailored. Other rules, and all numeric values, are proposed defaults that a product may tailor in its conformance profile ([EG-001](eg-001-guidelines-governance.md)).

## Purpose

Make compliance a by-product of the way we work: obligations known and traced, evidence produced by the pipeline, and changes assessed for their effect on certified baselines.

## Rules

1. **REG-01** Applicable standards and regulations MUST be identified per product and market and recorded in a compliance register with an owner. This includes, where relevant, safety, legal metrology, radio, electromagnetic compatibility and cybersecurity obligations.
1. **REG-02** The compliance register MUST map each obligation to requirements, evidence, owner and status.
1. **REG-03** Regulatory obligations MUST be captured as requirements with verification methods and traced like any other ([EG-006](eg-006-requirements-and-traceability.md)).
1. **REG-04** Evidence MUST be produced as a by-product of the process and stored in the release evidence pack (REL-04). It MUST NOT be assembled by hand at the end.
1. **REG-05** Every change touching a certified or regulated item MUST have a change impact assessment classifying it as no impact, notify or re-certify. Regulated components MUST be identified in CODEOWNERS, and the PR template asks the question.
1. **REG-06** The certified baseline (firmware and hardware versions) MUST be recorded. Changes outside it trigger assessment. Where applicable, regulated software SHOULD be separated architecturally from the rest.
1. **REG-07** Where a safety integrity level applies, the safety lifecycle of the chosen standard MUST be followed: hazard analysis, safety requirements, integrity level allocation, independence of verification and required coverage criteria. The chosen standard is recorded in an ADR.
1. **REG-08** Tools used for certified builds MUST be qualified or validated to the level required, and the toolchain frozen for the certified release.
1. **REG-09** Records MUST be retained and retrievable within an agreed time. Internal audits MUST be held at least annually against these guidelines and applicable standards, and findings tracked as defects.
1. **REG-10** Contact with notified bodies and test houses MUST be owned by a named person. Setup images and tools supplied for test are versioned and released like any other artefact.
1. **REG-11** Upcoming regulatory changes SHOULD be reviewed at least quarterly, with impact notes fed to planning.
1. **REG-12** Technical files MUST be maintained as documentation as code ([EG-004](eg-004-documentation-as-code.md)) and versioned with the release.
1. **REG-13** Team members working on regulated areas MUST have the relevant compliance training recorded ([EG-026](eg-026-competence-tooling-and-onboarding.md)).

## Change impact classes

| Class | Meaning | Action |
|-------|---------|--------|
| No impact | Outside certified scope, does not affect certified behaviour | Record rationale in the PR |
| Notify | Within scope but does not change certified behaviour | Notify the regulatory lead, record in evidence pack |
| Re-certify | Changes certified behaviour or scope | Plan re-assessment before release |

## Compliance

| Rule | Checked by |
|------|------------|
| REG-02, REG-03 | Compliance register audit, trace report |
| REG-04 | Release evidence pack completeness check |
| REG-05, REG-06 | CODEOWNERS on regulated paths, PR template, review |
| REG-09 | Annual internal audit |

## Checklist

Tick an item when it is true for your project. Rule IDs point to the detail above.

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

## Applying to personal projects and AI agents

### Personal projects

Starts at the **Full** profile (see [personal-projects.md](personal-projects.md)). Adopt only if the project is subject to a regulation or safety standard (for example radio, mains-connected, medical, or sold as a product). Otherwise record 'not applicable' in ADR-0001.

### AI agents

- Do not modify code, data or configuration in certified or regulated areas unless the task says so, and flag the change impact class in the PR (REG-05).
- Do not change tools or toolchain versions for certified builds (REG-08).
