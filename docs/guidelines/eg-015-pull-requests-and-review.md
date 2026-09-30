---
id: EG-015
title: "Pull requests and code review"
status: draft
owner: "Firmware lead"
version: 0.1.0
part: "Code and build"
related: [EG-005, EG-006, EG-014, EG-016]
review-by: 2027-09-30
supersedes:
---

- **Owner:** Firmware lead
- **Applies to:** All changes to protected branches, by people and agents
- **Enforcement:** Branch protection, CODEOWNERS, PR template, CI
- **Related:** [EG-005](eg-005-ai-agent-usage.md), [EG-006](eg-006-requirements-and-traceability.md), [EG-014](eg-014-version-control-and-versioning.md), [EG-016](eg-016-pipelines-and-quality-gates.md)

> **Note:** Rules marked *(core)* apply to every product and cannot be tailored. Other rules, and all numeric values, are proposed defaults that a product may tailor in its conformance profile ([EG-001](eg-001-guidelines-governance.md)).

## Purpose

Ensure that no change reaches a protected branch without independent review and evidence, and that review effort is spent on design and correctness rather than on what tools can check.

## Rules

1. **PRR-01** *(core)* All changes to protected branches MUST be made by PR. Direct pushes MUST NOT be allowed, including for owners.
1. **PRR-02** *(core)* The PR title MUST follow Conventional Commits and becomes the squash commit message.
1. **PRR-03** The PR description MUST follow the template: what and why, linked requirement, ticket or ADR, test evidence, risk and rollback notes, documentation updated, breaking change flag and AI assistance disclosure.
1. **PRR-04** A PR SHOULD have one purpose and stay under about 400 changed lines, excluding generated files. Larger changes MUST be split or accompanied by a walkthrough.
1. **PRR-05** *(core)* CODEOWNERS MUST define required reviewers for each path. At least one owner approves every PR, and safety, security and certified areas need two.
1. **PRR-06** *(core)* Reviewers MUST be someone other than the author who understands the area. An agent MUST NOT count as an approver (AGT-04).
1. **PRR-07** Required checks MUST pass before human review begins. Reviewers MUST NOT re-check what tools check.
1. **PRR-08** Reviewers SHOULD use the review focus by change type (below).
1. **PRR-09** The first review response SHOULD be given within one working day. PRs stale for more than three working days are escalated (VAL-04).
1. **PRR-10** Review comments MUST be labelled `blocking`, `suggestion`, `question` or `nit`, and SHOULD cite rule IDs. Comments address intent and correctness before style.
1. **PRR-11** All blocking comments MUST be resolved. New commits that change the approach MUST dismiss stale approvals.
1. **PRR-12** Draft PRs MAY be used for early feedback. Stacked PRs MAY be used when their order is documented.
1. **PRR-13** After approval, the author merges by squash by default. The branch is deleted after merge.
1. **PRR-14** PR links MUST be retained as review evidence and referenced from release traceability.
1. **PRR-15** Architecture review MUST NOT be a routine PR requirement. Architects are added as reviewers only for changes that meet RFC-12, and all other PRs are reviewed by the component owner or their delegates.

## Review focus by change type

| Change type | Reviewer focus |
|-------------|----------------|
| Firmware logic | Correctness against the requirement, error handling, resource use, concurrency, tests |
| Hardware access | Register use, timing, errata, isolation behind the abstraction layer |
| Build and pipeline | Reproducibility, gate integrity, secrets, blast radius |
| Interfaces | Compatibility, versioning, contract tests, documentation |
| Security-relevant code | Trust boundaries, input validation, key handling, threat model update |
| Documentation | Accuracy against code, structure, glossary use |
| Requirements | Testability, atomicity, allocation, change impact |

## PR template

```markdown
## What and why

## Links
- Requirement:
- Ticket:
- ADR or RFC:

## Evidence
- Tests run and results:
- Analysis and size or timing impact:

## Risk and rollback

## Checklist
- [ ] Documentation updated
- [ ] Breaking change flagged
- [ ] AI assistance disclosed (Assisted-by)
- [ ] Certified or regulated area touched (EG-023)
```

## Compliance

| Rule | Checked by |
|------|------------|
| PRR-01, PRR-05, PRR-06, PRR-11 | Branch protection and CODEOWNERS |
| PRR-02, PRR-03 | CI: PR title and template checks |
| PRR-04 | CI: diff size warning |
| PRR-15 | CODEOWNERS scope review |
| PRR-09 | Review latency metric ([EG-024](eg-024-planning-delivery-and-improvement.md)) |

## Checklist

Tick an item when it is true for your project. Rule IDs point to the detail above.

- [ ] All changes to protected branches go through PR with no direct pushes (PRR-01)
- [ ] PR titles follow Conventional Commits (PRR-02)
- [ ] PR descriptions follow the template (PRR-03)
- [ ] PRs have one purpose and stay around 400 changed lines or fewer, excluding generated files (PRR-04)
- [ ] CODEOWNERS define required reviewers, with two for safety, security and certified areas (PRR-05)
- [ ] Reviewers are not the author and understand the area, and agents do not approve (PRR-06)
- [ ] Required checks pass before human review (PRR-07)
- [ ] Reviewers use the review focus for the change type (PRR-08)
- [ ] First response is within one working day and stale PRs are escalated (PRR-09)
- [ ] Comments are labelled and cite rule IDs (PRR-10)
- [ ] Blocking comments are resolved and stale approvals dismissed (PRR-11)
- [ ] Draft and stacked PRs are used where helpful, with documented order (PRR-12)
- [ ] PRs merge by squash and branches are deleted (PRR-13)
- [ ] PR links are kept as review evidence (PRR-14)
- [ ] Architecture review is not a routine PR requirement, and other PRs are reviewed by component owners (PRR-15)

## Applying to personal projects and AI agents

### Personal projects

Starts at the **Standard** profile (see [personal-projects.md](personal-projects.md)). Still use PRs, mainly for agent work and for reviewing your own diff. Self-review with the template checklist. Waive CODEOWNERS and turnaround rules, but keep 'CI must pass before merge' and 'small PRs'.

### AI agents

- Open a PR with a Conventional Commit title and the filled template: what and why, links, evidence, risk and checklist (PRR-02, PRR-03).
- Keep to one purpose per PR and roughly under 400 lines excluding generated files (PRR-04).
- Label your review comments blocking, suggestion, question or nit (PRR-10).
- Never approve or merge your own PR (PRR-06).
- Wait for required checks and fix failures instead of bypassing them (PRR-07).
