---
id: EG-001
title: "Guidelines governance"
status: draft
owner: "Architecture group"
version: 0.1.0
part: "Foundations"
related: [EG-004, EG-008]
review-by: 2027-09-30
supersedes:
---

- **Owner:** Architecture group
- **Applies to:** All engineering teams, sites and agents
- **Enforcement:** CI (front matter and link checks), review
- **Related:** [EG-004](eg-004-documentation-as-code.md), [EG-008](eg-008-decision-records.md)
- **Principles:** GP-01 to GP-10 (see [principles.md](../business-principles/principles.md))

> **Note:** Rules marked *(core)* apply to every product and cannot be tailored. Other rules, and all numeric values, are proposed defaults that a product may tailor in its conformance profile ([EG-001](eg-001-guidelines-governance.md)).

## Purpose

Define how guidelines are written, approved, changed, retired and enforced, so that every other guideline is consistent.

## Rules

1. **GOV-01** *(core)* Every guideline MUST have a unique ID (`EG-nnn`), a named owner, a status (`draft`, `active`, `deprecated`), a version and a review-by date in its front matter.
1. **GOV-02** Every guideline MUST follow the standard template (below).
1. **GOV-03** Every rule MUST have a stable ID and use RFC 2119 keywords. A rule SHOULD carry a brief rationale where the reason is not obvious.
1. **GOV-04** Every guideline MUST state how compliance is checked: tooling, review, or manual audit. A rule with no check MUST be marked as advisory.
1. **GOV-05** A guideline SHOULD be short enough to read in one sitting. Longer material belongs in supporting how-to documents.
1. **GOV-06** *(core)* New guidelines and material changes MUST go through an RFC ([EG-008](eg-008-decision-records.md)), unless the change is editorial.
1. **GOV-07** *(core)* Changes MUST be made by pull request, approved by the owner and by at least one practitioner subject to the rule.
1. **GOV-08** Guidelines MUST be reviewed at least every 12 months. CI reports overdue reviews.
1. **GOV-09** *(core)* A deviation MUST be recorded as an exception with owner approval, scope, reason and expiry date. A permanent deviation means the rule is wrong and SHOULD be changed.
1. **GOV-10** Deprecated guidelines MUST remain in the repository with a pointer to their replacement.
1. **GOV-11** A guideline SHOULD include one correct and one incorrect example where this aids understanding.
1. **GOV-12** Guideline versions follow semantic versioning: MAJOR when a rule makes previously compliant work non-compliant, MINOR for new rules, PATCH for wording.
1. **GOV-13** Guidelines MUST be stored in `docs/guidelines/`, one file per guideline, named `eg-nnn-short-title.md`. The index MUST be generated from front matter.
1. **GOV-14** Each guideline MUST be assigned to a named owner who is accountable for keeping it useful, and who is the first contact for questions and exception requests.
1. **GOV-15** *(core)* Rules MUST be classified as core or tailorable. Core rules apply to every product without tailoring and are marked *(core)*. All other rules, and all numeric values, are defaults that a product MAY tailor through its conformance profile (GOV-16). The core set is kept small so that products stay consistent where it matters and free elsewhere.
1. **GOV-16** *(core)* Each product MUST have a conformance profile recording which guidelines apply, any tailored rules and values with the reason, approved exceptions, the components it uses and provides (COM-01), and its toolchain. The product's technical lead owns the profile and approves tailoring of non-core rules, and the architecture group is informed at its forum (RFC-11). Exceptions to core rules need the guideline owner's approval (GOV-09).

## Standard template

1. Header block: owner, applies to, enforcement, related guidelines
1. Purpose (why this exists, in two or three sentences)
1. Rules (with IDs, keywords and rationale where needed)
1. Supporting material (tables, templates, diagrams, examples)
1. Compliance (how each rule is checked, and by what)

## Front matter

```yaml
id: EG-000
title: Short title
status: draft
owner: Role
version: 0.1.0
part: Foundations
related: [EG-000]
review-by: 2027-09-30
supersedes:
```

The header block at the top of each guideline body carries the applies-to, enforcement and related guidelines for human readers.

## Compliance

| Rule | Checked by |
|------|------------|
| GOV-01, GOV-08, GOV-13 | CI: front matter schema validation and index generation |
| GOV-02, GOV-04 | CI: required headings check |
| GOV-06, GOV-07 | Branch protection and CODEOWNERS on `docs/guidelines/` |
| GOV-09 | Exception register review at each guideline review |
| GOV-15, GOV-16 | CI: core rule list generated from the guidelines, profile schema validation and comparison against the core list |

## Checklist

Tick an item when it is true for your project. Rule IDs point to the detail above.

- [ ] Guidelines live in `docs/guidelines/`, one file per guideline, named `eg-nnn-short-title.md` (GOV-13)
- [ ] Every guideline has front matter with id, title, status, owner, version and review-by (GOV-01)
- [ ] Every guideline follows the standard template and states how compliance is checked (GOV-02, GOV-04)
- [ ] Rules have stable IDs and RFC 2119 keywords, with a rationale where it is not obvious (GOV-03)
- [ ] Each guideline is short enough to read in one sitting, with examples where they help (GOV-05, GOV-11)
- [ ] Changes are made by PR with owner and practitioner approval, and by RFC when material (GOV-06, GOV-07)
- [ ] Review-by dates are checked by CI and no guideline is overdue (GOV-08)
- [ ] Exceptions are recorded with owner, scope, reason and expiry (GOV-09)
- [ ] Deprecated guidelines are kept with a pointer to their replacement (GOV-10)
- [ ] Guideline versions follow semantic versioning (GOV-12)
- [ ] The index is generated from front matter (GOV-13)
- [ ] Each guideline has an accountable owner who handles questions and exception requests (GOV-14)
- [ ] Core rules are marked and applied identically across products, and all other rules are tailored only through the product profile (GOV-15)
- [ ] Each product has a conformance profile recording applicability, thresholds, exceptions, components and toolchain (GOV-16)

## Applying to personal projects and AI agents

### Personal projects

Starts at the **Standard** profile (see [personal-projects.md](personal-projects.md)). Keep the files and IDs so rules can be cited. Skip owners, review-by cycles and RFCs, because you are the owner. Record which guidelines you adopted in ADR-0001.

### AI agents

- Do not edit anything in `docs/guidelines/` unless the task explicitly says so (AGT-05).
- Cite rules by ID.
- If a rule blocks the task, stop and ask rather than deviating (GOV-09).
