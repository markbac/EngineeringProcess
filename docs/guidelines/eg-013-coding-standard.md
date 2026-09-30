---
id: EG-013
title: "Coding standard"
status: draft
owner: "Firmware lead"
version: 0.1.0
part: "Code and build"
related: [EG-012, EG-016, EG-019, EG-026]
review-by: 2027-09-30
supersedes:
---

- **Owner:** Firmware lead
- **Applies to:** All languages used in product and tooling code
- **Enforcement:** Formatter, compiler, static analysis, review
- **Related:** [EG-012](eg-012-coding-principles.md), [EG-016](eg-016-pipelines-and-quality-gates.md), [EG-019](eg-019-logging-debug-and-diagnostics.md), [EG-026](eg-026-competence-tooling-and-onboarding.md)

> **Note:** Rules marked *(core)* apply to every product and cannot be tailored. Other rules, and all numeric values, are proposed defaults that a product may tailor in its conformance profile ([EG-001](eg-001-guidelines-governance.md)).

## Purpose

Require a coding standard to exist for every language in use, and define what it must contain. This guideline does not contain the coding rules themselves. It says what the coding standard must decide, how it is enforced and how it evolves.

## Rules

1. **COD-01** *(core)* The team MUST maintain one coding standard per language in use (for example C, C++, Python, shell, build scripts). Each MUST derive from the coding principles ([EG-012](eg-012-coding-principles.md)), and each rule MUST have an ID and cite the principle it serves.
1. **COD-02** Each standard MUST specify the language version, the permitted subset or rule set (for example MISRA C or a C++ subset), and the compiler and version.
1. **COD-03** Each standard MUST cover the topics in the table below, or state explicitly why a topic does not apply.
1. **COD-04** *(core)* Formatting MUST be applied by a formatter, not by hand. Its configuration lives in the repository, and CI checks it.
1. **COD-05** *(core)* Static analysis tools, rule sets and severities MUST be configured in the repository and pinned. Warnings MUST be errors. Suppressions MUST be inline, carry the rule ID and a justification, and be audited.
1. **COD-06** Rules MUST be classified as `mandatory`, `required` or `advisory`. Deviations follow GOV-09 and are recorded in a deviation log.
1. **COD-07** Each rule MUST give its rationale, a compliant and a non-compliant example, and identify the tool that checks it or state that it is checked in review.
1. **COD-08** Compiler flags MUST be standardised: a baseline warning set, hardening options, sanitisers for host builds, and documented effects of optimisation and link-time optimisation on debuggability. Flags are identical locally and in CI.
1. **COD-09** Standards MUST apply to new and changed code. Legacy code MUST be tracked against a baseline that is reduced over time. Unrelated legacy code MUST NOT be reformatted in feature PRs (CP-16).
1. **COD-10** Standards MUST be reviewed at least annually and changed through an RFC. Each change MUST include a migration approach.
1. **COD-11** Standards MUST be short enough to use. A one-page quick reference and a review checklist SHOULD be generated from them, and an agent-oriented condensed rule list SHOULD be kept in the repository ([EG-005](eg-005-ai-agent-usage.md)).
1. **COD-12** Tooling code and scripts MUST have a proportionate standard. Lack of a standard for scripts is not an exemption.

## What a coding standard must decide

| Topic | The standard must decide |
|-------|--------------------------|
| Naming | Conventions for files, types, functions, variables, constants, macros, and module prefixes |
| Layout | Formatting configuration, line length, file organisation |
| Structure | Module and header structure, include rules, dependency direction |
| Types | Fixed-width integers, enumerations, booleans, signed and unsigned arithmetic, casts |
| Constants and macros | When macros are allowed, constant definitions, magic numbers |
| Error handling | Return conventions, error code scheme, propagation, failure behaviour |
| Assertions | Where required, production behaviour, side-effect ban ([EG-019](eg-019-logging-debug-and-diagnostics.md)) |
| Memory | Allocation policy, stack limits, alignment, buffer handling, initialisation |
| Pointers | Permitted uses, ownership, null handling, pointer arithmetic |
| Concurrency | Rules for ISRs, shared data, locking, RTOS primitives, priorities |
| Hardware access | Register access, `volatile`, memory barriers, DMA and cache handling |
| Portability | Compiler extensions, endianness, target-specific code isolation |
| Undefined behaviour | Specific hazards to avoid and how they are detected |
| Comments | What to comment, format, requirement and ADR references |
| Banned constructs | Unsafe functions and language features, with alternatives |
| Testing hooks | Seams for test doubles, test-only code rules |
| Security | Secret handling, constant-time operations, input validation |

## Compliance

| Rule | Checked by |
|------|------------|
| COD-04 | CI: formatter check |
| COD-05, COD-06 | CI: analyser with warnings as errors, suppression audit report |
| COD-08 | Build configuration shared by local and CI builds |
| COD-09 | Baseline tracking report |
| COD-10 | Review-by date and RFC history |

## Checklist

Tick an item when it is true for your project. Rule IDs point to the detail above.

- [ ] There is one coding standard per language in use, with rule IDs that cite principles (COD-01)
- [ ] Language version, subset and compiler are specified (COD-02)
- [ ] The standard covers every required topic or says why not (COD-03)
- [ ] The formatter is configured in the repository and checked in CI (COD-04)
- [ ] Static analysis is configured and pinned, warnings are errors, and suppressions are justified and audited (COD-05)
- [ ] Rules are classified mandatory, required or advisory, with a deviation log (COD-06)
- [ ] Each rule has a rationale, examples and a checking tool (COD-07)
- [ ] Compiler flags are standardised and identical locally and in CI (COD-08)
- [ ] A legacy baseline is tracked and there is no drive-by reformatting (COD-09)
- [ ] The standard is reviewed annually through RFC (COD-10)
- [ ] A quick reference, review checklist and agent rule list exist (COD-11)
- [ ] Scripts and tooling code also have a proportionate standard (COD-12)

## Applying to personal projects and AI agents

### Personal projects

Starts at the **Standard** profile (see [personal-projects.md](personal-projects.md)). Choose a formatter and a linter per language, commit their configuration and fail CI on warnings. That is most of the value. Write topic entries only for topics you actually hit.

### AI agents

- Run the formatter and linter before every commit and do not hand-format (COD-04).
- Do not add suppressions without a rule ID and justification (COD-05).
- Use the flags in the build configuration unchanged (COD-08).
- Do not reformat unrelated code (COD-09).
- Follow the condensed rule list in the repository (COD-11).
