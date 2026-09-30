---
id: EG-017
title: "Testing principles and strategy"
status: draft
owner: "Test and quality lead"
version: 0.1.0
part: "Verification"
related: [EG-003, EG-006, EG-007, EG-016, EG-018, EG-021]
review-by: 2027-09-30
supersedes:
---

- **Owner:** Test and quality lead
- **Applies to:** All verification activity, environments and test code
- **Enforcement:** CI, review, release criteria
- **Related:** [EG-003](eg-003-quality-policy-and-attributes.md), [EG-006](eg-006-requirements-and-traceability.md), [EG-007](eg-007-architecture-principles.md), [EG-016](eg-016-pipelines-and-quality-gates.md), [EG-018](eg-018-defects-and-technical-debt.md), [EG-021](eg-021-release-update-and-production.md)
- **Principles:** TP-01 to TP-11 (defined below)

> **Note:** Rules marked *(core)* apply to every product and cannot be tailored. Other rules, and all numeric values, are proposed defaults that a product may tailor in its conformance profile ([EG-001](eg-001-guidelines-governance.md)).

## Purpose

Set the principles that guide how we test, require a test strategy for each product, and manage test environments (simulators and HIL rigs) as products in their own right.

## Testing principles

| ID | Principle | Statement |
|----|-----------|-----------|
| TP-01 | Cheapest level first | Test at the cheapest level that can catch the defect. Most tests run on the host. |
| TP-02 | Trace to requirements | Every test verifies a requirement, and every requirement has verification. |
| TP-03 | Deterministic and independent | Tests give the same result every run, in any order. |
| TP-04 | Behaviour over implementation | Tests check what the unit promises, not how it does it. |
| TP-05 | Fail clearly | A failing test says what went wrong and where. |
| TP-06 | Automate what repeats | Anything run more than twice is automated. |
| TP-07 | Tests are code | Tests are reviewed, refactored and maintained to the same standard. |
| TP-08 | Bugs start with a test | A defect is reproduced by a failing test before it is fixed. |
| TP-09 | Test what can go wrong | Negative, boundary and fault-injection cases are as important as the happy path. |
| TP-10 | Hardware for what only hardware shows | Timing, power, peripherals and environment need real hardware. |
| TP-11 | Controlled environments | The environment for every test run is known and recorded. |

## Rules

1. **TST-01** Each product MUST have a test strategy covering levels, entry and exit criteria, tools, environments, responsibilities and reporting.
1. **TST-02** Testing MUST be organised in levels (below), weighted towards host-based tests.
1. **TST-03** *(core)* Test names or metadata MUST include the requirement IDs they verify (REQ-06). The verification method recorded for each requirement MUST be executed.
1. **TST-04** Coverage MUST be measured on host tests with thresholds set per component criticality. Coverage MUST NOT decrease (ratchet). Requirement coverage is reported alongside code coverage, and stronger criteria (for example MC/DC) apply where a standard requires them.
1. **TST-05** Simulators, emulators and test doubles MUST be maintained and periodically validated against real hardware.
1. **TST-06** Negative tests and fault injection MUST be included for parsers, communication stacks, update, storage and security functions.
1. **TST-07** *(core)* Every fixed defect MUST have a regression test (DEF-04). The regression suite MUST run on every merge to `main`.
1. **TST-08** Test data and fixtures MUST be versioned with the tests.
1. **TST-09** HIL rigs and shared environments MUST be managed as products: named owner, configuration record, booking, calibration, health checks, spares and documented setup as code where possible.
1. **TST-10** Results MUST be archived per release and linked to requirements ([EG-021](eg-021-release-update-and-production.md)).
1. **TST-11** Non-functional tests (soak, power profile, size and timing trends, environmental) SHOULD run continuously or nightly, not only before release.
1. **TST-12** Verification of high-risk requirements MUST be performed or reviewed by someone other than the author.
1. **TST-13** Every release MUST be tested for upgrade from all supported previous versions and for rollback ([EG-021](eg-021-release-update-and-production.md)).
1. **TST-14** Exploratory testing SHOULD be planned and time-boxed, and findings recorded as defects or new tests.
1. **TST-15** Flaky tests are handled under PIP-09. Skipping or deleting a failing test MUST NOT be used to make a gate pass.

## Test levels

| Level | Runs on | Purpose |
|-------|---------|---------|
| Unit | Host | Logic of one unit, fast, deterministic |
| Component and integration | Host or simulator | Interactions between units and with doubles |
| HIL integration | Hardware rig | Real peripherals, timing, drivers |
| System | Hardware rig or product | End-to-end behaviour against system requirements |
| Non-functional | Rig or lab | Performance, power, soak, environmental, resilience |
| Security | Rig or lab | Fuzzing, penetration and security regression tests |
| Update and compatibility | Rig | Upgrade, downgrade and rollback across supported versions |
| Production test | Factory | Manufacturing defects and provisioning correctness |

## Compliance

| Rule | Checked by |
|------|------------|
| TST-03 | CI: test metadata check and trace report |
| TST-04 | CI: coverage gate and ratchet |
| TST-07, TST-13 | Pipeline configuration, release criteria |
| TST-09 | Rig register audit |

## Checklist

Tick an item when it is true for your project. Rule IDs point to the detail above.

- [ ] A test strategy exists per product with levels, entry and exit criteria, tools and environments (TST-01)
- [ ] Testing is weighted towards host-level tests (TST-02)
- [ ] Test names or metadata carry requirement IDs (TST-03)
- [ ] Coverage is measured with thresholds and a ratchet, and requirement coverage is reported (TST-04)
- [ ] Simulators and test doubles are maintained and validated against hardware (TST-05)
- [ ] Negative tests and fault injection cover parsers, comms, update, storage and security (TST-06)
- [ ] Every fixed defect has a regression test and the suite runs on every merge to `main` (TST-07)
- [ ] Test data and fixtures are versioned (TST-08)
- [ ] Rigs are managed as products (TST-09)
- [ ] Results are archived per release and linked to requirements (TST-10)
- [ ] Non-functional tests run nightly or continuously (TST-11)
- [ ] Verification of high-risk requirements is independent of the author (TST-12)
- [ ] Upgrade and rollback are tested from all supported versions (TST-13)
- [ ] Exploratory testing is planned and time-boxed, with findings recorded (TST-14)
- [ ] No failing test is skipped or deleted to pass a gate (TST-15)

## Applying to personal projects and AI agents

### Personal projects

Starts at the **Standard** profile (see [personal-projects.md](personal-projects.md)). Write unit tests on the host for logic, a regression test for every bug, and a smoke test for the whole thing. A coverage ratchet is cheap and effective. Skip rig management unless you own a rig.

### AI agents

- Write a failing test that reproduces a bug before fixing it (TP-08).
- Add tests in the same change as the code, named with requirement IDs (TST-03).
- Test behaviour and not implementation, and include negative and boundary cases (TP-04, TP-09).
- Never skip, delete or weaken a test to make a gate pass (TST-15).
- Check that generated tests verify the requirement and would fail if the code were wrong (AGT-11).
