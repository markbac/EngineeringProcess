# AGENTS.md

Instructions for AI coding agents working in this repository. Read this file first. The full guidelines are in `docs/guidelines/` and a condensed rule list is in `docs/guidelines/agent-rules.md`.

## Project

One paragraph: what this repository is, the target hardware or platform, and the main language.

## Commands

- Build: `<command>`
- Unit tests: `<command>`
- Lint and format: `<command>`
- Static analysis: `<command>`
- Everything CI runs: `<command>`
- Docs: `<command>`

## Conventions

- Commits: Conventional Commits, with `Refs:` for requirement or issue IDs and `Assisted-by:` for AI assistance
- Branches: short-lived `feat/`, `fix/`, `docs/` and `chore/`. Never push to `main`
- Requirements: `docs/requirements/`. Cite IDs as `REQ-...`
- Decisions: `docs/adr/`. Propose a new ADR for significant or hard-to-reverse decisions, and never edit accepted ones
- Principles: CP-02 simplicity, CP-16 surgical changes, CP-20 surface assumptions. When a rule is silent, apply `docs/guidelines/principles.md`
- Rules marked *(core)* cannot be tailored. Other rules follow the product conformance profile in `docs/conformance-profile.md`

## Boundaries

Do not modify any of the following without explicit instruction in the task: guidelines, `AGENTS.md`, pipeline definitions, CODEOWNERS, secrets and signing material, generated or vendored code, security-relevant code, and shared history. Never disable, skip or weaken a test or check.

Never put secrets or personal data in code, logs, commits or prompts.

## Working method

1. State assumptions and open questions before starting. Ask if a requirement is missing or ambiguous.
1. Make the smallest change that meets the requirement. Report unrelated problems and do not fix them in passing.
1. Add or update tests with the change. Reproduce a bug with a failing test before fixing it.
1. Run the full local check command and include the results in the PR.
1. Update documentation in the same change.
1. Open a PR with a Conventional Commit title and the filled template. Never approve or merge your own work.

## Definition of done

Builds cleanly, tests pass, lint and analysis are clean, docs are updated, the PR template is completed, and commits carry `Refs:` and `Assisted-by:`.

## Where things are

- Guidelines index: `docs/guidelines/README.md`
- Agent rules (condensed): `docs/guidelines/agent-rules.md`
- Principles: `docs/guidelines/principles.md`
- Component register: `docs/components.yaml` (where the product has one)
- Templates: `docs/templates/`
