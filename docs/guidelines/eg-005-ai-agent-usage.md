---
id: EG-005
title: "AI agent usage"
status: draft
owner: "Build and tooling lead and Security lead"
version: 0.1.0
part: "Foundations"
related: [EG-004, EG-011, EG-012, EG-015, EG-022]
review-by: 2027-09-30
supersedes:
---

- **Owner:** Build and tooling lead and Security lead
- **Applies to:** All use of AI coding agents and assistants on team repositories
- **Enforcement:** CI, branch protection, review
- **Related:** [EG-004](eg-004-documentation-as-code.md), [EG-011](eg-011-technology-and-third-party.md), [EG-012](eg-012-coding-principles.md), [EG-015](eg-015-pull-requests-and-review.md), [EG-022](eg-022-security-and-data-protection.md)
- **Principles:** AIP-01 to AIP-11 (see [principles.md](../business-principles/principles.md))

> **Note:** Rules marked *(core)* apply to every product and cannot be tailored. Other rules, and all numeric values, are proposed defaults that a product may tailor in its conformance profile ([EG-001](eg-001-guidelines-governance.md)).

## Purpose

Let agents raise productivity without lowering quality, security or traceability, by making standards machine-usable and enforcing them independently of the agent.

## Rules

1. **AGT-01** *(core)* Every repository MUST have an `AGENTS.md` at its root, reviewed and owned like code.
1. **AGT-02** `AGENTS.md` MUST state how to build, test, lint and format with exact commands, where the guidelines and ADRs are, the branching and commit conventions, and the agent boundaries (AGT-05).
1. **AGT-03** *(core)* Agent-authored changes MUST follow the same commit, PR, review and CI rules as human changes. There is no fast lane.
1. **AGT-04** *(core)* An agent MUST NOT approve or merge its own changes. At least one human reviewer who understands the change MUST approve.
1. **AGT-05** *(core)* Agents MUST NOT act in the areas listed in the boundaries table (below) without explicit human instruction in the task.
1. **AGT-06** *(core)* AI-assisted commits MUST carry a trailer, for example `Assisted-by: <tool>`, so that the extent of assistance is auditable.
1. **AGT-07** *(core)* Humans are accountable for all code they submit, whoever or whatever wrote it. The submitter MUST understand and be able to explain the change.
1. **AGT-08** *(core)* Data MUST NOT be sent to an agent service that is not approved for its classification ([EG-022](eg-022-security-and-data-protection.md)). The approved tools and their permitted data classes are held in one place, owned by the security lead.
1. **AGT-09** Agents SHOULD run the local checks and tests before proposing a change, and the PR SHOULD include the evidence.
1. **AGT-10** Agents SHOULD work on small, single-purpose changes. A large agent-generated diff MUST be split or accompanied by a written summary of intent and risk.
1. **AGT-11** Agent-generated tests SHOULD be reviewed for whether they verify requirements, not just whether they pass.
1. **AGT-12** Shared prompts, agent configuration and skills SHOULD be stored in the repository, versioned and reviewed.
1. **AGT-13** Licence and provenance concerns for generated code MUST be handled under [EG-011](eg-011-technology-and-third-party.md).
1. **AGT-14** `AGENTS.md` SHOULD link to the coding principles and name CP-02 (simplicity), CP-16 (surgical changes) and CP-20 (surface assumptions) explicitly.
1. **AGT-15** Agent-authored documentation MUST meet [EG-004](eg-004-documentation-as-code.md), and MUST be checked for accuracy by a human against the code or design it describes.

## Agent boundaries

| Boundary | Examples |
|----------|----------|
| Governance files | Guidelines, `AGENTS.md`, CODEOWNERS, pipeline definitions, branch protection |
| Secrets and signing | Keys, certificates, tokens, provisioning data |
| Generated and vendored code | Generated files, third-party SDKs, vendored sources |
| Security-relevant code | Bootloader, update, cryptography, authentication, debug-port control |
| Quality controls | Disabling or skipping tests, analysis or gates, or lowering thresholds |
| History | Rewriting shared history, force-pushing |
| Certified or regulated items | Code and data in certified baselines ([EG-023](eg-023-safety-regulatory-and-certification.md)) |

