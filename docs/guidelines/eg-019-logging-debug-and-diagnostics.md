---
id: EG-019
title: "Logging, debug and fault diagnostics"
status: draft
owner: "Firmware lead"
version: 0.1.0
part: "Diagnostics and field insight"
related: [EG-007, EG-012, EG-020, EG-022]
review-by: 2027-09-30
supersedes:
---

- **Owner:** Firmware lead
- **Applies to:** All firmware, debug tooling and production builds
- **Enforcement:** Build configuration, CI, review
- **Related:** [EG-007](eg-007-architecture-principles.md), [EG-012](eg-012-coding-principles.md), [EG-020](eg-020-observability-and-telemetry.md), [EG-022](eg-022-security-and-data-protection.md)
- **Principles:** OP-01 to OP-10 (see [principles.md](principles.md))

> **Note:** Rules marked *(core)* apply to every product and cannot be tailored. Other rules, and all numeric values, are proposed defaults that a product may tailor in its conformance profile ([EG-001](eg-001-guidelines-governance.md)).

## Purpose

Make the device explain its own behaviour and failures, cheaply and safely, during development and in the field, with a single framework for logging, debugging, fault handling and crash capture.

## Logging rules

1. **LOG-01** Logging purposes MUST be kept separate, each with its own level and retention policy: development trace, field diagnostics and security or audit events.
1. **LOG-02** Log levels MUST follow the definitions below. The compiled or default level for production MUST be defined, and `DEBUG` and `TRACE` MUST be compiled out or disabled in production.
1. **LOG-03** All logging MUST use one common logging facility. Ad-hoc `printf` MUST NOT be used. Every record has a module ID and severity, with compile-time filtering per module.
1. **LOG-04** The record format MUST be compact, structured and machine-parseable. Where flash is constrained, records SHOULD be tokenised or binary with an off-target decoder. Each record has a timestamp (source and unit defined), module, level, event ID and parameters.
1. **LOG-05** A single, versioned event and fault code registry MUST exist with an owner. Each code has a description, severity, likely cause and recommended action. The registry is the source of truth from which code and documentation are generated.
1. **LOG-06** Logging cost MUST be budgeted (flash, RAM, CPU). Logging MUST be non-blocking and safe in the contexts it is used in, rate-limited and de-duplicated. Logging from time-critical interrupts MUST be deferred.
1. **LOG-07** Persistent logs MUST use a wear-aware policy, with documented write limits. RAM ring buffers hold recent history.
1. **LOG-08** Logs MUST NOT contain secrets, keys or personal data, and MUST follow the data classification ([EG-022](eg-022-security-and-data-protection.md)).
1. **LOG-09** Messages MUST state what happened and give useful context. Logging inside tight loops MUST be avoided.
1. **LOG-10** Log decoding tools MUST be versioned with the firmware and retained (DBG-07).

## Debug and fault rules

1. **DBG-01** A standard debug setup per platform MUST be documented and kept in the repository: approved probes and adapters, debug server, IDE configuration and trace tools, starting with one command.
1. **DBG-02** Debug builds and production builds MUST be defined, with their differences documented. Production images MUST have debug interfaces disabled or protected ([EG-022](eg-022-security-and-data-protection.md)). Debug builds MUST NOT be released.
1. **DBG-03** Every fault path (hard fault, assertion, watchdog, stack overflow, brownout, memory error) MUST have defined behaviour: capture state, log, enter a safe state and reset if appropriate. The policy is recorded in an ADR.
1. **DBG-04** Assertions MUST be used for invariants (CP-05). Their production behaviour MUST be defined (for example log and reset), and they MUST NOT have side effects.
1. **DBG-05** The reset reason and last-known state MUST be captured at every boot and reported.
1. **DBG-06** A crash dump MUST have a defined format (registers, stack excerpt, fault status registers, version and build ID, key state), stored in reserved memory with a defined retrieval procedure and size budget.
1. **DBG-07** A build ID MUST be embedded in every image. Map files, ELF files and symbols MUST be archived per release for the supported life so that dumps can be decoded.
1. **DBG-08** Runtime diagnostics SHOULD include health counters (stack high-water marks, heap use, queue depths, CPU load), self-tests and a diagnostic command interface with access control.
1. **DBG-09** Watchdog design MUST be reviewed as a system property: window, feeding rules and reset handling. Watchdogs MUST NOT be fed blindly from timer interrupts.
1. **DBG-10** A documented procedure MUST exist to turn a field dump or log into a local reproduction, and the reproduction MUST become a test (TP-08).
1. **DBG-11** Trace and timing tools for analysis MUST be approved, and the cost of instrumentation documented.

