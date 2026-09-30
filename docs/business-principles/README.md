# Business & Vertical Principles Overview

## Generic Guidelines vs. Business & Vertical Principles

In this engineering framework:

- **Engineering Guidelines (`EG-001` – `EG-026`)** are **generic processes and mechanisms**. They define standard governance, version control rules, pull request workflows, CI/CD pipeline structures, test strategies, and compliance tracking that apply universally regardless of domain.
- **Principles (Architecture, Coding, Development)** are **specific to a business, product line, or industry vertical** (e.g., Automotive Embedded, Medical Devices, Cloud SaaS, High-Frequency Trading, Aerospace).

> **Key Rule:** Principles MUST NOT be hardcoded into generic process guidelines. Instead, each business unit or vertical selects, tailors, or plugs in its domain principles into the generic guideline governance model.

---

## Domain & Vertical Principle Catalogs

Organizations and product teams adopt principle catalogs tailored to their specific domain:

1. **[Reference Business Principles Catalogue](principles.md):** Core guiding principles, architecture principles (AP-01 to AP-17), coding principles (CP-01 to CP-20), and lifecycle principles.
2. **Embedded & Real-Time Systems:** Prioritizes deterministic timing (AP-12), memory budgets (AP-06), safety containment (AP-10), and hardware isolation (AP-03).
3. **Cloud & Microservices:** Prioritizes horizontal scalability, event-driven decoupling (AsyncAPI), zero-downtime releases, and telemetry (EG-020).
4. **Regulated / Medical / Automotive:** Prioritizes strict requirement traceability (EG-006), hazard analysis, certification profiles (EG-023), and formal verification.

---

## How Business Principles Integrate with Guidelines

| Guideline Governance | How Business Principles Integrate |
|---|---|
| **[EG-007 Architecture Principles Governance](../guidelines/eg-007-architecture-principles.md)** | Defines *how* ADRs cite principles and how CI enforces budget/dependency rules. The business supplies the active principle IDs (e.g., `AP-01`). |
| **[EG-012 Coding Principles Governance](../guidelines/eg-012-coding-principles.md)** | Defines *how* code reviews and static analysis enforce coding rules. The vertical supplies language-specific coding standards (e.g., MISRA, AUTOSAR, PEP8). |
| **[EG-008 Decision Records (ADRs)](../guidelines/eg-008-decision-records.md)** | ADRs cite active business principle IDs when recording architectural tradeoffs. |
