---
id: EG-002
title: "Engineering values and ways of working"
status: draft
owner: "Engineering manager"
version: 0.1.0
part: "Foundations"
related: [EG-008, EG-024, EG-026]
review-by: 2027-09-30
supersedes:
---

- **Owner:** Engineering manager
- **Applies to:** All team members and sites
- **Enforcement:** Review, retrospectives, ownership register checks
- **Related:** [EG-008](eg-008-decision-records.md), [EG-024](eg-024-planning-delivery-and-improvement.md), [EG-026](eg-026-competence-tooling-and-onboarding.md)
- **Principles:** EV-01 to EV-08 (see [principles.md](../business-principles/principles.md))

> **Note:** Rules marked *(core)* apply to every product and cannot be tailored. Other rules, and all numeric values, are proposed defaults that a product may tailor in its conformance profile ([EG-001](eg-001-guidelines-governance.md)).

## Purpose

State the values that tie the other guidelines together, and set out how the team makes decisions, resolves disagreements, and works across sites and time zones.

## Values

| ID | Value | Meaning in practice |
|----|-------|---------------------|
| EV-01 | Ownership | Every asset has a named owner accountable for its quality and future |
| EV-02 | Quality built in | Quality is produced by the way we work, not inspected in at the end |
| EV-03 | Written and open by default | Decisions, agreements and handovers are recorded where others can find them |
| EV-04 | Evidence over opinion | Claims about performance, defects and risk are backed by data |
| EV-05 | Blameless learning | We fix systems and processes, not people |
| EV-06 | Small steps | Small, frequent, reversible changes beat large, rare ones |
| EV-07 | Simplicity | The simplest solution that meets the need is preferred |
| EV-08 | Respect for others' time | Cross-site work is designed for time zones, and requests are clear and complete |

## Rules

1. **VAL-01** The values above SHOULD be used as tie-breakers when guidelines are silent and principles do not settle a question.
1. **VAL-02** Every component, guideline, pipeline, test rig and tool MUST have a named owner in CODEOWNERS or the ownership register. Unowned assets are reported monthly.
1. **VAL-03** Decision rights MUST be recorded in the decision rights table (below). The accountable person decides after consulting those affected.
1. **VAL-04** Disagreements escalate in steps: discuss directly, write it up as an RFC or ADR, sponsor decides, then architecture group or engineering manager. Each step has a time limit of five working days.
1. **VAL-05** After a decision, the team MUST disagree and commit. Reopening a decision needs new evidence, recorded in a new ADR.
1. **VAL-06** Decisions, agreements and handovers MUST be written down in the repository or tracker. Outcomes of meetings MUST be recorded within one working day.
1. **VAL-07** Every component MUST have one owning site and a named deputy at a second site, so that no knowledge or authority is site-exclusive.
1. **VAL-08** Cross-site working agreements MUST define core overlap hours, expected response time (acknowledge within one working day), and a handover note for work that passes between sites.
1. **VAL-09** All sites use the same tools, conventions and pipelines. A site-specific variant needs an ADR.
1. **VAL-10** Work status MUST be visible in the tracker and pipeline, so that status is read, not requested.
1. **VAL-11** Changes SHOULD be small enough to be reviewed within one working day.
1. **VAL-12** Raising a risk, a disagreement or a mistake MUST be treated as expected behaviour and never penalised.

## Decision rights

| Decision | Decides | Must consult |
|----------|---------|--------------|
| Component design within its boundary | Component owner | Architecture group |
| Interface between components or sites | Architecture group | Both component owners |
| Change to a guideline | Guideline owner, through an RFC | Affected teams |
| Adoption of a tool or dependency | Architecture group, through an RFC | Build and tooling lead, security lead |
| Release go or no-go | Release manager | Test and quality lead, security lead |
| Exception to a security rule | Security lead | Architecture group |
| Priority between work items | Product owner | Engineering manager |

## Handover note

A handover note between sites states: what was done, what is in progress and where, what is blocked and by whom, what needs a decision, and where the current state lives (branch, PR, ticket).

## Compliance

| Rule | Checked by |
|------|------------|
| VAL-02 | Ownership register and CODEOWNERS check in CI |
| VAL-04, VAL-05 | RFC and ADR history review |
| VAL-06, VAL-10 | Retrospective review, tracker audit |
| VAL-07, VAL-08 | Ownership register, quarterly cross-site review |

## Checklist

Tick an item when it is true for your project. Rule IDs point to the detail above.

- [ ] Values are published and used as tie-breakers (VAL-01)
- [ ] Every component, pipeline, rig and tool has a named owner in CODEOWNERS or the ownership register (VAL-02)
- [ ] The decision rights table is current (VAL-03)
- [ ] Escalation steps and time limits are agreed, and decisions are committed to once made (VAL-04, VAL-05)
- [ ] Decisions, agreements and meeting outcomes are written down within one working day (VAL-06)
- [ ] Each component has an owning site and a deputy at another site (VAL-07)
- [ ] Cross-site agreements cover overlap hours, response time and the handover note (VAL-08)
- [ ] All sites use the same tools and conventions, and variants have an ADR (VAL-09)
- [ ] Work status is visible in the tracker and pipeline (VAL-10)
- [ ] Changes are small enough to review within one working day (VAL-11)
- [ ] Raising a risk, disagreement or mistake is treated as expected behaviour (VAL-12)

## Applying to personal projects and AI agents

### Personal projects

Starts at the **Full** profile (see [personal-projects.md](personal-projects.md)). Keep written-by-default, small steps, simplicity and evidence over opinion. Decision rights collapse to you. Skip the cross-site rules.

### AI agents

- Prefer small, reviewable changes (VAL-11).
- Record decisions and assumptions in the PR or an ADR, not only in chat (VAL-06).
- Raise risks and doubts early and do not hide uncertainty (VAL-12).
