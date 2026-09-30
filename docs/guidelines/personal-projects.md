---
title: "Using the guidelines on personal projects"
status: draft
owner: "Project owner"
last-reviewed: 2026-09-29
---

## Purpose

The guidelines are written for a team, but the ideas scale down. This page says which guidelines to adopt for a personal project, what to simplify, and what never to drop, especially when AI agents do part of the work.

Working alone does not mean working without controls. When an agent writes code, you are also the reviewer, the test lead and the release manager, and the guidelines are the checks that keep those roles honest.

## Profiles

| Profile | Use it for | Adopt |
|---------|------------|-------|
| Starter | Scripts, experiments and weekend projects | The Starter guidelines in the table below |
| Standard | Any project you intend to maintain, or where agents work regularly | Starter plus the Standard guidelines |
| Full | Multi-person, deployed or regulated work | Everything, taking items as they apply |

## What to adopt and how to simplify

| ID | Guideline | Starts at | What to keep or simplify |
|----|-----------|-----------|--------------------------|
| [EG-001](eg-001-guidelines-governance.md) | Guidelines governance | Standard | Keep the files and IDs so rules can be cited. Skip owners, review-by cycles and RFCs, because you are the owner. Record which guidelines you adopted in ADR-0001. |
| [EG-002](eg-002-values-and-ways-of-working.md) | Engineering values and ways of working | Full | Keep written-by-default, small steps, simplicity and evidence over opinion. Decision rights collapse to you. Skip the cross-site rules. |
| [EG-003](eg-003-quality-policy-and-attributes.md) | Quality policy and quality attributes | Standard | Pick your top three quality attributes (for example correctness, simplicity, resource use) and write them in the README. Use the NFR scenario format only for requirements that matter. |
| [EG-004](eg-004-documentation-as-code.md) | Documentation as code and terminology | Starter | Start with a README and `AGENTS.md`. Add `docs/adr/` and Mermaid diagrams at the Standard profile. Front matter and a glossary become worthwhile once several people or agents share the same terms. |
| [EG-005](eg-005-ai-agent-usage.md) | AI agent usage | Starter | This is the guideline that matters most for solo work with agents. You are the human approver. Keep every rule. CODEOWNERS is just you. Use PRs (or at least branches with CI) so that you review diffs before they reach `main`. |
| [EG-006](eg-006-requirements-and-traceability.md) | Requirements and traceability | Standard | Keep a short `docs/requirements/` list with IDs and a one-line verification each, and reference IDs with `Refs:` in commits. Skip formal levels and three-way review. For a small script, a 'what it must do' list in the README is enough. |
| [EG-007](eg-007-architecture-principles.md) | Architecture principles | Standard | Adopt five or six principles that fit and write them in the README. Good defaults are AP-02, AP-03, AP-05, AP-07, AP-08 and AP-13. |
| [EG-008](eg-008-decision-records.md) | Decision records: RFCs and ADRs | Standard | Keep ADRs. They are your memory and your agents' memory. Replace RFCs with a short design note in `docs/rfc/` for large changes, with no comment period and you as sponsor. |
| [EG-009](eg-009-interfaces-and-co-design.md) | Interfaces and hardware and software co-design | Standard | Write down any boundary that another module, script, agent or device relies on (an API, a file format, a register map). Keep datasheet versions in `docs/reference/` or link them by version. |
| [EG-010](eg-010-components-reuse-and-variants.md) | Components, reuse and variants | Full | Only needed if you reuse your own code across projects. Publish it as a versioned package or tagged repository and pin it, instead of copying it between projects. Keep a short list of the components you maintain and their versions. |
| [EG-011](eg-011-technology-and-third-party.md) | Technology selection and third-party components | Standard | Keep pinning, checksums, a dependency list with licences, and automated update PRs. The radar can be a table in the README. |
| [EG-012](eg-012-coding-principles.md) | Coding principles | Starter | Use as is. It is language-neutral and costs nothing. Paste CP-02, CP-16 and CP-20 into every agent brief. |
| [EG-013](eg-013-coding-standard.md) | Coding standard | Standard | Choose a formatter and a linter per language, commit their configuration and fail CI on warnings. That is most of the value. Write topic entries only for topics you actually hit. |
| [EG-014](eg-014-version-control-and-versioning.md) | Version control, commits and versioning | Starter | Use Conventional Commits from day one, because they drive your version and changelog. Signed tags are recommended but optional. Use release branches only if you support old versions. |
| [EG-015](eg-015-pull-requests-and-review.md) | Pull requests and code review | Standard | Still use PRs, mainly for agent work and for reviewing your own diff. Self-review with the template checklist. Waive CODEOWNERS and turnaround rules, but keep 'CI must pass before merge' and 'small PRs'. |
| [EG-016](eg-016-pipelines-and-quality-gates.md) | Pipelines and quality gates | Standard | Use one workflow that runs the same `make` targets as your machine: format check, build, tests, lint and secret scan. Pin the toolchain with a container or lockfile. Skip rotations, service levels and HIL queueing. |
| [EG-017](eg-017-testing-principles-and-strategy.md) | Testing principles and strategy | Standard | Write unit tests on the host for logic, a regression test for every bug, and a smoke test for the whole thing. A coverage ratchet is cheap and effective. Skip rig management unless you own a rig. |
| [EG-018](eg-018-defects-and-technical-debt.md) | Defect and technical debt management | Standard | An issue list with `bug` and `tech-debt` labels is enough. Reproduce, add a regression test, and note the root cause for anything serious. Keep a short debt list and clear it regularly. |
| [EG-019](eg-019-logging-debug-and-diagnostics.md) | Logging, debug and fault diagnostics | Standard | Use one logging function with levels and module tags from the start, and no stray prints. Embed a build ID. For hardware projects, keep a one-page debug setup note. Skip binary log tokenisation unless flash is tight. |
| [EG-020](eg-020-observability-and-telemetry.md) | Observability and telemetry | Full | Needed only if the project runs somewhere you cannot see. Define three or four health questions, emit versioned metrics and set a few alerts that each have an action. Skip it for local tools. |
| [EG-021](eg-021-release-update-and-production.md) | Release, update and production | Standard | Tag, build once, generate the changelog from commits and publish. Keep a one-line release checklist and write down which versions you support. Skip staged rollout and production provisioning unless you ship devices. |
| [EG-022](eg-022-security-and-data-protection.md) | Security and data protection | Starter | Non-negotiable even solo: secret scanning, multi-factor authentication, dependency updates and a written list of what data may go to which AI tool. Do a one-page threat model only if the project is internet-facing or handles other people's data. |
| [EG-023](eg-023-safety-regulatory-and-certification.md) | Safety, regulatory and certification | Full | Adopt only if the project is subject to a regulation or safety standard (for example radio, mains-connected, medical, or sold as a product). Otherwise record 'not applicable' in ADR-0001. |
| [EG-024](eg-024-planning-delivery-and-improvement.md) | Planning, delivery and improvement | Full | A backlog, a short Definition of Done and a five-line risk list are enough. Hold a short retrospective after each release or milestone. Skip formal metrics unless they help you. |
| [EG-025](eg-025-research-and-prototyping.md) | Research, prototyping and experiments | Standard | This is where personal projects live. Keep a `prototypes/` folder, one experiment record per spike, and a firm stop, extend or graduate decision. Never copy prototype code into the product: re-implement it against the graduation checklist. |
| [EG-026](eg-026-competence-tooling-and-onboarding.md) | Competence, tooling and onboarding | Full | Treat the expected-depth table as your learning plan, especially git internals and the debug tools. Keep a short learning log and a `docs/how-to/` page for anything you had to relearn twice. A one-command environment setup is worth doing even solo, and it is what lets agents work reliably. |

