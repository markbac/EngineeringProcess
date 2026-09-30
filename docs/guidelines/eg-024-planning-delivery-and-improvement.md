---
id: EG-024
title: "Planning, delivery and improvement"
status: draft
owner: "Engineering manager"
version: 0.1.0
part: "Delivery, research and people"
related: [EG-002, EG-003, EG-018, EG-020, EG-021]
review-by: 2027-09-30
supersedes:
---

- **Owner:** Engineering manager
- **Applies to:** All planning, delivery management and improvement activity
- **Enforcement:** Tracker configuration, review, retrospectives
- **Related:** [EG-002](eg-002-values-and-ways-of-working.md), [EG-003](eg-003-quality-policy-and-attributes.md), [EG-018](eg-018-defects-and-technical-debt.md), [EG-020](eg-020-observability-and-telemetry.md), [EG-021](eg-021-release-update-and-production.md)

> **Note:** Rules marked *(core)* apply to every product and cannot be tailored. Other rules, and all numeric values, are proposed defaults that a product may tailor in its conformance profile ([EG-001](eg-001-guidelines-governance.md)).

## Purpose

Plan honestly, deliver visibly and learn continuously: shared definitions of ready and done, forecasts that admit uncertainty, managed risks and dependencies, and a small set of metrics used for improvement.

## Rules

1. **PLN-01** Work MUST be planned in time-boxed iterations or flow with a visible backlog. Every item traces to a requirement, a defect or an approved improvement (REQ-13).
1. **PLN-02** Each work item type MUST have a Definition of Ready (below).
1. **PLN-03** Each work item type MUST have a Definition of Done (below), and the PR template checklist reflects it.
1. **PLN-04** Estimates SHOULD be relative or ranges, calibrated from history. Forecasts MUST be given as ranges with stated confidence and be updated regularly. Single-point commitments MUST NOT be made for uncertain work.
1. **PLN-05** A risk register MUST be kept (ID, description, cause, impact, probability, exposure, mitigation, owner, trigger, review date), reviewed at least fortnightly, with top risks visible to the sponsor.
1. **PLN-06** Dependencies across teams, sites, hardware and vendors MUST be recorded with an owner and a need-by date.
1. **PLN-07** Escalation thresholds MUST be defined for risk exposure, schedule slip and blocked time (proposed: blocked for more than two working days) and follow VAL-04.
1. **PLN-08** Capacity MUST be reserved for support, technical debt (DEF-10) and improvement.
1. **PLN-09** A small set of metrics MUST be agreed and tracked: lead time, release frequency, change failure rate, time to restore, escaped defects, review latency, build stability and flaky test rate. Metrics are used at team level for improvement and MUST NOT be used to rank individuals.
1. **PLN-10** Retrospectives MUST be held at a fixed cadence. Actions have an owner and date in the tracker and are reviewed at the next retrospective.
1. **PLN-11** Blameless postmortems MUST be held for severity 1 and 2 escapes, failed releases, pipeline outages and security incidents. They follow the template below and are published within five working days.
1. **PLN-12** Process and tooling improvements MUST be treated as first-class work in the backlog, tied to the metrics.
1. **PLN-13** Friction with a guideline MUST be raised as an issue or RFC, so that guidelines are kept useful (GOV-06).
1. **PLN-14** Status reporting SHOULD be derived from tracker and pipeline data, not compiled manually.

## Definition of Ready

| Work item type | Ready when |
|----------------|------------|
| Feature | Requirement linked and approved, acceptance criteria stated, dependencies identified, estimate given, need for an ADR or RFC decided |
| Defect | Reproducible or diagnostics attached, severity assigned, component identified |
| Technical debt or improvement | Impact described, scope bounded, owner named |
| Spike | Question stated, time-box set, exit criteria defined ([EG-025](eg-025-research-and-prototyping.md)) |

## Definition of Done

| Work item type | Done when |
|----------------|-----------|
| Feature | Reviewed and merged, tests added and passing, requirement trace updated, documentation updated, ADR written if needed, logging and diagnostics added, budgets checked |
| Defect | Root cause recorded, regression test added, fix verified by someone else |
| Technical debt or improvement | Change merged, debt register and documentation updated |
| Spike | Findings recorded in an experiment record and a decision made |

## Postmortem template

```markdown
## Summary
## Impact
## Timeline
## Contributing factors
## What went well
## Actions (owner and date)
```

## Compliance

| Rule | Checked by |
|------|------------|
| PLN-02, PLN-03 | Tracker workflow and PR template |
| PLN-05, PLN-06 | Risk register and dependency register reviews |
| PLN-09 | Metrics dashboard generated from tracker and pipeline data |
| PLN-10, PLN-11 | Action tracking in the tracker |

## Checklist

Tick an item when it is true for your project. Rule IDs point to the detail above.

- [ ] Work is planned in time-boxed iterations or flow with a visible backlog, and every item is traceable (PLN-01)
- [ ] A Definition of Ready exists per work item type (PLN-02)
- [ ] A Definition of Done exists per type and the PR template reflects it (PLN-03)
- [ ] Estimates are ranges and forecasts state confidence (PLN-04)
- [ ] A risk register is maintained and reviewed fortnightly (PLN-05)
- [ ] Dependencies are recorded with an owner and need-by date (PLN-06)
- [ ] Escalation thresholds are defined (PLN-07)
- [ ] Capacity is reserved for support, debt and improvement (PLN-08)
- [ ] A small metric set is tracked and not used to rank individuals (PLN-09)
- [ ] Retrospectives are held and actions are tracked (PLN-10)
- [ ] Blameless postmortems follow severity 1 and 2 escapes, failed releases, outages and security incidents (PLN-11)
- [ ] Improvements are first-class backlog items (PLN-12)
- [ ] Friction with a guideline is raised as an issue or RFC (PLN-13)
- [ ] Status is derived from tracker and pipeline data (PLN-14)

## Applying to personal projects and AI agents

### Personal projects

Starts at the **Full** profile (see [personal-projects.md](personal-projects.md)). A backlog, a short Definition of Done and a five-line risk list are enough. Hold a short retrospective after each release or milestone. Skip formal metrics unless they help you.

### AI agents

- Treat the Definition of Done for the work item type as the finish line: reviewed, tested, documented, traced, with diagnostics and budgets checked (PLN-03).
- State uncertainty as a range and not a single date (PLN-04).
- Report blockers and risks in the PR or task summary and do not work around them silently (PLN-05, PLN-06).
- Draft postmortems from the template when asked (PLN-11).
