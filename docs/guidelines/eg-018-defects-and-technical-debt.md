---
id: EG-018
title: "Defect and technical debt management"
status: draft
owner: "Test and quality lead"
version: 0.1.0
part: "Verification"
related: [EG-017, EG-019, EG-020, EG-021, EG-024]
review-by: 2027-09-30
supersedes:
---

- **Owner:** Test and quality lead
- **Applies to:** All defects and technical debt in product and tooling
- **Enforcement:** Tracker configuration, review, release criteria
- **Related:** [EG-017](eg-017-testing-principles-and-strategy.md), [EG-019](eg-019-logging-debug-and-diagnostics.md), [EG-020](eg-020-observability-and-telemetry.md), [EG-021](eg-021-release-update-and-production.md), [EG-024](eg-024-planning-delivery-and-improvement.md)

> **Note:** Rules marked *(core)* apply to every product and cannot be tailored. Other rules, and all numeric values, are proposed defaults that a product may tailor in its conformance profile ([EG-001](eg-001-guidelines-governance.md)).

## Purpose

Handle defects and technical debt consistently: visible, classified, analysed and closed with evidence, so that each one improves the process and none is hidden.

## Rules

1. **DEF-01** *(core)* All defects MUST be recorded in the tracker. Private lists MUST NOT be used. A record includes version found, environment, steps, expected and actual results, severity, component, linked requirement and logs or dumps.
1. **DEF-02** *(core)* Severity MUST follow the definitions below. Priority is set separately by the product owner.
1. **DEF-03** New defects MUST be triaged within two working days. Fix targets are set by severity.
1. **DEF-04** A defect lifecycle is `new`, `triaged`, `in progress`, `fixed`, `verified`, `closed`. Verification MUST be done by someone other than the fixer, and closure requires a regression test (TST-07).
1. **DEF-05** Root cause analysis MUST be done for severity 1 and 2 defects and for escapes. The cause is categorised as requirement, design, code, test gap, tooling or process.
1. **DEF-06** For each escape, the team MUST ask which gate should have caught it, and record the improvement to that gate.
1. **DEF-07** Commits and PRs MUST reference the defect (`Refs:`). Release notes MUST list fixed defects and known issues.
1. **DEF-08** Field defects MUST have a defined intake route, reproduction using diagnostics ([EG-019](eg-019-logging-debug-and-diagnostics.md)), and notification to the release manager. Security defects follow [EG-022](eg-022-security-and-data-protection.md).
1. **DEF-09** Technical debt MUST be recorded in the tracker with a `tech-debt` label, impact, cost estimate and owner, and be visible in a debt register.
1. **DEF-10** Capacity MUST be reserved for debt reduction each iteration (proposed 10 to 20 percent). Debt older than six months MUST be reviewed.
1. **DEF-11** Debt taken deliberately (for example to meet a date) MUST be recorded with a repayment plan and expiry.
1. **DEF-12** Static analysis suppressions and guideline deviations count as debt and MUST be tracked (COD-05, GOV-09).
1. **DEF-13** Defect and debt metrics (trends, escape rate, age, reopen rate) MUST be reviewed for improvement ([EG-024](eg-024-planning-delivery-and-improvement.md)) and MUST NOT be used to rank individuals.

## Severity definitions

| Severity | Definition | Examples |
|----------|------------|----------|
| 1 Critical | Safety hazard, security compromise, data loss, or fleet-wide failure without recovery | Bricking update failure, key exposure |
| 2 Major | Requirement not met with no workaround, or widespread degradation | Missed real-time deadline in normal use |
| 3 Minor | Requirement not met with a workaround, or limited impact | Incorrect diagnostic counter |
| 4 Trivial | Cosmetic or documentation defect | Typo in a log message |

## Compliance

| Rule | Checked by |
|------|------------|
| DEF-01, DEF-02, DEF-09 | Tracker required fields and workflow |
| DEF-04 | Workflow enforcement and CI regression test check |
| DEF-05, DEF-06 | Postmortem records ([EG-024](eg-024-planning-delivery-and-improvement.md)) |
| DEF-10 | Iteration planning review |

## Checklist

Tick an item when it is true for your project. Rule IDs point to the detail above.

- [ ] All defects are in the tracker with the required fields (DEF-01)
- [ ] Severity uses the agreed definitions, with priority set separately (DEF-02)
- [ ] New defects are triaged within two working days (DEF-03)
- [ ] The lifecycle is followed, verification is by someone else and closure needs a regression test (DEF-04)
- [ ] Root cause analysis is done for severity 1 and 2 defects and escapes (DEF-05)
- [ ] Each escape asks which gate should have caught it (DEF-06)
- [ ] Commits reference defects and release notes list fixes and known issues (DEF-07)
- [ ] A field defect route exists, with reproduction and release manager notification (DEF-08)
- [ ] Technical debt is recorded with label, impact, estimate and owner (DEF-09)
- [ ] Capacity is reserved for debt and old debt is reviewed (DEF-10)
- [ ] Deliberate debt has a repayment plan and expiry (DEF-11)
- [ ] Suppressions and deviations are tracked as debt (DEF-12)
- [ ] Metrics are used for improvement and not for ranking individuals (DEF-13)

## Applying to personal projects and AI agents

### Personal projects

Starts at the **Standard** profile (see [personal-projects.md](personal-projects.md)). An issue list with `bug` and `tech-debt` labels is enough. Reproduce, add a regression test, and note the root cause for anything serious. Keep a short debt list and clear it regularly.

### AI agents

- When fixing a defect, reproduce it with a test first, fix it, reference it in the commit (`Refs:`) and record the root cause category in the PR (DEF-05).
- Log unrelated problems you notice as tech-debt items instead of fixing them in passing (CP-16, DEF-09).
- Never close a defect without a regression test (DEF-04).
