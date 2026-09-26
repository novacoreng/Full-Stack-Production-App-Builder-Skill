# Full-Stack Production App Builder

A reusable AI-agent skill for taking web and mobile applications from idea to verified production release.

## Canonical source package

This repository contains the actual skill source, not only a prompt or README.

- `SKILL.md` — canonical skill instructions and execution rules
- `workflows/` — discovery, requirements, PRD, TRD, UX/UI, UI quality/accessibility, web/mobile, adaptive/foldables, frontend/backend, API/database, auth/payments, infrastructure, testing, debugging, security, supply chain, performance, deployment, GitHub, legal/compliance, and tool orchestration
- `templates/` — PRD, TRD, Product Contract, process flows, feature matrix, infrastructure matrix, test-admin lifecycle, testing, security, deployment, database, project state, handoff, and device test matrix
- `references/` — platform, accessibility, security, engineering standards, Android, iOS, web, and foldable guidance
- `adapters/` — ChatGPT, Claude, and Codex platform notes
- `examples/` — phase reporting example

## Mandatory build loop

Every implementation phase follows:

**Build → Test → Verify → Fix → Lock → Move to next phase.**

A phase cannot be locked while required tests, acceptance criteria, integration checks, security checks, runtime verification, UI/accessibility verification, or documentation remain unresolved.

The detailed release gates are defined in `workflows/build-quality-gates.md` and should be applied to every implementation phase and release candidate.

## UI quality is a build gate

The builder does not treat UI as decoration or a compile-only concern. Every user-facing screen must be verified for visual hierarchy, semantic colors, spacing, typography, loading/skeleton/empty/error/success states, clutter, responsive/adaptive behavior, keyboard/focus behavior, accessibility, and runtime interaction. Automated checks are combined with manual browser/device verification where applicable.

## GitHub-first development

When GitHub tooling is available, the skill asks for or confirms the target repository before implementation, inspects it, checkpoints changes, commits meaningful milestones, and verifies remote state. It never claims a push occurred without tool evidence.

## Connected infrastructure

The builder treats infrastructure as part of the application. It selects only the services actually required by the accepted product/technical requirements and can orchestrate supported providers such as Supabase, Vercel, Cloudflare, AWS, OneSignal, payment/email/SMS providers, storage, observability, and AI services.

If a required project, folder, bucket, DNS record, OAuth application, webhook, credential, or other resource cannot be created by connected tooling, the skill marks it blocked, explains exactly what the developer must create, provides the smallest step-by-step setup, and resumes after confirmation. It never invents infrastructure or silently substitutes mocks.

## Technology selection

Technology is requirement-driven. React Native, Expo, Clerk, Convex, Next.js, Supabase, or any other framework/service is not mandatory merely because it is familiar. The builder evaluates requirements, platforms, existing infrastructure, cost, scalability, security, maintainability, team constraints, and migration impact, then records the selected architecture and rejected alternatives.

## Test-admin verification

After a successful non-production build/deployment, products with an admin role receive a dedicated test-admin lifecycle. Credentials are temporary/rotatable, least-privilege, non-production by default, stored only in approved secret storage, and never committed or printed. The agent uses the account to verify admin UI and backend authorization boundaries and cleans it up when the test window ends.

## Secure delivery and reliability

The skill adds dependency/secret/SAST/SCA checks, SBOM/dependency inventory where appropriate, protected CI/CD environments, artifact/commit traceability, health/readiness checks, observability, rate limits, idempotency, retries/timeouts, backups/restore, rollback, disaster recovery, incident runbooks, and cost/usage controls according to product risk.

## Engineering standards

The skill uses current standards as verification references, including OWASP ASVS, OWASP SAMM, NIST SSDF, NIST's generative-AI SSDF profile where applicable, and WCAG 2.2 for web accessibility. These are engineering baselines, not claims of certification or legal compliance.

## Legal/compliance audit

The skill includes a dedicated legal/privacy/compliance workflow covering age/child privacy, third-party resource loading, analytics/session replay, commercial email, subscriptions/automatic renewal, user uploads/copyright, privacy/consent controls, and owner-only external actions.

The workflow is an engineering audit, not legal advice. Jurisdiction and product applicability must be established and material legal conclusions should be reviewed by qualified counsel.

## Installation

### Claude
Use this repository as the canonical skill folder or package the folder with `SKILL.md` as its root when uploading a Claude Skill.

### Other Agent Skills-compatible platforms
Use `SKILL.md` as the canonical entry point and load supporting workflows/references as needed.

## Production principle

The skill does not declare a project production-ready merely because it builds. Required requirements, integrations, infrastructure, tests, security, privacy/compliance checks, UI/accessibility gates, deployment, observability, recovery, and verification gates must pass.
