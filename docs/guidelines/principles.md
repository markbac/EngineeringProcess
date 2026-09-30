---
title: "Principles catalogue"
status: draft
owner: "Architecture group"
last-reviewed: 2026-09-29
---

## Purpose

Principles are the reasons behind the rules. Rules say what to do and can be checked. Principles say what to aim for, and decide the cases that no rule covers. When a rule is silent or unclear, apply the relevant principle, say which one you applied, and record any significant decision as an ADR.

This page gathers every principle set in one place. Each set is owned by the guideline named in its heading, and changes to a principle go through an RFC ([EG-008](eg-008-decision-records.md)).

## How to use principles

1. Start with the [start-here list](#start-here), which holds the principles that matter most day to day and for AI agents.
1. In reviews, cite a principle or rule ID so that feedback is explainable (CPR-02).
1. Where principles conflict, use the precedence order in [EG-007](eg-007-architecture-principles.md) (PRN-03). A product may tailor that order through its quality attribute profile, recorded in an ADR.
1. Where a principle can be checked by a tool, it should be (PRN-04).

> **Note:** Principles are not rules. They are not audited item by item, and they do not override a core rule. A core rule that seems wrong is changed through an RFC and not worked around.

## Start here

Fourteen principles to learn first. They cover most day-to-day judgement and are the ones an AI agent should apply when a rule is silent.

| ID | Principle | Statement |
|----|-----------|-----------|
| AP-02 | Layered, one-way dependencies | Hardware abstraction, platform services and application logic are separate layers, and dependencies point in one direction. |
| AP-05 | Simplicity | Choose the simplest design that meets the requirements. Complexity must earn its place. |
| AP-07 | Design for test | Logic is separable from hardware so that it runs on the host, and every component has seams for test doubles and HIL. |
| AP-13 | Prefer reversible decisions | Make cheap-to-reverse decisions quickly. Take irreversible ones deliberately, with evidence. |
| CP-02 | Simplicity, no speculation | Write the minimum code that solves the stated problem. |
| CP-06 | No silent failure | Errors are detected and either handled or propagated, never ignored. |
| CP-16 | Surgical changes | Change only what the task needs, and clean up only what your own change made redundant. |
| CP-20 | Surface assumptions | State assumptions and ask when something is unclear. Present alternatives rather than choosing silently. |
| TP-08 | Bugs start with a test | A defect is reproduced by a failing test before it is fixed. |
| SP-06 | Trust nothing at boundaries | Input from outside a trust boundary is untrusted and validated. |
| LP-01 | Build once, promote | The artefact that is tested is the artefact that is released. |
| AIP-01 | Humans stay accountable | The person who submits a change owns it and can explain it. |
| AIP-06 | Context lives in the repository | Agents have no memory between sessions, so context is kept in the repository. |
| WP-01 | Docs live with the code | Documentation is text in version control, next to what it describes. |

## Guiding principles for consistency (GP)

Set out in [EG-001](eg-001-guidelines-governance.md).

| ID | Principle | Statement |
|----|-----------|-----------|
| GP-01 | One way to do each thing | Where two approaches exist, the guideline picks one and records why. |
| GP-02 | If a tool can check it, a tool checks it | Reviewers spend attention on design, not formatting. |
| GP-03 | Conventions drive outcomes | A convention that does not feed an automated result (version, changelog, trace report, release) is etiquette and will decay. Prefer conventions that machines can read. |
| GP-04 | Everything is text in version control | Requirements, decisions, diagrams, pipelines, repository settings and guidelines are reviewed, versioned and diffable. |
| GP-05 | Record decisions once, at the right level | Context in an RFC, outcome in an ADR, rules in a guideline, enforcement in tooling. |
| GP-06 | Local equals CI | Any check that runs in the pipeline runs identically on a developer machine with one command. |
| GP-07 | Guidelines are short and owned | A few pages each, one named owner, a review date, and a stated way of checking compliance. |
| GP-08 | Understand the tool | Using a tool without knowing how it works (git, the linker, the RTOS, the debug probe) is a risk. Each guideline names the competence expected. |
| GP-09 | Explain the why | Rules carry a rationale where it is not obvious, so that people and agents can apply them sensibly at the edges. |
| GP-10 | Sequence adoption | Start with what other practices depend on: commit conventions, a single version source and a reproducible pipeline. |

## Engineering values (EV)

Set out in [EG-002](eg-002-values-and-ways-of-working.md).

| ID | Principle | Statement |
|----|-----------|-----------|
| EV-01 | Ownership | Every asset has a named owner accountable for its quality and future |
| EV-02 | Quality built in | Quality is produced by the way we work, not inspected in at the end |
| EV-03 | Written and open by default | Decisions, agreements and handovers are recorded where others can find them |
| EV-04 | Evidence over opinion | Claims about performance, defects and risk are backed by data |
| EV-05 | Blameless learning | We fix systems and processes, not people |
| EV-06 | Small steps | Small, frequent, reversible changes beat large, rare ones |
| EV-07 | Simplicity | The simplest solution that meets the need is preferred |
| EV-08 | Respect for others' time | Cross-site work is designed for time zones, and requests are clear and complete |

## Requirements and decision principles (RP)

Set out in [EG-006](eg-006-requirements-and-traceability.md) and [EG-008](eg-008-decision-records.md).

| ID | Principle | Statement | Typical implications |
|----|-----------|-----------|----------------------|
| RP-01 | Needs before solutions | Requirements say what is needed and why, not how it is built. | Solution-neutral wording, with the design recorded separately. |
| RP-02 | One requirement, one statement | Each requirement is atomic and unambiguous. | No compound requirements, and no words such as 'and/or' or 'appropriate'. |
| RP-03 | Verifiable or not a requirement | If a requirement cannot be verified, it is rewritten or removed. | Every requirement names a verification method. |
| RP-04 | Traceable both ways | Every requirement traces up to a need and down to design, code and test. | The pipeline generates the trace report and gaps are visible. |
| RP-05 | Measurable quality | Quality attributes are stated as measurable scenarios. | Environment, stimulus, response and measure, from the NFR catalogue. |
| RP-06 | Stable identity | Identifiers are permanent and never reused. | Retired requirements stay in the record. |
| RP-07 | Manage change, do not avoid it | Change is expected, assessed for impact and recorded. | A change impact check flags dependent tests and documents. |
| RP-08 | Decide with evidence and record why | Decisions weigh real options with evidence and are written down. | ADRs with options, consequences and verification. |

## Architecture principles (AP)

Set out in [EG-007](eg-007-architecture-principles.md).

| ID | Principle | Statement | Typical implications |
|----|-----------|-----------|----------------------|
| AP-01 | Requirements first | Architecture exists to satisfy requirements and quality attributes, and is traceable to them. | Every component and interface traces to a requirement. Quality attributes are stated measurably. |
| AP-02 | Layered, one-way dependencies | Hardware abstraction, platform services and application logic are separate layers, and dependencies point in one direction. | No application code touches registers directly. Dependency direction is checked in CI. |
| AP-03 | Isolate what changes | Volatile things (silicon, vendor SDKs, protocols, cloud endpoints) sit behind stable interfaces that we own. | Vendor code is wrapped by adapters and can be swapped for tests or new hardware. |
| AP-04 | Interfaces are contracts | Every interface is explicit, owned, versioned and tested for compatibility. | Definitions in machine-readable form where possible. Breaking changes follow semantic versioning. |
| AP-05 | Simplicity | Choose the simplest design that meets the requirements. Complexity must earn its place. | Fewer components, fewer modes, fewer configuration options. |
| AP-06 | Budgets are architecture | Flash, RAM, CPU, power, latency and bandwidth are allocated to components and tracked from the start. | Budget table in the architecture document. Size and timing are tracked in CI and a regression fails the gate. |
| AP-07 | Design for test | Logic is separable from hardware so that it runs on the host, and every component has seams for test doubles and HIL. | Hardware access behind interfaces, dependency injection, no hidden global state. |
| AP-08 | Design for diagnosis | The system explains its own state and failures. | Logging, fault codes, crash capture and telemetry are architectural components ([EG-019](eg-019-logging-debug-and-diagnostics.md), [EG-020](eg-020-observability-and-telemetry.md)). |
| AP-09 | Secure by design | Security is a design property: least privilege, defence in depth, secure defaults, minimal attack surface. | Trust boundaries, threat model and key handling are designed before implementation. |
| AP-10 | Fail safe and recover | Every fault has defined behaviour, and there is a route back to a known good state. | Watchdog, fault containment, power-fail handling, rollback on a failed update. |
| AP-11 | Design for the whole lifecycle | Field update, compatibility over time, manufacture, service and end of life are designed in from the outset. | Update mechanism, version compatibility rules, provisioning flow, decommissioning. |
| AP-12 | Deterministic where it matters | Timing-critical behaviour is predictable and bounded. | Bounded resource use, no dynamic allocation in critical paths, analysable scheduling. |
| AP-13 | Prefer reversible decisions | Make cheap-to-reverse decisions quickly. Take irreversible ones deliberately, with evidence. | Flash layout, crypto scheme and wire formats need an RFC and an ADR. |
| AP-14 | Reuse before build, with control | Reuse proven components and buy where sensible, but own the boundary. | Third-party choices go through [EG-011](eg-011-technology-and-third-party.md) and sit behind interfaces (AP-03). |
| AP-15 | Check architecture continuously | Architectural intent is enforced by automated checks as well as review. | Dependency rules, budget checks and interface compatibility tests run in the pipeline. |
| AP-16 | Structure follows ownership | Component boundaries match ownership, so that responsibilities are clear across sites. | Each component has an owner. Cross-site interfaces are contracts (AP-04). |
| AP-17 | Record the why | Decisions and their reasoning are kept where the code lives. | ADRs ([EG-008](eg-008-decision-records.md)) and architecture documents in the repository ([EG-004](eg-004-documentation-as-code.md)). |

## Coding principles (CP)

Set out in [EG-012](eg-012-coding-principles.md).

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

## Testing principles (TP)

Set out in [EG-017](eg-017-testing-principles-and-strategy.md).

| ID | Principle | Statement | Typical implications |
|----|-----------|-----------|----------------------|
| TP-01 | Cheapest level first | Test at the cheapest level that can catch the defect. Most tests run on the host. | Most tests run on the host, and hardware tests only where hardware is needed. |
| TP-02 | Trace to requirements | Every test verifies a requirement, and every requirement has verification. | Test names carry requirement IDs and the trace report shows gaps. |
| TP-03 | Deterministic and independent | Tests give the same result every run, in any order. | No dependence on time, order or shared state, and flaky tests are quarantined. |
| TP-04 | Behaviour over implementation | Tests check what the unit promises, not how it does it. | Assert on outputs and observable effects, not on internal calls. |
| TP-05 | Fail clearly | A failing test says what went wrong and where. | Assertion messages and logs show expected against actual. |
| TP-06 | Automate what repeats | Anything run more than twice is automated. | Regression, HIL and soak runs are scheduled in the pipeline. |
| TP-07 | Tests are code | Tests are reviewed, refactored and maintained to the same standard. | Test code follows the coding standard and is refactored. |
| TP-08 | Bugs start with a test | A defect is reproduced by a failing test before it is fixed. | A failing test comes first, then the fix, and the test stays. |
| TP-09 | Test what can go wrong | Negative, boundary and fault-injection cases are as important as the happy path. | Fault injection, boundary values and malformed input are included. |
| TP-10 | Hardware for what only hardware shows | Timing, power, peripherals and environment need real hardware. | Timing, power and peripheral behaviour are verified on rigs. |
| TP-11 | Controlled environments | The environment for every test run is known and recorded. | Toolchain, firmware version and rig configuration are recorded with every result. |

## Security principles (SP)

Set out in [EG-022](eg-022-security-and-data-protection.md).

| ID | Principle | Statement | Typical implications |
|----|-----------|-----------|----------------------|
| SP-01 | Secure by design | Security is designed in before implementation, not added afterwards. | Threat model at design time, with security requirements traced. |
| SP-02 | Least privilege | Every component, person, process and credential has only the access it needs. | Memory protection, scoped tokens, role-based access. |
| SP-03 | Defence in depth | No single control is relied on, and any one layer may fail. | Layered checks, isolation, secure boot together with signed updates. |
| SP-04 | Minimise attack surface | Fewer interfaces, features and privileges mean fewer weaknesses. | Unused interfaces removed, debug ports locked in production. |
| SP-05 | Secure defaults | The default configuration is the safe one. | Risky features off by default, and no default credentials. |
| SP-06 | Trust nothing at boundaries | Input from outside a trust boundary is untrusted and validated. | Parsers validated and fuzzed, and lengths and ranges checked. |
| SP-07 | Protect secrets and keys | Secrets never appear in source, logs or prompts, and keys have a managed lifecycle. | Vault or HSM, rotation and revocation, secret scanning. |
| SP-08 | Use proven cryptography | Never invent cryptography. Use vetted algorithms and libraries. | Approved list, and crypto agility considered. |
| SP-09 | Fail securely | On failure the system stays safe and does not leak or open up. | Deny by default, and a safe state on fault. |
| SP-10 | Assume compromise | Design so that breaches are detected, contained and recoverable. | Audit events, revocation, recovery and the ability to update. |
| SP-11 | Security is continuous | Vulnerabilities are found, tracked and fixed for the whole life of the product. | SBOM monitoring and patch times. |
| SP-12 | Minimise and classify data | Collect and keep only what is needed, and handle it by its classification. | Classification scheme and retention limits. |

## Diagnostics and operations principles (OP)

Set out in [EG-019](eg-019-logging-debug-and-diagnostics.md) and [EG-020](eg-020-observability-and-telemetry.md).

| ID | Principle | Statement | Typical implications |
|----|-----------|-----------|----------------------|
| OP-01 | The system explains itself | Logs, fault codes and crash capture are built in from the start. | A common logging facility, a fault registry and crash dumps. |
| OP-02 | Measure before you optimise | Decisions about performance and reliability use data, not intuition. | Budgets, traces and telemetry. |
| OP-03 | Diagnostics are budgeted | The cost of diagnostics in memory, power and bandwidth is planned. | Log and telemetry budgets, rate limiting. |
| OP-04 | Fail visibly and recover | Faults are detected, recorded and recovered from, never silent. | Defined fault behaviour, watchdog, reset reason captured. |
| OP-05 | Every alert has an action | An alert has an owner, a runbook and a required action. | No alert without a response. |
| OP-06 | Same signals in lab and field | Lab and field emit the same diagnostics and telemetry. | Parsers and dashboards are exercised before release. |
| OP-07 | Reproducible from evidence | A field failure can be turned into a local reproduction and then a test. | Build IDs, symbols retained, a documented procedure. |
| OP-08 | Private by default | Logs and telemetry hold no secrets and no personal data unless approved. | Classification applied to every field. |
| OP-09 | Production is not debug | Debug and production builds differ, and production interfaces are locked. | Separate build configurations and release checks. |
| OP-10 | Field data feeds engineering | What we learn in the field changes requirements, tests and priorities. | A regular field review that feeds triage. |

## Lifecycle and release principles (LP)

Set out in [EG-014](eg-014-version-control-and-versioning.md), [EG-016](eg-016-pipelines-and-quality-gates.md) and [EG-021](eg-021-release-update-and-production.md).

| ID | Principle | Statement | Typical implications |
|----|-----------|-----------|----------------------|
| LP-01 | Build once, promote | The artefact that is tested is the artefact that is released. | Immutable artefacts with metadata, and no rebuild for release. |
| LP-02 | Reproducible builds | The same commit and toolchain give the same result anywhere. | Pinned containerised toolchains. |
| LP-03 | Everything shipped is traceable | Any device can be traced to its version, hardware, components and evidence. | Version from tags, bill of materials, evidence pack. |
| LP-04 | Small, frequent, reversible releases | Smaller releases carry less risk and are easier to reverse. | Short-lived branches and staged rollout. |
| LP-05 | Updates are safe by design | An update is authenticated, atomic and recoverable. | A/B images, power-fail safety, rollback. |
| LP-06 | Roll out in stages and watch | Release to a few first and let real data decide. | Health gates and a halt switch. |
| LP-07 | Support what you ship | Every shipped version has a stated support period and end of life. | Supported version list and security update duration. |
| LP-08 | Evidence is a by-product | Proof of quality and compliance is produced by the process, not assembled afterwards. | Pipeline-generated evidence pack. |
| LP-09 | Compatibility is a promise | Versions state what they are compatible with, and that is tested. | Semantic versioning and a compatibility matrix. |
| LP-10 | Manufacturing is part of design | Provisioning, production test and yield are designed in. | Design for test and controlled key injection. |

## Documentation principles (WP)

Set out in [EG-004](eg-004-documentation-as-code.md).

| ID | Principle | Statement | Typical implications |
|----|-----------|-----------|----------------------|
| WP-01 | Docs live with the code | Documentation is text in version control, next to what it describes. | Same repository, same PR, same review. |
| WP-02 | One source of truth | Define a fact once, link to it elsewhere, and generate what can be generated. | Generated references, and no hand-kept copies. |
| WP-03 | Audience and purpose first | State who a document is for and what question it answers. | Tutorial, how-to, reference and explanation kept apart. |
| WP-04 | Short, plain, precise | Write plainly, with the conclusion first and terms defined. | Short sentences, active voice, British English. |
| WP-05 | Diagrams are text | Diagrams are source that can be reviewed and diffed. | Mermaid or PlantUML. |
| WP-06 | Reviewed like code | Documents are linted, link-checked and reviewed. | Docs build in CI. |
| WP-07 | Explain why | Record the reasoning as well as the result. | ADRs and rationale fields. |
| WP-08 | Readable by people and agents | Structure, IDs and front matter make documents navigable by both. | Consistent headings and stable identifiers. |
| WP-09 | Keep it or delete it | A stale document is worse than none, so every document has an owner and a review date. | Front matter with owner and review date. |
| WP-10 | One vocabulary | Terms are defined once and used consistently. | A single glossary. |

## AI agent principles (AIP)

Set out in [EG-005](eg-005-ai-agent-usage.md).

| ID | Principle | Statement | Typical implications |
|----|-----------|-----------|----------------------|
| AIP-01 | Humans stay accountable | The person who submits a change owns it and can explain it. | No merge without a human who understands the change. |
| AIP-02 | Agents are untrusted contributors | Review agent output as you would any new contributor's, and more carefully where it is opaque. | Same PR, review and CI rules. |
| AIP-03 | Controls do not depend on the agent | Enforcement lives in tooling, not in prompts. | Hooks, gates, branch protection and CODEOWNERS. |
| AIP-04 | Explicit beats implicit | Agents have no tribal knowledge, so rules, commands and boundaries are written down. | AGENTS.md and numbered rules. |
| AIP-05 | Small, scoped tasks | One purpose per task, and small diffs. | Task briefs with a definition of done. |
| AIP-06 | Context lives in the repository | Agents have no memory between sessions, so context is kept in the repository. | ADRs, requirements, how-to pages and AGENTS.md. |
| AIP-07 | Evidence over assertion | Agents show test and analysis output and do not just claim success. | Results included in the PR. |
| AIP-08 | Surface assumptions | Agents state assumptions and ask when unclear. | See CP-20. |
| AIP-09 | Least authority, least data | Give agents only the permissions and data the task needs. | Data classes per tool and scoped credentials. |
| AIP-10 | Provenance is recorded | AI assistance and its licence implications are traceable. | Commit trailers and provenance checks. |
| AIP-11 | Learn from corrections | A mistake made twice becomes a written rule. | Update AGENTS.md or the guideline. |
