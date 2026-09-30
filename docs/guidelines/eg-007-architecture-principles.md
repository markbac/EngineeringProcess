---
id: EG-007
title: "Architecture principles governance"
status: draft
owner: "Architecture group"
version: 0.1.0
part: "Requirements, architecture and design"
related: [EG-003, EG-008, EG-012, EG-010]
review-by: 2027-09-30
supersedes:
---

- **Owner:** Architecture group
- **Applies to:** Architecture governance and decision-making across products and teams
- **Enforcement:** Architecture review, ADRs, CI (dependency direction and resource budget checks)
- **Related:** [EG-003](eg-003-quality-policy-and-attributes.md), [EG-008](eg-008-decision-records.md), [EG-012](eg-012-coding-principles.md), [EG-010](eg-010-components-reuse-and-variants.md)

> **Architectural Note:** Guidelines are generic process standards. Actual architectural principles (e.g. AP-01 to AP-17) are defined per business, product line, or vertical market in [Business Principles](../business-principles/README.md). This guideline governs how business principles are declared, cited, and enforced.

---

## Purpose

Principles are the durable reasons behind architecture decisions. Guidelines define the generic governance framework; business verticals supply the domain-specific principles (e.g. automotive safety vs. cloud microservices).

This guideline establishes the mandatory rules for citing, reviewing, and enforcing business principles across engineering teams and AI agents.

---

## Governance Rules

1. **PRN-01** ADRs and RFCs MUST cite the active business/vertical principle IDs (from `docs/business-principles/`) that drove or constrained the decision.
2. **PRN-02** A decision that deviates from an established business principle MUST explicitly record the deviation in its ADR, including rationale and risk mitigation.
3. **PRN-03** Where principles conflict, the business unit's precedence order applies unless an approved ADR defines a product-specific exception.
4. **PRN-04** Where a business principle can be checked automatically (dependency direction, resource budgets, schema compatibility), enforcement MUST be integrated into CI.
5. **PRN-05** Business principles MUST be reviewed annually by the business unit lead and modified only via an RFC.
6. **PRN-06** Products MAY tailor principle precedence using their quality attribute profile ([EG-003](eg-003-quality-policy-and-attributes.md)).

---

## Principle Enforcement Mechanics

```text
Business Vertical Principles (e.g. AP-02 Layered Dependencies)
            │
            ▼
Generic Guideline Governance (EG-007 PRN-01 to PRN-06)
            │
            ▼
Automated Pipeline Enforcement (CI Check / Architecture Review / ADR)
```

---

## Compliance

| Rule | Checked By |
|---|---|
| **PRN-01, PRN-02** | Architecture review & principles field in [ADR template](../templates-reference/adr.md) |
| **PRN-04** | Pipeline checks (dependency direction, memory/CPU budgets, contract compatibility) |
| **PRN-05** | Annual governance review date |

---

## Checklist

- [ ] Active business principles are selected from [Business Principles](../business-principles/README.md) for the product (PRN-05)
- [ ] ADRs and RFCs cite business principle IDs (PRN-01)
- [ ] Deviations from business principles are recorded in ADRs with trade-off rationale (PRN-02)
- [ ] Automated architecture rules (budgets, dependency direction) run in CI pipeline (PRN-04)
