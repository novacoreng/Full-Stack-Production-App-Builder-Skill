# Full-Stack Production App Builder

A reusable AI-agent skill for taking web and mobile applications from idea to verified production release.

## Installation

### Claude
Zip this folder with the folder itself as the ZIP root. Upload it through Claude's Skills UI.

### Other Agent Skills-compatible platforms
Use the same folder containing SKILL.md as the canonical skill package. Platform-specific instructions should live in adapters rather than changing the core workflow.

## What it covers

Discovery, project identity, process flows, PRD, TRD, UX/UI, responsive/adaptive design, foldables, frontend, backend, database, APIs, authentication, payments, security, privacy/legal compliance auditing, performance, testing, debugging, deployment, documentation, GitHub, project state, and agent handoff.

## Mandatory build loop

Every implementation phase follows:

**Build → Test → Verify → Fix → Lock → Move to next phase.**

A phase cannot be locked while required tests, acceptance criteria, integration checks, security checks, runtime verification, or documentation remain unresolved.

## Legal/compliance audit

The skill includes a dedicated legal/privacy/compliance workflow covering age/child privacy, third-party resource loading, analytics/session replay, commercial email, subscriptions/automatic renewal, user uploads/copyright, privacy/consent controls, and owner-only external actions.

The workflow is an engineering audit, not legal advice. Jurisdiction and product applicability must be established and material legal conclusions should be reviewed by qualified counsel.

## Production principle

The skill does not declare a project production-ready merely because it builds. Required requirements, integrations, tests, security, privacy/compliance checks, deployment, and verification gates must pass.
