---
id: EG-012
title: "Coding principles governance"
status: draft
owner: "Firmware and Software lead"
version: 0.1.0
part: "Code and build"
related: [EG-005, EG-013, EG-015]
review-by: 2027-09-30
supersedes:
---

- **Owner:** Firmware and Software lead
- **Applies to:** Code development by human engineers and AI agents
- **Enforcement:** Code review, static analysis, linter gates
- **Related:** [EG-005](eg-005-ai-agent-usage.md), [EG-013](eg-013-coding-standard.md), [EG-015](eg-015-pull-requests-and-review.md)

> **Development Note:** Generic guidelines govern code review workflows, PR quality gates, and surgical change boundaries. Specific coding principles (e.g. CP-01 to CP-20) are provided per business vertical or programming language domain in [Business Principles](../business-principles/README.md).

---

## Purpose

This guideline defines the generic governance for coding practices across projects. Specific coding rules (e.g., MISRA for embedded C, PEP8 for Python, or strict concurrency rules for cloud microservices) are configured per business vertical and programming domain.

---

## Governance Rules

1. **CPR-01** Every project MUST select and adopt a coding principles profile from [Business Principles](../business-principles/README.md) matching its tech stack and business vertical.
2. **CPR-02** Code changes MUST be surgical: touch only code necessary for the requirement or defect fix, preserving unrelated formatting and comments.
3. **CPR-03** Automated static analysis and linting MUST enforce coding principles in the local build and CI pipeline ([EG-016](eg-016-pipelines-and-quality-gates.md)).
4. **CPR-04** AI coding agents MUST cite active coding principle IDs when explaining implementation choices in pull requests or agent task briefs.

---

## Compliance

| Rule | Checked By |
|---|---|
| **CPR-01** | Product conformance profile ([EG-001](eg-001-guidelines-governance.md)) |
| **CPR-02, CPR-04** | Peer review & PR review checklist ([EG-015](eg-015-pull-requests-and-review.md)) |
| **CPR-03** | CI pipeline linter & static analysis quality gate |
