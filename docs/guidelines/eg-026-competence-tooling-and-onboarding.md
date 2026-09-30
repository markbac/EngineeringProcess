---
id: EG-026
title: "Competence, tooling and onboarding"
status: draft
owner: "Engineering manager"
version: 0.1.0
part: "Delivery, research and people"
related: [EG-002, EG-005, EG-011, EG-013, EG-014]
review-by: 2027-09-30
supersedes:
---

- **Owner:** Engineering manager
- **Applies to:** All team members, all sites, and all tools and domains used
- **Enforcement:** Competence matrix reviews, onboarding audit, review
- **Related:** [EG-002](eg-002-values-and-ways-of-working.md), [EG-005](eg-005-ai-agent-usage.md), [EG-011](eg-011-technology-and-third-party.md), [EG-013](eg-013-coding-standard.md), [EG-014](eg-014-version-control-and-versioning.md)

> **Note:** Rules marked *(core)* apply to every product and cannot be tailored. Other rules, and all numeric values, are proposed defaults that a product may tailor in its conformance profile ([EG-001](eg-001-guidelines-governance.md)).

## Purpose

Keep skills, tool mastery and domain knowledge deliberately maintained, so that the team understands the tools and domain it depends on and no capability sits with a single person or site.

## Rules

1. **CMP-01** A competence matrix MUST be maintained covering languages, RTOS, silicon platforms, protocols, tools, domain areas, security and test, with levels 0 to 4. It is reviewed twice a year.
1. **CMP-02** Areas with a single competent person MUST be tracked as risks (PLN-05), with a plan to build cover.
1. **CMP-03** Expected depth for each tool MUST be defined (below) and used in onboarding and training plans.
1. **CMP-04** Each tool and domain area MUST have a champion who maintains a short "how we use X" page in `docs/how-to/` and answers questions. Champions are listed in the ownership register.
1. **CMP-05** Each domain area (protocols, standards, regulation, hardware, security, customer use) MUST have a named subject matter expert and deputy, and a short primer document.
1. **CMP-06** Onboarding MUST follow a documented path: environment set up in under one day by one command, a first-week checklist, a buddy, a guided walkthrough of these guidelines (not just a link) and a first PR through the full process.
1. **CMP-07** The environment setup MUST be tested in CI, so that onboarding does not rot.
1. **CMP-08** An annual training plan MUST exist, with protected learning time (proposed 5 percent), recorded by person.
1. **CMP-09** Knowledge sharing MUST be regular: technical talks, cross-site pairing or rotations and design walkthroughs of major components. Sessions SHOULD be recorded and stored.
1. **CMP-10** Rationale MUST be captured in ADRs and documents, not in people's heads. A handover checklist MUST be used when someone leaves or changes role.
1. **CMP-11** Key areas MUST have knowledge at two or more sites (VAL-07).
1. **CMP-12** Team members MUST be trained in effective and safe use of AI agents, including reviewing agent output and handling data ([EG-005](eg-005-ai-agent-usage.md), [EG-022](eg-022-security-and-data-protection.md)).
1. **CMP-13** New tool versions or tools MUST be introduced with training and a radar update (TEC-01).

## Expected depth by tool and domain

| Area | Expected understanding |
|------|------------------------|
| Git | Object model (commits, refs, the graph), rebase versus merge, reflog for recovery, bisect, worktrees, rerere, `cherry-pick -x`, history rewriting rules |
| Build system and linker | Build system internals, linker scripts, map files, memory layout, reproducibility |
| Compiler | Flags, optimisation and link-time optimisation effects, undefined behaviour, debuggability |
| Static analysis and test tools | What each checks, false positive profile, configuration, suppression rules |
| Debug and trace | Probes, breakpoints and trace, crash dump decoding, timing analysis |
| Target platform | Peripherals, memory map, errata, boot process |
| RTOS | Scheduling, priorities, synchronisation, memory model, interrupt handling |
| Bootloader and update | Chain of trust, image formats, atomic update, rollback |
| CI and containers | Pipeline structure, container toolchains, artefact handling |
| Domain and standards | Protocols, regulatory context and use cases for our products |

## Compliance

| Rule | Checked by |
|------|------------|
| CMP-01, CMP-02 | Competence matrix review, risk register |
| CMP-04, CMP-05 | Ownership register and how-to page check |
| CMP-06, CMP-07 | Onboarding feedback, CI environment setup job |
| CMP-08 | Training plan review |

## Checklist

Tick an item when it is true for your project. Rule IDs point to the detail above.

- [ ] A competence matrix covers languages, RTOS, platforms, protocols, tools, domains, security and test (CMP-01)
- [ ] Single-person areas are tracked as risks (CMP-02)
- [ ] Expected depth per tool is defined and used in training (CMP-03)
- [ ] Each tool and domain area has a champion and a how-to page (CMP-04)
- [ ] Domain experts and deputies are named and primers written (CMP-05)
- [ ] An onboarding path is documented and the environment is set up in under one day (CMP-06)
- [ ] Environment setup is tested in CI (CMP-07)
- [ ] An annual training plan has protected learning time (CMP-08)
- [ ] Knowledge sharing is regular and sessions are recorded (CMP-09)
- [ ] Rationale is captured in ADRs and docs, and a handover checklist exists for leavers (CMP-10)
- [ ] Key areas are known at two or more sites (CMP-11)
- [ ] The team is trained in safe and effective use of AI agents (CMP-12)
- [ ] New tools are introduced with training and a radar update (CMP-13)

## Applying to personal projects and AI agents

### Personal projects

Starts at the **Full** profile (see [personal-projects.md](personal-projects.md)). Treat the expected-depth table as your learning plan, especially git internals and the debug tools. Keep a short learning log and a `docs/how-to/` page for anything you had to relearn twice. A one-command environment setup is worth doing even solo, and it is what lets agents work reliably.

### AI agents

- Write or update a `docs/how-to/` page when you discover a non-obvious procedure (CMP-04, CMP-10).
- Keep the environment setup script working and tested (CMP-07).
- Point to ADRs and docs for rationale and do not rely on chat history (CMP-10).
