---
id: EG-022
title: "Security and data protection"
status: draft
owner: "Security lead"
version: 0.1.0
part: "Release, risk and compliance"
related: [EG-005, EG-011, EG-016, EG-019, EG-020, EG-021]
review-by: 2027-09-30
supersedes:
---

- **Owner:** Security lead
- **Applies to:** All products, tooling, pipelines, data and AI tool use
- **Enforcement:** CI, review, security testing, audits
- **Related:** [EG-005](eg-005-ai-agent-usage.md), [EG-011](eg-011-technology-and-third-party.md), [EG-016](eg-016-pipelines-and-quality-gates.md), [EG-019](eg-019-logging-debug-and-diagnostics.md), [EG-020](eg-020-observability-and-telemetry.md), [EG-021](eg-021-release-update-and-production.md)
- **Principles:** SP-01 to SP-12 (see [principles.md](principles.md))

> **Note:** Rules marked *(core)* apply to every product and cannot be tailored. Other rules, and all numeric values, are proposed defaults that a product may tailor in its conformance profile ([EG-001](eg-001-guidelines-governance.md)).

## Purpose

Build security and privacy into products and into the way we build them, from threat model to key handling to vulnerability response.

## Rules

1. **SEC-01** Each product MUST have security requirements and a threat model, created at design time and updated on every architecture-significant change, using an agreed method and stored in the repository.
1. **SEC-02** The security architecture MUST address trust boundaries, secure boot with a chain of trust, authenticated and encrypted communication, secure update, protected storage, debug port protection, least privilege and memory protection where the hardware allows.
1. **SEC-03** *(core)* Only approved cryptographic algorithms and vetted libraries MUST be used, from a list owned by the security lead. Home-grown cryptography MUST NOT be used.
1. **SEC-04** Key management MUST be documented, with a key hierarchy, protected signing (HSM or protected service), controlled provisioning, and rotation and revocation plans. Private keys MUST NOT be in repositories or pipeline logs.
1. **SEC-05** *(core)* Secrets MUST NOT be in source. Secret scanning MUST run pre-commit and in CI. A leaked secret is an incident and MUST be rotated.
1. **SEC-06** Secure coding rules (CP-17), security-focused review of security-relevant code and static analysis with security rule sets MUST be applied. Parsers and protocol handlers SHOULD be fuzzed.
1. **SEC-07** Security testing (fuzzing, penetration testing before major releases, security regression tests) MUST be performed and its findings tracked as defects.
1. **SEC-08** *(core)* Vulnerability management MUST have an intake channel, a coordinated disclosure policy, severity assessment and patch times by severity (below). The SBOM MUST be monitored against vulnerability feeds.
1. **SEC-09** Supply chain controls MUST include signed artefacts, provenance, pinned dependencies ([EG-011](eg-011-technology-and-third-party.md), [EG-016](eg-016-pipelines-and-quality-gates.md)), least-privilege pipeline credentials and a two-person rule for release signing.
1. **SEC-10** *(core)* A data classification scheme MUST be in place (below), with handling rules for storage, logs, telemetry, sharing and AI tools.
1. **SEC-11** Products and telemetry MUST follow privacy by design: data minimisation, purpose limitation, defined retention and an impact assessment where personal data is processed (OBS-05, LOG-08).
1. **SEC-12** Access to repositories, pipelines, rigs and signing MUST be least-privilege, use multi-factor authentication and be reviewed quarterly.
1. **SEC-13** Debug and manufacturing interfaces MUST be disabled or protected in production (DBG-02, REL-13).
1. **SEC-14** A security incident procedure MUST define roles, communication and post-incident review (PLN-11).

## Data classification

| Class | Description | Handling | AI tools permitted |
|-------|-------------|----------|--------------------|
| Public | Published material | No restriction | Any approved tool |
| Internal | General engineering material | Company systems only | Approved tools only |
| Confidential | Source code, designs, customer or commercial information | Access controlled, encrypted in transit and at rest | Only tools approved for confidential data |
| Restricted | Keys, credentials, personal data, export-controlled material | Minimum access, no copies, audit trail | None unless explicitly approved |

## Patch times by severity

Proposed starting points, to be confirmed through an RFC.

| Severity | Assessment | Fix or mitigation available within |
|----------|------------|-------------------------------------|
| Critical | Actively exploited or trivially exploitable | 14 days |
| High | Serious impact, reasonable exploitability | 30 days |
| Medium | Limited impact or difficult to exploit | 90 days |
| Low | Minimal impact | Next planned release |

## Compliance

| Rule | Checked by |
|------|------------|
| SEC-05 | CI and pre-commit secret scanning |
| SEC-06, SEC-07 | Analyser rule sets, fuzzing jobs, penetration test reports |
| SEC-08 | SBOM monitoring reports, vulnerability register |
| SEC-09, SEC-12 | Pipeline and access configuration audit |
| SEC-10 | Classification review of repositories, tools and telemetry |

## Checklist

Tick an item when it is true for your project. Rule IDs point to the detail above.

- [ ] Security requirements and a threat model exist and are updated on architecture change (SEC-01)
- [ ] The security architecture covers trust boundaries, secure boot, encrypted comms, secure update, protected storage and debug protection (SEC-02)
- [ ] Only approved cryptography and vetted libraries are used (SEC-03)
- [ ] Key hierarchy, protected signing, provisioning, rotation and revocation are documented (SEC-04)
- [ ] No secrets are in source, and scanning runs pre-commit and in CI (SEC-05)
- [ ] Secure coding rules and security-focused review apply, and parsers are fuzzed (SEC-06)
- [ ] Security testing is performed and findings are tracked (SEC-07)
- [ ] Vulnerability intake, disclosure policy, patch times and SBOM monitoring exist (SEC-08)
- [ ] Supply chain controls are in place (SEC-09)
- [ ] A data classification scheme has handling rules, including for AI tools (SEC-10)
- [ ] Privacy by design, retention and impact assessment are applied where needed (SEC-11)
- [ ] Access is least-privilege with multi-factor authentication and quarterly review (SEC-12)
- [ ] Debug and manufacturing interfaces are protected in production (SEC-13)
- [ ] A security incident procedure is defined (SEC-14)

## Applying to personal projects and AI agents

### Personal projects

Starts at the **Starter** profile (see [personal-projects.md](personal-projects.md)). Non-negotiable even solo: secret scanning, multi-factor authentication, dependency updates and a written list of what data may go to which AI tool. Do a one-page threat model only if the project is internet-facing or handles other people's data.

### AI agents

- Never write secrets, keys or tokens into code, config, logs, commits or prompts (SEC-05).
- If you find one, stop and report it.
- Never send Confidential or Restricted data to an unapproved tool (AGT-08, SEC-10).
- Do not use home-grown cryptography (SEC-03).
- Do not touch security-relevant code, authentication, key handling or debug protection without explicit instruction (AGT-05).
- Validate all input (CP-17).