## What to scale down

- **Roles collapse to you.** Owner, approver, release manager and security lead are all you. Keep the separation of activities: write, review, verify.
- **Approvals become self-review.** Review your own diff with the PR template checklist. Agent-authored changes are reviewed by you, line by line, with CI green, before merging.
- **RFCs become design notes.** Drop sponsors and comment periods. Write the note in `docs/rfc/` before a large change.
- **The conformance profile is your ADR-0001.** There is only one product, so record the profile you adopted and any tailoring there. All core rules still apply, and [core-rules.md](core-rules.md) lists them.
- **Registers and cycles are optional.** Ownership registers, review-by dates and competence matrices are worth having only when several people share the work.
- **Relax thresholds but keep ratchets.** PR size, coverage targets and patch times can be looser. Coverage must still not fall and warnings must stay at zero.
- **Heavy infrastructure only if you own it.** HIL queueing, on-call rotations, service levels and staged rollout apply only when you run that infrastructure.

## What never scales down

1. Everything is in version control, with Conventional Commits (VCS-03).
1. No secrets in the repository, logs or prompts, with scanning in CI (SEC-05).
1. CI runs the same commands you run locally, and no check is skipped to get a green build (PIP-01, PIP-08, TST-15).
1. Every behaviour you rely on has a test, and every bug gets a regression test (TST-07).
1. A human reviews agent output before it reaches `main` (AGT-03, AGT-04, AGT-07).
1. Agent boundaries and data classes for AI tools are written down and respected (AGT-05, AGT-08, SEC-10).
1. Dependencies are pinned and their licences known (TEC-04, TEC-05).
1. Significant decisions are recorded as ADRs, because agents and future you have no memory (ADR-03).
1. Documentation is updated in the same change as the behaviour (DOC-04).

