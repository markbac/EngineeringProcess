---
id: EG-025
title: "Research, prototyping and experiments"
status: draft
owner: "Research lead"
version: 0.1.0
part: "Delivery, research and people"
related: [EG-008, EG-011, EG-022, EG-024]
review-by: 2027-09-30
supersedes:
---

- **Owner:** Research lead
- **Applies to:** All exploratory work: spikes, prototypes, experiments and evaluations
- **Enforcement:** Repository structure, review, graduation checklist
- **Related:** [EG-008](eg-008-decision-records.md), [EG-011](eg-011-technology-and-third-party.md), [EG-022](eg-022-security-and-data-protection.md), [EG-024](eg-024-planning-delivery-and-improvement.md)

> **Note:** Rules marked *(core)* apply to every product and cannot be tailored. Other rules, and all numeric values, are proposed defaults that a product may tailor in its conformance profile ([EG-001](eg-001-guidelines-governance.md)).

## Purpose

Give exploratory work room to move quickly without letting prototypes quietly become products, and make sure findings, including negative ones, are recorded and reproducible.

## Rules

1. **RSH-01** Work MUST be classified as exploratory or production in the work item. Exploratory work MUST have a question to answer and a time-box.
1. **RSH-02** Exploratory code MUST live in designated locations (`prototypes/`, a separate repository or `proto/` branches), be clearly marked non-production and be excluded from release builds and baselines.
1. **RSH-03** Exploratory work MAY be exempt from the coding standard details, requirement traceability and full gates. It MUST NOT be exempt from: no secrets in code, licence compliance ([EG-011](eg-011-technology-and-third-party.md)), data classification ([EG-022](eg-022-security-and-data-protection.md)), version control and a working build.
1. **RSH-04** Prototype code MUST NOT be promoted by copying it into the product. Graduation requires re-implementation or hardening against the production guidelines, following the graduation checklist (below).
1. **RSH-05** Each exploration MUST produce an experiment record in `docs/research/`: question, method, setup (versions, hardware, configuration), results, conclusion and next step. Negative results MUST be recorded.
1. **RSH-06** Experiments MUST be reproducible: scripts and configuration versioned, data locations recorded and the environment described.
1. **RSH-07** Each exploration MUST end with a decision: stop, extend (with reason) or graduate. Decisions affecting architecture group to an RFC or ADR ([EG-008](eg-008-decision-records.md)).
1. **RSH-08** Maturity MUST be stated using the levels below, and the guidelines that apply increase with each level.
1. **RSH-09** Prototypes MUST be reviewed at the end of their time-box. Prototypes without an owner MUST be archived after 90 days.
1. **RSH-10** Evaluation boards, lab equipment and their configurations MUST be recorded with an owner.
1. **RSH-11** Findings SHOULD be shared with the team at the end of each exploration (demo or short write-up).
1. **RSH-12** AI agents MAY be used for prototyping under the same data rules. Prototype status does not relax AGT-05.

## Maturity levels

| Level | Name | Rules that apply | Exit needs |
|-------|------|------------------|------------|
| R0 | Idea | None | A question and a sponsor |
| R1 | Feasibility spike | RSH-03 minimum | Experiment record and decision |
| R2 | Prototype | Adds coding basics, docs in repository, review | Demonstrated against stated criteria |
| R3 | Pre-production candidate | Adds requirements, architecture and ADRs, coding standard, tests, security review | Graduation checklist passed |
| R4 | Product | All guidelines | Normal release process ([EG-021](eg-021-release-update-and-production.md)) |

## Graduation checklist

1. Requirements written and traced ([EG-006](eg-006-requirements-and-traceability.md))
1. Architecture reviewed against principles, ADRs recorded ([EG-007](eg-007-architecture-principles.md), [EG-008](eg-008-decision-records.md))
1. Code conforms to the coding standard and is reviewed ([EG-013](eg-013-coding-standard.md), [EG-015](eg-015-pull-requests-and-review.md))
1. Tests at required levels, and pipeline gates passing ([EG-016](eg-016-pipelines-and-quality-gates.md), [EG-017](eg-017-testing-principles-and-strategy.md))
1. Security review and licence check completed ([EG-022](eg-022-security-and-data-protection.md), [EG-011](eg-011-technology-and-third-party.md))
1. Diagnostics and observability designed in ([EG-019](eg-019-logging-debug-and-diagnostics.md), [EG-020](eg-020-observability-and-telemetry.md))
1. Documentation as code ([EG-004](eg-004-documentation-as-code.md))

## Compliance

| Rule | Checked by |
|------|------------|
| RSH-02 | CI: release builds exclude prototype paths |
| RSH-04, RSH-08 | Graduation review by architecture group |
| RSH-05 | Experiment record template check in CI |
| RSH-09 | Quarterly prototype inventory review |

## Checklist

Tick an item when it is true for your project. Rule IDs point to the detail above.

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

## Applying to personal projects and AI agents

### Personal projects

Starts at the **Standard** profile (see [personal-projects.md](personal-projects.md)). This is where personal projects live. Keep a `prototypes/` folder, one experiment record per spike, and a firm stop, extend or graduate decision. Never copy prototype code into the product: re-implement it against the graduation checklist.

### AI agents

- State the question and time-box before starting a spike (RSH-01).
- Put spike code only under `prototypes/` or a `proto/` branch (RSH-02).
- Record results, including negative ones, in `docs/research/` using the experiment record template (RSH-05).
- Do not promote prototype code into the product by copying it, propose a graduation task instead (RSH-04).
- Prototype status does not relax agent boundaries (RSH-12).
