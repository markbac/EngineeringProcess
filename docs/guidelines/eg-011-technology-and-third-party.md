---
id: EG-011
title: "Technology selection and third-party components"
status: draft
owner: "Architecture group"
version: 0.1.0
part: "Requirements, architecture and design"
related: [EG-005, EG-016, EG-022, EG-010]
review-by: 2027-09-30
supersedes:
---

- **Owner:** Architecture group
- **Applies to:** All tools, platforms, libraries, vendor SDKs and open-source components
- **Enforcement:** RFC and ADR review, CI (manifest, licence and checksum checks)
- **Related:** [EG-005](eg-005-ai-agent-usage.md), [EG-016](eg-016-pipelines-and-quality-gates.md), [EG-022](eg-022-security-and-data-protection.md), [EG-010](eg-010-components-reuse-and-variants.md)

> **Note:** Rules marked *(core)* apply to every product and cannot be tailored. Other rules, and all numeric values, are proposed defaults that a product may tailor in its conformance profile ([EG-001](eg-001-guidelines-governance.md)).

## Purpose

Keep technology choices consistent, deliberate and reversible, and keep every third-party component known, licensed, pinned and maintained.

## Rules

1. **TEC-01** The team MUST maintain a technology radar in the repository, classifying languages, tools, libraries, platforms and RTOSes as `adopt`, `trial`, `assess` or `hold`. Changes are made through an RFC.
1. **TEC-02** Adopting a new dependency or tool MUST be supported by an evaluation recorded in an ADR, covering fit, maturity, licence, security posture, support and longevity, footprint and cost of exit.
1. **TEC-03** *(core)* A licence policy MUST list approved licences and prohibited ones. Any other licence needs legal review before use.
1. **TEC-04** *(core)* All third-party components MUST be recorded in a manifest (name, version, source, licence, checksum, owner). An SBOM MUST be generated for each release.
1. **TEC-05** *(core)* Versions MUST be pinned and checksums verified. Floating versions and unpinned downloads in builds MUST NOT be used.
1. **TEC-06** Vendor SDKs and libraries MUST be wrapped behind interfaces we own (AP-03). Patches to vendored code MUST be kept as a patch set with rationale and upstream status. Silent forks MUST NOT exist.
1. **TEC-07** Dependency updates SHOULD be proposed automatically (for example Renovate or Dependabot). Security updates follow the patch times in [EG-022](eg-022-security-and-data-protection.md), and other updates are reviewed at least quarterly.
1. **TEC-08** Each dependency MUST have an owner. Critical dependencies SHOULD have an exit strategy recorded in an ADR.
1. **TEC-09** AI-generated code MUST meet the same licence and provenance controls. Known third-party code MUST NOT be pasted in, and licence scanning SHOULD be used where tooling exists.
1. **TEC-10** Compiler, analyser and build tool versions MUST be pinned in the containerised toolchain ([EG-016](eg-016-pipelines-and-quality-gates.md)) and listed in the radar.
1. **TEC-11** End-of-life dates for dependencies and tools MUST be monitored, and replacement planned before support ends.

## Evaluation criteria

| Criterion | Questions |
|-----------|-----------|
| Fit | Does it meet the requirements and quality attributes? |
| Maturity | Is it proven on similar targets, and how active is the project? |
| Licence | Is the licence approved, and are the obligations manageable? |
| Security | Track record, disclosure process, patch speed |
| Support | Vendor or community support, expected lifetime |
| Footprint | Flash, RAM and CPU cost against budgets |
| Exit | How hard is it to replace, and is it behind our interface? |

## Compliance

| Rule | Checked by |
|------|------------|
| TEC-03, TEC-04 | CI: licence scan and manifest completeness check |
| TEC-05 | CI: checksum verification, ban on unpinned dependencies |
| TEC-06 | Review, dependency direction check |
| TEC-07 | Automated update tooling reports |

## Checklist

Tick an item when it is true for your project. Rule IDs point to the detail above.

- [ ] A technology radar exists with adopt, trial, assess and hold (TEC-01)
- [ ] New dependencies and tools have an evaluation recorded in an ADR (TEC-02)
- [ ] A licence policy lists approved and prohibited licences (TEC-03)
- [ ] A manifest of third-party components exists and an SBOM is produced per release (TEC-04)
- [ ] Versions are pinned and checksums verified (TEC-05)
- [ ] Vendor SDKs are wrapped behind our interfaces and patches are tracked (TEC-06)
- [ ] Dependency updates are proposed automatically, with security patch times (TEC-07)
- [ ] Each dependency has an owner, and critical ones have an exit strategy (TEC-08)
- [ ] AI-generated code is checked for licence and provenance (TEC-09)
- [ ] Toolchain versions are pinned in containers and listed in the radar (TEC-10)
- [ ] End-of-life dates are monitored (TEC-11)

## Applying to personal projects and AI agents

### Personal projects

Starts at the **Standard** profile (see [personal-projects.md](personal-projects.md)). Keep pinning, checksums, a dependency list with licences, and automated update PRs. The radar can be a table in the README.

### AI agents

- Do not add a dependency or tool without asking or drafting an ADR (TEC-02).
- Pin exact versions and update the manifest (TEC-04, TEC-05).
- Check licences against the approved list (TEC-03).
- Do not paste code of unknown provenance (TEC-09).
- Wrap vendor code behind an interface (TEC-06) and never edit vendored code directly.
