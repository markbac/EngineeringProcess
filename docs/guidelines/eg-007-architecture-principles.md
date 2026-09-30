---
id: EG-007
title: "Architecture principles"
status: draft
owner: "Architecture group"
version: 0.1.0
part: "Requirements, architecture and design"
related: [EG-003, EG-008, EG-012, EG-010]
review-by: 2027-09-30
supersedes:
---

- **Owner:** Architecture group
- **Applies to:** All architecture and design work, by people and agents
- **Enforcement:** Architecture review, ADRs, CI (dependency direction and budget checks)
- **Related:** [EG-003](eg-003-quality-policy-and-attributes.md), [EG-008](eg-008-decision-records.md), [EG-012](eg-012-coding-principles.md), [EG-010](eg-010-components-reuse-and-variants.md)
- **Principles:** AP-01 to AP-17 (defined below)

> **Note:** Rules marked *(core)* apply to every product and cannot be tailored. Other rules, and all numeric values, are proposed defaults that a product may tailor in its conformance profile ([EG-001](eg-001-guidelines-governance.md)).

## Purpose

Principles are the durable reasons behind architecture decisions. Rules cover situations we have already met. Principles guide judgement in new ones and settle disagreements. Each principle has an ID so that it can be cited in an ADR, an RFC or a review comment.

A principle becomes effective when it is carried through to enforcement. For example:

1. Principle: AP-02 Layered, one-way dependencies
1. Guideline rule: application code MUST NOT include hardware register headers
1. Tooling: a CI dependency check fails the build if the rule is broken

## Rules

1. **PRN-01** ADRs and RFCs SHOULD cite the principles that drove or constrained the decision.
1. **PRN-02** A decision that goes against a principle MUST say so in its ADR, with the reasons and the consequences accepted.
1. **PRN-03** Where principles conflict, the precedence order below applies unless an ADR states otherwise.
1. **PRN-04** Where a principle can be checked automatically (dependency direction, resource budgets, interface compatibility), it MUST be checked in CI.
1. **PRN-05** Principles MUST be reviewed at least annually and changed only through an RFC.
1. **PRN-06** A product MAY tailor the precedence order using its quality attribute profile (QUA-03), recorded in an ADR.

## Principles

| ID | Principle | Statement | Typical implications |
|----|-----------|-----------|----------------------|
| AP-01 | Requirements first | Architecture exists to satisfy requirements and quality attributes, and is traceable to them. | Every component and interface traces to a requirement. Quality attributes are stated measurably. |
| AP-02 | Layered, one-way dependencies | Hardware abstraction, platform services and application logic are separate layers, and dependencies point in one direction. | No application code touches registers directly. Dependency direction is checked in CI. |
| AP-03 | Isolate what changes | Volatile things (silicon, vendor SDKs, protocols, cloud endpoints) sit behind stable interfaces that we own. | Vendor code is wrapped by adapters and can be swapped for tests or new hardware. |
| AP-04 | Interfaces are contracts | Every interface is explicit, owned, versioned and tested for compatibility. | Definitions in machine-readable form where possible. Breaking changes follow semantic versioning. |
| AP-05 | Simplicity | Choose the simplest design that meets the requirements. Complexity must earn its place. | Fewer components, fewer modes, fewer configuration options. |
| AP-06 | Budgets are architecture | Flash, RAM, CPU, power, latency and bandwidth are allocated to components and tracked from the start. | Budget table in the architecture document. Size and timing are tracked in CI and a regression fails the gate. |
| AP-07 | Design for test | Logic is separable from hardware so that it runs on the host, and every component has seams for test doubles and HIL. | Hardware access behind interfaces, dependency injection, no hidden global state. |
| AP-08 | Design for diagnosis | The system explains its own state and failures. | Logging, fault codes, crash capture and telemetry are architectural components ([EG-019](eg-019-logging-debug-and-diagnostics.md), [EG-020](eg-020-observability-and-telemetry.md)). |
| AP-09 | Secure by design | Security is a design property: least privilege, defence in depth, secure defaults, minimal attack surface. | Trust boundaries, threat model and key handling are designed before implementation. |
| AP-10 | Fail safe and recover | Every fault has defined behaviour, and there is a route back to a known good state. | Watchdog, fault containment, power-fail handling, rollback on a failed update. |
| AP-11 | Design for the whole lifecycle | Field update, compatibility over time, manufacture, service and end of life are designed in from the outset. | Update mechanism, version compatibility rules, provisioning flow, decommissioning. |
| AP-12 | Deterministic where it matters | Timing-critical behaviour is predictable and bounded. | Bounded resource use, no dynamic allocation in critical paths, analysable scheduling. |
| AP-13 | Prefer reversible decisions | Make cheap-to-reverse decisions quickly. Take irreversible ones deliberately, with evidence. | Flash layout, crypto scheme and wire formats need an RFC and an ADR. |
| AP-14 | Reuse before build, with control | Reuse proven components and buy where sensible, but own the boundary. | Third-party choices go through [EG-011](eg-011-technology-and-third-party.md) and sit behind interfaces (AP-03). |
| AP-15 | Check architecture continuously | Architectural intent is enforced by automated checks as well as review. | Dependency rules, budget checks and interface compatibility tests run in the pipeline. |
| AP-16 | Structure follows ownership | Component boundaries match ownership, so that responsibilities are clear across sites. | Each component has an owner. Cross-site interfaces are contracts (AP-04). |
| AP-17 | Record the why | Decisions and their reasoning are kept where the code lives. | ADRs ([EG-008](eg-008-decision-records.md)) and architecture documents in the repository ([EG-004](eg-004-documentation-as-code.md)). |

## Precedence when principles conflict

This is a proposed order, to be confirmed through an RFC.

1. Safety and security
1. Correctness and requirements
1. Recoverability and diagnosability
1. Testability and maintainability
1. Performance and resource efficiency
1. Convenience and speed of delivery

## Compliance

| Rule | Checked by |
|------|------------|
| PRN-01, PRN-02 | Architecture review and the principles field in the ADR template |
| PRN-04 | CI: dependency direction, size and timing budgets, interface compatibility |
| PRN-05 | Review-by date in front matter |

## Checklist

Tick an item when it is true for your project. Rule IDs point to the detail above.

- [ ] Principles are reviewed and adopted for the product, and changed only by RFC (PRN-05)
- [ ] ADRs and RFCs cite the principles that drove them (PRN-01)
- [ ] Decisions that go against a principle say so and record the consequences (PRN-02)
- [ ] The precedence order is applied, and tailored per quality profile where needed (PRN-03, PRN-06)
- [ ] Dependency direction, budgets and interface compatibility are checked in CI (PRN-04)
- [ ] Layers are defined and no application code touches hardware directly (AP-02)
- [ ] Silicon, SDKs and protocols sit behind interfaces we own (AP-03)
- [ ] Flash, RAM, CPU, power and latency budgets are allocated and tracked (AP-06)
- [ ] Diagnosis, security, fail-safe behaviour and lifecycle are designed in from the start (AP-08 to AP-11)

## Applying to personal projects and AI agents

### Personal projects

Starts at the **Standard** profile (see [personal-projects.md](personal-projects.md)). Adopt five or six principles that fit and write them in the README. Good defaults are AP-02, AP-03, AP-05, AP-07, AP-08 and AP-13.

### AI agents

- Respect layering and dependency direction (AP-02) and keep third-party and hardware code behind our interfaces (AP-03).
- Choose the simplest design that meets the requirement (AP-05).
- When a design choice is significant or hard to reverse, propose an ADR instead of just implementing it (AP-13).
- Cite principle IDs in design notes (PRN-01).
