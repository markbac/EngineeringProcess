---
id: EG-012
title: "Coding principles"
status: draft
owner: "Firmware lead"
version: 0.1.0
part: "Code and build"
related: [EG-005, EG-007, EG-013, EG-019]
review-by: 2027-09-30
supersedes:
---

- **Owner:** Firmware lead
- **Applies to:** All source code, build scripts and test code, by people and agents
- **Enforcement:** Formatter, compiler, static analysis, review
- **Related:** [EG-005](eg-005-ai-agent-usage.md), [EG-007](eg-007-architecture-principles.md), [EG-013](eg-013-coding-standard.md), [EG-019](eg-019-logging-debug-and-diagnostics.md)
- **Principles:** CP-01 to CP-21 (defined below)

> **Note:** Rules marked *(core)* apply to every product and cannot be tailored. Other rules, and all numeric values, are proposed defaults that a product may tailor in its conformance profile ([EG-001](eg-001-guidelines-governance.md)).

## Purpose

Set out the language-neutral principles from which the coding standard ([EG-013](eg-013-coding-standard.md)) is derived. When the standard is silent or ambiguous, the principles decide.

## Rules

1. **CPR-01** *(core)* The coding standard MUST derive from these principles, and each of its rules SHOULD cite the principle it serves.
1. **CPR-02** Review comments SHOULD cite a principle or rule ID, so that feedback is consistent and explainable.
1. **CPR-03** Deviations MUST be recorded as required by GOV-09, in the code (suppression with rule ID and reason) and in the deviation log.
1. **CPR-04** Where a principle can be checked by a tool, it MUST be enforced in CI rather than left to review.

## Principles

| ID | Principle | Statement | Typical implications |
|----|-----------|-----------|----------------------|
| CP-01 | Clarity over cleverness | Code is read far more often than it is written. Write for the next reader. | Plain constructs and descriptive names. Anything clever is explained. |
| CP-02 | Simplicity, no speculation | Write the minimum code that solves the stated problem. | No unrequested features, no abstractions for single use, no configurability nobody asked for. |
| CP-03 | Correct first, then small and fast | Optimise against measured budgets, not intuition. | Measure before optimising. Record the reason for any non-obvious optimisation. |
| CP-04 | Make wrong code hard to write | Use types, `const`, enumerations and narrow interfaces to prevent misuse. | Distinct types over raw integers, no ambiguous boolean parameters, invalid states unrepresentable where practical. |
| CP-05 | Validate at boundaries, assert invariants | Check external input where it enters the system. Assert what must never be false. | Every interface, protocol parser and configuration loader validates. Assertion policy follows [EG-019](eg-019-logging-debug-and-diagnostics.md). |
| CP-06 | No silent failure | Errors are detected and either handled or propagated, never ignored. | Return values checked, error codes defined, every failure path has defined behaviour. |
| CP-07 | Predictable resource use | Memory, stack and execution time are bounded and known. | Static allocation by default, bounded loops, stack usage analysed. |
| CP-08 | No undefined behaviour | Do not rely on behaviour the language leaves undefined or unspecified. | Restricted language subset, warnings as errors, static analysis, sanitisers in host tests. |
| CP-09 | Limit shared state | Minimise globals and shared mutable data. State has one owner. | Documented ownership and locking or message-passing rules, `const` by default. |
| CP-10 | High cohesion, low coupling | Small units with one clear responsibility and narrow interfaces. | Size guidance for functions and modules, dependency direction respected (AP-02). |
| CP-11 | Keep hardware separate from logic | Logic never touches registers or vendor APIs directly. | Hardware abstraction layer, logic testable on the host (AP-07). |
| CP-12 | Code and tests together | Code is written to be tested, and changes arrive with their tests. | Tests in the same PR, requirement IDs in test names, a bug fix starts with a failing test. |
| CP-13 | Comments explain why | Names and structure say what. Comments record intent, constraints and non-obvious reasons. | No comments that restate the code. Reference the requirement, ADR or erratum where relevant. |
| CP-14 | Consistency over preference | Follow the agreed style and existing conventions, even where you would choose differently. | Formatter and linter enforce style, so there are no style debates in review. |
| CP-15 | Warnings are defects | The build is free of compiler and analyser warnings. | Warnings as errors. Suppressions are inline, justified and reviewed. |
| CP-16 | Surgical changes | Change only what the task needs, and clean up only what your own change made redundant. | Small diffs. Every changed line traces to the request. Unrelated problems are reported, not fixed in passing. |
| CP-17 | Secure by habit | Treat all input as untrusted and avoid unsafe constructs. | Banned function list, no secrets in code, safe buffer handling, constant-time comparison for secrets. |
| CP-18 | Observable by construction | Code emits what is needed to understand its behaviour in the field. | Logging and fault reporting follow [EG-019](eg-019-logging-debug-and-diagnostics.md). |
| CP-19 | Duplication over the wrong abstraction | Abstract when a pattern is proven, not before. | Rule of three, and refactor only with tests in place. |
| CP-20 | Surface assumptions | State assumptions and ask when something is unclear. Present alternatives rather than choosing silently. | Assumptions recorded in the PR description or ADR. Open questions raised before implementation, not after. |
| CP-21 | Deviations are explicit | When a principle or rule is broken, say so where the code is and record why. | Suppression comments carry the rule ID and justification. Deviation log maintained. |

> **Note:** CP-02, CP-16 and CP-20 matter most for AI agents, which tend to over-build, touch adjacent code and resolve ambiguity silently.

## Compliance

| Rule | Checked by |
|------|------------|
| CPR-01 | Review of [EG-013](eg-013-coding-standard.md) changes through the RFC process |
| CPR-03 | Static analysis suppression audit in CI |
| CPR-04 | Formatter, compiler flags and analyser gates in CI |

## Checklist

Tick an item when it is true for your project. Rule IDs point to the detail above.

- [ ] The coding standard derives from the principles and cites them (CPR-01)
- [ ] Review comments cite principle or rule IDs (CPR-02)
- [ ] Deviations are recorded in the code and in the deviation log (CPR-03)
- [ ] Principles that a tool can check are enforced in CI (CPR-04)
- [ ] Changes are the minimum needed and every changed line traces to the request (CP-02, CP-16)
- [ ] Wrong code is hard to write: distinct types, `const`, narrow interfaces (CP-04)
- [ ] Input is validated at boundaries and invariants are asserted (CP-05)
- [ ] There is no silent failure and every error path is defined (CP-06)
- [ ] Resource use is bounded and undefined behaviour is avoided (CP-07, CP-08)
- [ ] Warnings are treated as errors (CP-15)
- [ ] Assumptions are stated and questions raised before implementing (CP-20)

## Applying to personal projects and AI agents

### Personal projects

Starts at the **Starter** profile (see [personal-projects.md](personal-projects.md)). Use as is. It is language-neutral and costs nothing. Paste CP-02, CP-16 and CP-20 into every agent brief.

### AI agents

- Apply CP-02: write the minimum code, with no speculative features.
- Apply CP-16: change only what is needed and report unrelated problems instead of fixing them.
- Apply CP-20: state assumptions, ask when unclear and present alternatives.
- Handle every error path (CP-06), validate inputs at boundaries (CP-05) and keep warnings at zero (CP-15).
- Mark any deviation with the rule ID and a reason (CP-21).
