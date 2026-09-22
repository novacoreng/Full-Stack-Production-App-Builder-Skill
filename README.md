# Full-Stack Production App Builder

A reusable AI-agent skill for taking web and mobile applications from idea to verified production release.

## Canonical source package

This repository contains the actual skill source, not only a prompt or README.

- `SKILL.md` — canonical skill instructions and execution rules
- `workflows/` — discovery, requirements, PRD, TRD, UX/UI, web/mobile, adaptive/foldables, frontend/backend, API/database, auth/payments, testing, debugging, security, performance, deployment, GitHub, legal/compliance, and tool orchestration
- `templates/` — PRD, TRD, Product Contract, process flows, feature matrix, testing, security, deployment, database, project state, handoff, and device test matrix
- `references/` — platform, accessibility, security, Android, iOS, web, and foldable guidance
- `adapters/` — ChatGPT, Claude, and Codex platform notes
- `examples/` — phase reporting example

## Mandatory build loop

Every implementation phase follows:

**Build → Test → Verify → Fix → Lock → Move to next phase.**

A phase cannot be locked while required tests, acceptance criteria, integration checks, security checks, runtime verification, or documentation remain unresolved.

## Legal/compliance audit

The skill includes a dedicated legal/privacy/compliance workflow covering age/child privacy, third-party resource loading, analytics/session replay, commercial email, subscriptions/automatic renewal, user uploads/copyright, privacy/consent controls, and owner-only external actions.

The workflow is an engineering audit, not legal advice. Jurisdiction and product applicability must be established and material legal conclusions should be reviewed by qualified counsel.

## Installation

### Claude
Use this repository as the canonical skill folder or package the folder with `SKILL.md` as its root when uploading a Claude Skill.

### Other Agent Skills-compatible platforms
Use `SKILL.md` as the canonical entry point and load supporting workflows/references as needed.

## Production principle

The skill does not declare a project production-ready merely because it builds. Required requirements, integrations, tests, security, privacy/compliance checks, deployment, and verification gates must pass.
