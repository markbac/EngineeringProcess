---
id: EG-009
title: "Interfaces and hardware and software co-design"
status: draft
owner: "Architecture group"
version: 0.1.0
part: "Requirements, architecture and design"
related: [EG-007, EG-011, EG-017, EG-021, EG-010]
review-by: 2027-09-30
supersedes:
---

- **Owner:** Architecture group
- **Applies to:** All software, protocol, hardware and cross-site interfaces
- **Enforcement:** CI (contract tests, generation checks), review
- **Related:** [EG-007](eg-007-architecture-principles.md), [EG-011](eg-011-technology-and-third-party.md), [EG-017](eg-017-testing-principles-and-strategy.md), [EG-021](eg-021-release-update-and-production.md), [EG-010](eg-010-components-reuse-and-variants.md)

> **Note:** Rules marked *(core)* apply to every product and cannot be tailored. Other rules, and all numeric values, are proposed defaults that a product may tailor in its conformance profile ([EG-001](eg-001-guidelines-governance.md)).

## Purpose

Make every boundary an owned, versioned, verified contract, and keep hardware and firmware teams working from one shared, controlled description of the platform.

## Rules

1. **INT-01** Every interface (software API, inter-processor link, protocol, hardware and software boundary, external system) MUST have an owner and a specification in the repository.
1. **INT-02** An interface specification MUST state its purpose, roles, data formats, timing, error handling, versioning and compatibility rules, security properties and verification method.
1. **INT-03** Interfaces SHOULD be defined in machine-readable form (headers, IDL, schemas, register descriptions such as SVD) and used to generate code and documentation. Hand-maintained copies MUST NOT exist.
1. **INT-04** Interfaces MUST be versioned with semantic versioning. A compatibility matrix MUST be maintained, and a breaking change needs an RFC and a coordinated release.
1. **INT-05** Provider and consumer MUST both run interface contract tests in CI.
1. **INT-06** A hardware interface agreement (pin map, memory map, clocks, power, boot configuration, peripherals) MUST be kept as a versioned document. Firmware headers SHOULD be generated from it where possible.
1. **INT-07** Every hardware revision or component change MUST be reviewed for firmware impact, and the firmware team notified before release of the change. The hardware revision MUST be recorded in the bill of materials ([EG-021](eg-021-release-update-and-production.md)).
1. **INT-08** A silicon errata register MUST be kept. Each erratum is reviewed when a silicon revision is adopted, and tracked with affected components, workaround and references to code or ADRs.
1. **INT-09** A bring-up plan MUST exist for new hardware: board-level test firmware, checklists, and emulation or simulation so that firmware work starts before hardware arrives.
1. **INT-10** Cross-site interfaces are the highest-risk contracts. Changes MUST be announced by change notice or RFC with agreed lead time.
1. **INT-11** Datasheets, reference manuals and vendor documents MUST be version-controlled or referenced by exact version, and cited by ID in the design.

## Interface specification skeleton

```markdown
# Interface: <name>

- Owner:
- Version:
- Providers and consumers:

## Purpose
## Data and encoding
## Timing and ordering
## Errors and recovery
## Versioning and compatibility
## Security properties
## Verification
```

## Compliance

| Rule | Checked by |
|------|------------|
| INT-03 | CI: generation check fails if generated files differ from committed sources |
| INT-04, INT-05 | CI: contract tests on both sides, compatibility matrix check |
| INT-07, INT-08 | Hardware change review, errata register audit |

## Checklist

Tick an item when it is true for your project. Rule IDs point to the detail above.

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

## Applying to personal projects and AI agents

### Personal projects

Starts at the **Standard** profile (see [personal-projects.md](personal-projects.md)). Write down any boundary that another module, script, agent or device relies on (an API, a file format, a register map). Keep datasheet versions in `docs/reference/` or link them by version.

### AI agents

- Do not change a documented interface without an ADR or RFC and a version bump (INT-04).
- Regenerate generated interface files instead of editing them (INT-03).
- Add or update contract tests on both sides when touching an interface (INT-05).
- Cite datasheets and errata by ID and version (INT-11).