## Log levels

| Level | Meaning | Production |
|-------|---------|------------|
| ERROR | An operation failed and the system could not recover it locally | Enabled |
| WARN | Unexpected condition handled, but worth attention | Enabled |
| INFO | Significant normal event (boot, update, state change) | Enabled at defined volume |
| DEBUG | Detail for development | Compiled out or disabled |
| TRACE | Fine-grained flow for development | Compiled out |

## Compliance

| Rule | Checked by |
|------|------------|
| LOG-02, LOG-03 | CI: build configuration check and lint for banned `printf` use |
| LOG-05 | CI: registry schema and uniqueness check, generation check |
| LOG-06 | CI: size and timing budget report |
| DBG-02 | Release criteria and production image verification ([EG-021](eg-021-release-update-and-production.md)) |
| DBG-07 | Release evidence pack completeness check |

## Checklist

Tick an item when it is true for your project. Rule IDs point to the detail above.

- [ ] Logging purposes are separated, each with its own levels and retention (LOG-01)
- [ ] Log levels are defined and DEBUG and TRACE are off in production (LOG-02)
- [ ] There is one logging facility, no ad-hoc printf, and every record has a module ID and severity (LOG-03)
- [ ] The format is compact, structured and machine-parseable, with an off-target decoder if needed (LOG-04)
- [ ] A versioned event and fault code registry has an owner (LOG-05)
- [ ] Logging cost is budgeted, non-blocking and rate-limited (LOG-06)
- [ ] Persistent logs are wear-aware (LOG-07)
- [ ] Logs contain no secrets or personal data (LOG-08)
- [ ] Messages say what happened with context, and there is no logging in tight loops (LOG-09)
- [ ] Log decoding tools are versioned with the firmware (LOG-10)
- [ ] A standard debug setup is documented per platform and starts with one command (DBG-01)
- [ ] Debug and production builds are defined, debug builds are never released, and production interfaces are locked (DBG-02)
- [ ] Every fault path has defined behaviour, recorded in an ADR (DBG-03)
- [ ] Assertions guard invariants, have defined production behaviour and no side effects (DBG-04)
- [ ] The reset reason is captured at every boot (DBG-05)
- [ ] The crash dump format is defined, a build ID is embedded and symbols are archived per release (DBG-06, DBG-07)
- [ ] Runtime diagnostics exist and the watchdog design is reviewed (DBG-08, DBG-09)
- [ ] A procedure turns a field dump into a local reproduction, which becomes a test (DBG-10)
- [ ] Trace and timing tools are approved and the cost of instrumentation is documented (DBG-11)

## Applying to personal projects and AI agents

### Personal projects

Starts at the **Standard** profile (see [personal-projects.md](personal-projects.md)). Use one logging function with levels and module tags from the start, and no stray prints. Embed a build ID. For hardware projects, keep a one-page debug setup note. Skip binary log tokenisation unless flash is tight.

### AI agents

- Use the project's logging facility with the correct level and module, and never `printf` or ad-hoc prints (LOG-03).
- Never log secrets, keys or personal data (LOG-08).
- Handle every fault path explicitly (DBG-03).
- Do not put side effects in assertions (DBG-04).
- Add event and fault codes to the registry and never invent them inline (LOG-05).
