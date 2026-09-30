---
id: EG-020
title: "Observability and telemetry"
status: draft
owner: "Platform lead"
version: 0.1.0
part: "Diagnostics and field insight"
related: [EG-003, EG-018, EG-019, EG-021, EG-022]
review-by: 2027-09-30
supersedes:
---

- **Owner:** Platform lead
- **Applies to:** Devices, backend platform and the tooling that receives and displays their data
- **Enforcement:** CI (schema checks), review, release criteria
- **Related:** [EG-003](eg-003-quality-policy-and-attributes.md), [EG-018](eg-018-defects-and-technical-debt.md), [EG-019](eg-019-logging-debug-and-diagnostics.md), [EG-021](eg-021-release-update-and-production.md), [EG-022](eg-022-security-and-data-protection.md)

> **Note:** Rules marked *(core)* apply to every product and cannot be tailored. Other rules, and all numeric values, are proposed defaults that a product may tailor in its conformance profile ([EG-001](eg-001-guidelines-governance.md)).

## Purpose

Define what we must be able to know about devices in the field and in the lab, how that data is collected, structured and protected, and how it feeds back into engineering decisions.

## Rules

1. **OBS-01** Each product MUST define its observability requirements: the questions the team must be able to answer about a device and the fleet (is it healthy, which version, what failed, did the update succeed, what are the resource margins). These are captured as requirements ([EG-006](eg-006-requirements-and-traceability.md)).
1. **OBS-02** The telemetry schema MUST be documented and versioned with an owner. Metric names, units and types (counter, gauge, event) MUST follow naming conventions, and schema changes follow semantic versioning with backward compatibility.
1. **OBS-03** Every record MUST carry context: pseudonymous device ID, firmware version, hardware revision, configuration version, boot count and time source.
1. **OBS-04** Bandwidth, battery, storage and cost budgets per device MUST be defined, with sampling and aggregation policy to stay within them.
1. **OBS-05** Telemetry MUST follow data minimisation and the data classification ([EG-022](eg-022-security-and-data-protection.md)). Personal data MUST NOT be collected without approval. Retention periods MUST be defined.
1. **OBS-06** Transport MUST handle offline buffering, back-pressure, ordering, de-duplication and loss detection.
1. **OBS-07** Backend ingestion, storage, dashboards and alerts MUST be defined as code and versioned.
1. **OBS-08** Fleet health indicators and objectives MUST be defined (for example update success rate, crash-free rate, connectivity). Every alert has an owner, a runbook and a required action. Alerts without actions MUST NOT exist.
1. **OBS-09** Update rollouts MUST use telemetry health gates with automatic halt criteria ([EG-021](eg-021-release-update-and-production.md)).
1. **OBS-10** Field insights MUST be reviewed at least monthly and fed into defect triage, requirements and test gaps ([EG-018](eg-018-defects-and-technical-debt.md), [EG-024](eg-024-planning-delivery-and-improvement.md)).
1. **OBS-11** Lab and HIL environments SHOULD emit the same telemetry, so that parsers and dashboards are exercised before release.
1. **OBS-12** Telemetry data quality MUST be checked: schema validation, gap and anomaly detection, and time source checks.
1. **OBS-13** Operational runbooks MUST exist for the top alerts and be kept with the dashboards and alert definitions.

## Signals

| Signal | Answers | Examples |
|--------|---------|----------|
| Logs | What happened, in what order | Event records, fault codes |
| Metrics | How much, how often, how healthy | Counters, gauges, resource margins |
| Events | Significant state changes | Boot, update result, connectivity change |
| Dumps | Why did it fail | Crash dump with build ID |

## Compliance

| Rule | Checked by |
|------|------------|
| OBS-02, OBS-03 | CI: schema validation and compatibility check |
| OBS-05 | Privacy review, telemetry field register |
| OBS-07, OBS-08 | Code review of dashboards and alerts, alert audit |
| OBS-10 | Monthly review record |

## Checklist

Tick an item when it is true for your project. Rule IDs point to the detail above.

- [ ] Observability requirements are defined per product (OBS-01)
- [ ] The telemetry schema is versioned, owned and follows naming conventions (OBS-02)
- [ ] Every record carries device, firmware, hardware, configuration and time context (OBS-03)
- [ ] Bandwidth, battery, storage and cost budgets exist with a sampling policy (OBS-04)
- [ ] Data minimisation, classification and retention are applied (OBS-05)
- [ ] Transport handles offline buffering, ordering, de-duplication and loss detection (OBS-06)
- [ ] Backend, dashboards and alerts are defined as code (OBS-07)
- [ ] Health indicators and objectives are defined, and every alert has an owner, runbook and action (OBS-08, OBS-13)
- [ ] Rollouts are gated by telemetry with automatic halt criteria (OBS-09)
- [ ] Field insights are reviewed monthly and fed into triage and tests (OBS-10)
- [ ] Lab and HIL environments emit the same telemetry (OBS-11)
- [ ] Data quality checks are in place (OBS-12)

## Applying to personal projects and AI agents

### Personal projects

Starts at the **Full** profile (see [personal-projects.md](personal-projects.md)). Needed only if the project runs somewhere you cannot see. Define three or four health questions, emit versioned metrics and set a few alerts that each have an action. Skip it for local tools.

### AI agents

- Do not add telemetry fields without updating the versioned schema and classification (OBS-02, OBS-05).
- Give every metric a name, unit and type per the convention (OBS-02).
- Never add personal data to telemetry (OBS-05).
- Do not add alerts without an owner, runbook and action (OBS-08).
