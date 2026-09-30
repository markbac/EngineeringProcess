---
id: EG-010
title: "Components, reuse and variants"
status: draft
owner: "Architecture group"
version: 0.1.0
part: "Requirements, architecture and design"
related: [EG-007, EG-009, EG-011, EG-014, EG-021]
review-by: 2027-09-30
supersedes:
---

- **Owner:** Architecture group
- **Applies to:** Every component, whether built in the product, reused from another product, or third party
- **Enforcement:** Component register checks in CI, dependency checks in the pipeline, review
- **Related:** [EG-007](eg-007-architecture-principles.md), [EG-009](eg-009-interfaces-and-co-design.md), [EG-011](eg-011-technology-and-third-party.md), [EG-014](eg-014-version-control-and-versioning.md), [EG-021](eg-021-release-update-and-production.md)

> **Note:** Rules marked *(core)* apply to every product and cannot be tailored. Other rules, and all numeric values, are proposed defaults that a product may tailor in its conformance profile ([EG-001](eg-001-guidelines-governance.md)).

## Purpose

Define how the parts of a product are named, owned, versioned and consumed, so that the same rules work whether a product is self-contained, shares components with other products, or uses third-party code. Sharing is treated as a spectrum and not as a requirement: the rules apply to a component with one consumer and scale up as consumers are added.

## Rules

1. **COM-01** *(core)* Every component MUST be listed in a component register recording its owner, deputy, repository, current version, status (`active`, `maintenance`, `deprecated`, `retired`) and consumers. Third-party components are listed with the same fields ([EG-011](eg-011-technology-and-third-party.md)). A product keeps its own register, or uses a shared register where products share components.
1. **COM-02** *(core)* Every component MUST have a named owner and a deputy. A component with no owner MUST be escalated to the architecture group within one month.
1. **COM-03** *(core)* Consumers MUST depend on released, versioned artefacts. They MUST NOT depend on a branch, an unreleased commit or a copy of the source.
1. **COM-04** Component interfaces MUST follow [EG-009](eg-009-interfaces-and-co-design.md), and component versions MUST follow semantic versioning ([EG-014](eg-014-version-control-and-versioning.md)).
1. **COM-05** Before building or copying functionality, the author MUST check the register. A fork of a component MUST be recorded in an ADR, with either a plan to converge or the reason not to.
1. **COM-06** A consumer MUST NOT patch a component locally. Changes are contributed to the owner, who reviews them under the same rules as any other change. An urgent local patch needs an exception (GOV-09) with an expiry date.
1. **COM-07** A change to a component with more than one consumer MUST include a consumer impact assessment. A breaking change MUST come with migration guidance and a deprecation notice agreed with the consumers.
1. **COM-08** Each component MUST build and pass its tests without any consumer present, and MUST publish versioned artefacts with release notes generated from Conventional Commits ([EG-014](eg-014-version-control-and-versioning.md)).
1. **COM-09** Variation between products or configurations SHOULD be expressed through documented variation points (build-time configuration, runtime configuration or an extension interface) and not by branching or copying. Supported variants MUST be recorded in the register.
1. **COM-10** Each product MUST have a bill of materials listing the version of every component it ships ([EG-021](eg-021-release-update-and-production.md)).
1. **COM-11** Where a component is used in more than one configuration, the supported combinations MUST be tested and recorded in a compatibility matrix. The number of supported combinations SHOULD be kept small.
1. **COM-12** Transfer of ownership, deprecation and retirement of a component MUST be recorded in the register and communicated to every consumer.
1. **COM-13** Consumers MUST report defects and requests through the owner's tracker. Severity 1 and 2 defects ([EG-018](eg-018-defects-and-technical-debt.md)) SHOULD be visible to all consumers.

## How the rules scale

| Situation | What applies | What can be relaxed |
|-----------|--------------|---------------------|
| No sharing: the component sits inside one product | COM-01, COM-02, COM-03, COM-10 | Compatibility matrix, deprecation notices and consumer impact assessment |
| A few internal consumers | Also COM-04 to COM-08 and COM-12 | Formal variation points, if there is one variant |
| Many consumers across products | All rules | Nothing, and the owner needs time set aside to serve consumers |
| Third-party component | COM-01, COM-03, COM-05, COM-06, COM-10 and [EG-011](eg-011-technology-and-third-party.md) | Owner is the internal sponsor, who tracks upstream releases and defects |

A component that gains a second consumer moves down this table. The owner and deputy then agree the additional rules with the new consumer and record the change in the register.

## Component register example

```yaml
components:
  - name: bootloader
    owner: "A. Owner"
    deputy: "B. Deputy"
    repository: "git@example.com:firmware/bootloader.git"
    version: 2.4.1
    status: active
    consumers: [product-a, product-b]
    interfaces: [IF-BOOT-001]
    variation-points: [flash-layout, signature-scheme]
```

## Compliance

| Rule | Checked by |
|------|------------|
| COM-01, COM-02, COM-12 | CI: register schema validation and ownership check |
| COM-03, COM-08, COM-10 | CI: dependency resolution rejects branch and unreleased references, and generates the bill of materials |
| COM-04, COM-07, COM-11 | Interface compatibility tests, review by the component owner |
| COM-05, COM-06, COM-09, COM-13 | Review, ADR history, tracker audit |

## Checklist

Tick an item when it is true for your project. Rule IDs point to the detail above.

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

## Applying to personal projects and AI agents

### Personal projects

Starts at the **Full** profile (see [personal-projects.md](personal-projects.md)). Only needed if you reuse your own code across projects. Publish it as a versioned package or tagged repository and pin it, instead of copying it between projects. Keep a short list of the components you maintain and their versions.

### AI agents

- Do not copy code from another component or repository into this one, depend on a pinned released version instead (COM-05, COM-03).
- Do not patch a component you consume, propose the change to its owner (COM-06).
- Do not depend on a branch or an unreleased commit (COM-03).
- When you change a component that has other consumers, state the consumer impact and compatibility (COM-07).