## Minimum `AGENTS.md` contents

```markdown
# AGENTS.md

## Project
One paragraph: what this repository is and its target hardware.

## Commands
- Build: `make build`
- Unit tests (host): `make test`
- Static analysis: `make analyse`
- Format and lint: `make lint`
- Docs: `make docs`

## Conventions
- Commits: Conventional Commits, scopes listed in docs/guidelines
- Branches: trunk-based, short-lived `feat/` and `fix/` branches
- Requirements: reference IDs in commit footers as `Refs: REQ-...`
- Decisions: see docs/adr/, write a new ADR for significant decisions
- Principles: simplicity (CP-02), surgical changes (CP-16), surface assumptions (CP-20)

## Boundaries
Do not modify: guidelines, pipeline definitions, CODEOWNERS, signing material,
vendor code, generated files. Ask a human first for anything security-relevant.

## Definition of done
Builds cleanly, tests pass, analysis clean, docs updated, PR template completed.
```

## Compliance

| Rule | Checked by |
|------|------------|
| AGT-01, AGT-02 | CI: `AGENTS.md` presence and required headings |
| AGT-03, AGT-04 | Branch protection: required human approvals for all authors |
| AGT-05 | CODEOWNERS on protected paths, review |
| AGT-06 | CI: commit trailer format check |
| AGT-08 | Approved tools register, security lead audit |

## Checklist

Tick an item when it is true for your project. Rule IDs point to the detail above.

- [ ] `AGENTS.md` exists at the repository root with commands, conventions, boundaries and definition of done (AGT-01, AGT-02)
- [ ] Agent changes follow the same commit, PR, review and CI rules as human changes (AGT-03)
- [ ] A human approves every agent-authored change, and agents never approve or merge their own work (AGT-04)
- [ ] Agent boundaries are protected by CODEOWNERS or branch protection (AGT-05)
- [ ] AI-assisted commits carry an `Assisted-by:` trailer (AGT-06)
- [ ] The submitter understands and can explain every line submitted (AGT-07)
- [ ] An approved-tools register lists each tool and the data classes it may receive (AGT-08)
- [ ] Agents run local checks first and the PR includes the evidence (AGT-09)
- [ ] Large agent diffs are split or accompanied by a summary of intent and risk (AGT-10)
- [ ] Agent-generated tests are reviewed for whether they verify requirements (AGT-11)
- [ ] Shared prompts, agent configuration and skills are versioned and reviewed (AGT-12)
- [ ] Licence and provenance of generated code is handled under the technology guideline (AGT-13)
- [ ] `AGENTS.md` names CP-02, CP-16 and CP-20 (AGT-14)
- [ ] Agent-written documentation is checked by a human against the code or design (AGT-15)

## Applying to personal projects and AI agents

### Personal projects

Starts at the **Starter** profile (see [personal-projects.md](personal-projects.md)). This is the guideline that matters most for solo work with agents. You are the human approver. Keep every rule. CODEOWNERS is just you. Use PRs (or at least branches with CI) so that you review diffs before they reach `main`.

### AI agents

- Read `AGENTS.md` first and follow it (AGT-01).
- You may not approve or merge your own work (AGT-04).
- Do not touch governance files, secrets or signing material, generated or vendored code, security-relevant code, quality controls, shared history or certified items unless the task says so (AGT-05).
- Add an `Assisted-by:` trailer to your commits (AGT-06).
- Run the build, tests and lint before proposing a change and include the results (AGT-09).
- Keep changes small and single-purpose, and summarise intent and risk for larger ones (AGT-10).
- Do not send data to a tool that is not approved for its classification (AGT-08).