## Bootstrap a new project

1. Create the repository. Copy `docs/guidelines/`, `docs/templates/`, `AGENTS.md` and `CLAUDE.md` into it.
1. Choose your profile. Set `status: active` on the guidelines you adopt, and delete or mark `deprecated` the rest.
1. Fill in `AGENTS.md`: a project summary and the commands for build, test, lint and everything CI runs.
1. Add one command (for example `make ci`) that runs the format check, build, tests, lint and secret scan, and point CI at it.
1. Install a commit-msg hook that enforces Conventional Commits, and a secret scanner as a pre-commit hook.
1. Protect `main` where your host supports it (required PRs and required checks). Where it does not, adopt the habit of never committing to `main` directly.
1. Copy `docs/templates/pull-request-template.md` to `.github/pull_request_template.md`, or your host's equivalent.
1. Write ADR-0001: the profile you adopted, the guidelines that do not apply (for example [EG-023](eg-023-safety-regulatory-and-certification.md)), and your top three quality attributes ([EG-003](eg-003-quality-policy-and-attributes.md)).
1. Add the first requirements to `docs/requirements/` and tag `v0.1.0`.

## Working with AI agents on personal projects

### Setup

- Keep `AGENTS.md` at the repository root. For Claude Code, `CLAUDE.md` contains `@AGENTS.md` so that both tools read the same instructions.
- Keep [agent-rules.md](agent-rules.md) in the repository and tell the agent to read it at the start of a task.
- Keep a short approved-tools list: which AI tools may see which data class ([EG-022](eg-022-security-and-data-protection.md), SEC-10).
- Point the agent at [principles.md](principles.md). When a rule is silent, the start-here principles decide.

### Each task

- Use the task brief template (`docs/templates/agent-task-brief.md`): goal, requirement IDs, scope, constraints and definition of done.
- Ask the agent for its assumptions and open questions first (CP-20). For anything larger than a small fix, ask for a short plan before code.
- Keep tasks small and single-purpose (AGT-10).
- Require the agent to run the check command and report the results (AGT-09).
- Review the diff yourself. Does every changed line trace to the request (CP-16)? Would the new tests fail if the code were wrong (AGT-11)?

### Between sessions

- Agents have no memory. Put context in the repository (ADRs, requirements, how-to pages, `AGENTS.md`) and not in chat.
- When an agent gets something wrong twice, add the missing rule or fact to `AGENTS.md` or the guidelines.
- Version the prompts and skills you reuse (AGT-12).

### Data

- Never paste secrets, keys or other people's personal data into a prompt (SEC-05, AGT-08).
- Classify what you share using the scheme in [EG-022](eg-022-security-and-data-protection.md), and only use tools you have approved for that class.
