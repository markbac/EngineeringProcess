---
id: EG-003
title: "Quality policy and quality attributes"
status: draft
owner: "Test and quality lead"
version: 0.1.0
part: "Foundations"
related: [EG-006, EG-007, EG-017, EG-021]
review-by: 2027-09-30
supersedes:
---

- **Owner:** Test and quality lead
- **Applies to:** All products and all engineering activities
- **Enforcement:** Review, CI (budget and gate checks), release criteria
- **Related:** [EG-006](eg-006-requirements-and-traceability.md), [EG-007](eg-007-architecture-principles.md), [EG-017](eg-017-testing-principles-and-strategy.md), [EG-021](eg-021-release-update-and-production.md)

> **Note:** Rules marked *(core)* apply to every product and cannot be tailored. Other rules, and all numeric values, are proposed defaults that a product may tailor in its conformance profile ([EG-001](eg-001-guidelines-governance.md)).

## Purpose

Define what quality means for our products so that requirements, architecture, tests and reviews aim at the same targets. Provide reusable non-functional requirement (NFR) templates so that quality attributes are made measurable rather than described in adjectives.

## Rules

1. **QUA-01** The team MUST maintain a quality policy of no more than one page, stating that products meet their requirements, are secure, can be diagnosed and updated in the field, and can be maintained for their supported life.
1. **QUA-02** The team MUST maintain a quality attribute model (below), adapted from ISO/IEC 25010, with definitions and example measures.
1. **QUA-03** Each product MUST have a quality attribute profile ranking its top attributes, approved by the architecture group and product owner. The profile guides trade-offs (see the precedence order in [EG-007](eg-007-architecture-principles.md)).
1. **QUA-04** Quality attributes MUST be stated as measurable scenarios in requirements: environment, stimulus, response and measure.
1. **QUA-05** The team MUST maintain an NFR catalogue at `docs/requirements/nfr-catalogue.md` with reusable templates. Teams select and tailor entries rather than writing NFRs from scratch.
1. **QUA-06** Quality MUST be built in. There is no separate quality phase: the gates in [EG-016](eg-016-pipelines-and-quality-gates.md) and the release criteria in [EG-021](eg-021-release-update-and-production.md) are the quality controls.
1. **QUA-07** Each release MUST have quality evidence: gate results, requirement verification, budget margins, defect status and coverage. This is included in the release evidence pack ([EG-021](eg-021-release-update-and-production.md)).
1. **QUA-08** Quality objectives and the attribute model SHOULD be reviewed at least annually, using field data ([EG-020](eg-020-observability-and-telemetry.md)) and escaped defect analysis ([EG-018](eg-018-defects-and-technical-debt.md)).

## Quality attribute model

| Attribute | Question it answers | Example measure |
|-----------|--------------------|-----------------|
| Functional correctness | Does it do what the requirements say? | Requirement verification pass rate |
| Performance and timing | Does it meet deadlines and throughput needs? | Worst-case execution time, latency percentiles |
| Reliability | Does it keep working over time and under faults? | Crash-free rate, soak hours without failure |
| Security | Is it protected against misuse and attack? | Open vulnerabilities by severity |
| Safety | Does it avoid harm when it fails? | Hazard mitigations verified |
| Resource efficiency | Does it stay within flash, RAM, CPU and power budgets? | Budget margin per component |
| Maintainability | Can it be changed safely and cheaply? | Change failure rate, review latency |
| Testability | Can behaviour be verified quickly and cheaply? | Share of logic testable on the host |
| Diagnosability | Can failures be understood in the field? | Share of field faults with a usable dump or log |
| Updatability | Can it be updated safely in the field? | Update success and rollback success rates |
| Interoperability | Does it work with other systems and revisions? | Compatibility matrix pass rate |
| Manufacturability | Can it be built, provisioned and tested at scale? | First-pass yield |

## NFR scenario template

```text
ID:           NFR-PERF-012
Attribute:    Performance and timing
Environment:  Normal operation, flash 80 percent full
Stimulus:     A firmware image is received for update
Response:     The image is validated and staged in the background
Measure:      The 10 ms control task misses no deadlines across 1000 updates
Verification: Test (HIL, nightly)
```

## Compliance

| Rule | Checked by |
|------|------------|
| QUA-04, QUA-05 | Requirement review checklist, NFR template check in CI |
| QUA-06 | Gate configuration review in [EG-016](eg-016-pipelines-and-quality-gates.md) |
| QUA-07 | Release evidence pack completeness check |
| QUA-08 | Review-by date in front matter |

## Checklist

Tick an item when it is true for your project. Rule IDs point to the detail above.

- [ ] A one-page quality policy is published (QUA-01)
- [ ] A quality attribute model exists with definitions and example measures (QUA-02)
- [ ] Each product has a ranked quality attribute profile, approved by the architecture lead and product owner (QUA-03)
- [ ] Quality attributes are stated as measurable scenarios in requirements (QUA-04)
- [ ] An NFR catalogue exists and requirements are selected from it (QUA-05)
- [ ] There is no separate quality phase, the gates are the quality controls (QUA-06)
- [ ] Each release has quality evidence in its evidence pack (QUA-07)
- [ ] The model and objectives are reviewed annually using field data (QUA-08)

## Applying to personal projects and AI agents

### Personal projects

Starts at the **Standard** profile (see [personal-projects.md](personal-projects.md)). Pick your top three quality attributes (for example correctness, simplicity, resource use) and write them in the README. Use the NFR scenario format only for requirements that matter.

### AI agents

- When a task involves a trade-off, use the project's ranked quality attributes and say which one you optimised (QUA-03).
- Write measurable acceptance criteria (environment, stimulus, response, measure) and not adjectives (QUA-04).
