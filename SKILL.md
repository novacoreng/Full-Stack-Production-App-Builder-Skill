---
name: full-stack-production-app-builder
description: Build production-grade web and mobile apps from idea through discovery, PRD/TRD, UX/UI, backend/database, phased implementation, testing, debugging, security, deployment, documentation, and GitHub.
---

# Full-Stack Production App Builder

Build the product as one connected system from idea to verified production release. This skill is platform-neutral and requirement-driven.

## Core rules
1. Understand before building.
2. Ask targeted questions when material information is missing.
3. Confirm project name and logo/icon before development.
4. Map complete user and system process flows before implementation.
5. Resolve material requirements, tweaks, open questions, and acceptance criteria before PRD acceptance.
6. Do not code until the PRD is explicitly accepted unless the user explicitly requests a prototype/discovery implementation.
7. After PRD acceptance, proceed through the roadmap automatically unless genuinely blocked.
8. Treat frontend, backend, database, integrations, notifications, and infrastructure as one system.
9. Select technology from requirements; never force React Native, Expo, Clerk, Convex, Supabase, Next.js, PostgreSQL, Vercel, AWS, Cloudflare, or any other technology merely because it is available.
10. Build production-grade, responsive, adaptive, accessible experiences for relevant phones, foldables, tablets, desktop, and web environments.
11. Never commit secrets.
12. Never claim production readiness or external configuration without evidence.
13. Maintain PROJECT_STATE.md, AGENT_HANDOFF.md, CHANGELOG.md, and relevant phase records continuously.

## Mandatory pre-production build flow
Before production implementation begins, every project must pass these planning gates in this order:

**PRD → TRD → App Flow → Design Brief → Background Schema → Documentation Plan → Production**

Do not skip, merge away, or silently reorder these gates. If an artifact already exists, audit it against the current accepted requirements and explicitly re-accept/lock it before moving forward.

1. **PRD** — lock product purpose, users, scope, requirements, product rules, acceptance criteria, non-goals and success conditions.
2. **TRD** — translate the accepted PRD into architecture, technology decisions, frontend/backend responsibilities, APIs, integrations, infrastructure, security, environments, testing and deployment requirements.
3. **App Flow** — map complete user journeys and system flows from entry through success, failure, recovery, continued use and return; include auth, permissions, backend/provider interactions and exceptional states.
4. **Design Brief** — define approved visual/product direction, information hierarchy, responsive/adaptive behavior, accessibility, interaction patterns, component/state requirements, branding constraints and design references without changing locked product rules.
5. **Background Schema** — define the underlying data/backend model required to support the PRD/TRD/app flows: entities/tables, fields/types, relationships, constraints, indexes, ownership/tenancy, RLS/authorization, lifecycle/statuses, audit fields, migrations, retention and sensitive-data classification. This is a design artifact before production migrations are applied.
6. **Documentation Plan** — define which living documents must be created/maintained during production, their owners/update triggers and evidence requirements. At minimum consider PROJECT_STATE, AGENT_HANDOFF, CHANGELOG, API/database/infrastructure/security/testing/deployment docs and product-specific compliance/runbooks.
7. **Production** — only after gates 1–6 are locked may production implementation begin. Production then follows the numbered phase loop, applicable workflow matrix, GitHub checkpoints, testing, security and release gates.

A material change after a gate is locked requires change-impact analysis across all downstream artifacts. Update and re-lock every affected downstream gate before continuing production work.

## Mandatory pre-production build flow
Before production implementation begins, every project must pass these planning gates in this order:

**PRD → TRD → App Flow → Design Brief → Background Schema → Documentation Plan → Production**

1. **PRD**: lock product purpose, users, scope, requirements, rules, acceptance criteria, non-goals and success conditions.
2. **TRD**: translate the PRD into architecture, technology decisions, frontend/backend responsibilities, APIs, integrations, infrastructure, security, environments, testing and deployment requirements.
3. **App Flow**: map complete user and system journeys including success, failure, recovery, auth, permissions and provider/backend interactions.
4. **Design Brief**: lock visual direction, information hierarchy, responsive/adaptive behavior, accessibility, interactions, components/states, branding constraints and approved references.
5. **Background Schema**: define the underlying backend/data model before production migrations: entities/tables, typed fields, relationships, constraints, indexes, ownership/tenancy, authorization/RLS, lifecycle states, audit fields, migration approach, retention and sensitive-data classification.
6. **Documentation Plan**: define the living documents, update triggers, evidence and ownership required throughout the build, including state, handoff, changelog, API, database, infrastructure, security, testing, deployment and applicable compliance/runbooks.
7. **Production**: production implementation starts only after gates 1–6 are accepted and locked. It then follows the numbered phase loop, workflow coverage matrix, GitHub checkpoints, testing, security and release gates.

Do not silently skip or reorder these gates. Existing artifacts may be reused only after auditing them against current accepted requirements. A material change after a gate is locked requires downstream change-impact analysis and re-locking of every affected artifact before production continues.

## Phase-based delivery
Every project MUST be divided into explicit numbered phases derived from the accepted PRD, TRD, process-flow matrix, capability matrix, and architecture decisions.

Before each phase, state:
- objective;
- requirements/features covered;
- frontend work;
- backend/API work;
- database/migrations;
- integrations/infrastructure;
- notifications/communication where applicable;
- security/access-control work;
- tests and acceptance criteria;
- expected GitHub checkpoint.

### Mandatory phase loop
**Build → Test → Verify → Fix → Lock → Commit → Move to next phase.**

TEST and VERIFY include interactive runtime/device/browser/API testing where applicable. Compilation, static checks, unit tests, or CI alone do not prove real-user functionality. Follow `workflows/device-interactive-qa.md` whenever the environment/tooling can run the product.

A phase is not locked until applicable acceptance criteria and required verification pass, or a genuine external blocker is documented. After a successful lock, automatically begin the next phase; do not require the user to say “proceed.”

### GitHub checkpoint rule
When a GitHub repository is connected and authorized:
1. inspect repository state before the phase;
2. build the phase;
3. test, verify, and fix;
4. update state/handoff/changelog and relevant docs;
5. create a meaningful phase checkpoint commit;
6. verify the commit SHA and changed files remotely;
7. only then lock the phase and move forward.

Do not batch multiple completed phases into one final commit. The Git history should show the build progression. Example messages:
- `Phase 01: project foundation`
- `Phase 02: authentication and onboarding`
- `Phase 03: core data and backend`
- `Phase 04: notifications and integrations`

Never claim a commit/push occurred without tool evidence.

## TRD-driven infrastructure and backend
The TRD is authoritative for backend and infrastructure requirements. During every phase, configure the backend resources required by that phase rather than postponing backend work until the end.

Consider, where applicable:
- database/schema/migrations;
- authentication/authorization/RLS;
- storage buckets and access rules;
- server functions/API routes;
- queues/background jobs/scheduled tasks;
- webhooks;
- payments;
- email/SMS;
- push notifications;
- analytics/observability/error tracking;
- realtime;
- search/file processing;
- AI/model providers;
- DNS/domains/hosting;
- environment variables/secrets;
- backups/recovery;
- rate limits/usage controls.

If a required provider is connected and tooling permits the action, configure it during the relevant phase and verify it. Use least privilege and never expose secrets.

### Missing provider/resource protocol
If a required provider or resource is not connected or cannot be created with available tooling:
1. mark it `BLOCKED` in the infrastructure matrix;
2. explain why it is required and which phase depends on it;
3. identify the exact connection, permission, project, bucket, database, DNS record, OAuth app, webhook, credential, notification app, or other resource required;
4. give concise setup steps using current official documentation where appropriate;
5. offer to guide the developer step-by-step;
6. resume configuration when available;
7. verify the resource before locking the dependent phase.

Never invent IDs, URLs, credentials, deployments, or configuration status.

### Notifications
Notifications are backend infrastructure, not UI-only features. When required, configure and verify the complete event → backend → provider → device → tap/deep-link flow, including platform credentials, environments, permission handling, device-token registration/refresh, server-side authorization, templates, preferences/opt-out, retries/errors, rate limits, analytics/receipts where supported, and test delivery.

### Backend verification gate
Before locking a backend-changing phase, verify as applicable:
- migration applied and schema matches TRD;
- authorization/RLS enforced server-side;
- API contract matches frontend;
- secrets remain server-side;
- webhook signatures and idempotency are handled;
- error/timeout/retry behavior is tested;
- observability is available;
- required external services are reachable;
- notification/payment/email integrations work;
- environments are not accidentally mixed.

Record provider, environment, resource, safe ID/reference, configuration, permission scope, verification, phase, commit SHA, and manual owner action. Never record secret values.

## Final traceability
The final project document must show:
**requirements → process flow → phase → code → backend/infrastructure → tests → verification → GitHub checkpoint → deployment/version evidence.**

## Phase lock record
For every locked phase record:
- phase number/name;
- requirements/features completed;
- files/systems changed;
- backend/infrastructure changes;
- tests and results;
- verification evidence;
- bugs and fixes;
- acceptance criteria status;
- blockers/limitations;
- checkpoint commit SHA;
- next phase.

A later regression requires change-impact analysis, a fix, re-verification, and a new checkpoint commit.

## Definition of Done
A feature is complete only when applicable items pass:
- requirement and process flow mapped;
- UI implemented;
- API/backend implemented;
- database implemented/migrated;
- integrations/infrastructure configured;
- notifications configured where required;
- loading/empty/error/success states handled;
- authentication/authorization handled;
- security reviewed;
- accessibility checked;
- responsive/adaptive behavior verified;
- static checks passed;
- automated tests passed;
- backend/database contract verified;
- interactive action tested where runtime interaction is available;
- relevant failure state tested;
- authorization/privacy checked;
- relevant runtime logs inspected;
- regression test passed;
- device/browser verification completed or explicitly marked pending/unavailable;
- provider verification completed or explicitly marked blocked;
- tests passed;
- documentation updated;
- acceptance criteria passed;
- GitHub checkpoint created and verified.

All other workflows and capability registries in this repository remain applicable, including UX/UI, accessibility, skeleton loaders, semantic colors, clutter audits, testing, security, reliability, regulatory/compliance, AI, integrations, payments, and deployment.

## Security release gate
For security-sensitive or high-impact products, use `workflows/security.md` as a mandatory release gate. Assume the client is hostile; enforce identity, authorization, verification and financial state server-side; test direct API abuse, IDOR/BOLA, client-state tampering, replay and concurrency; audit secrets/RLS/storage/providers/supply chain; fail closed on ambiguous security-critical state; and never claim “100% secure.” Unresolved CRITICAL findings block production, and applicable HIGH findings in authentication, authorization, financial integrity, KYC/PII, admin or payments require reviewed mitigation/risk acceptance before release.

## Interactive runtime verification
A successful build is not proof that the application works for a real user. For substantial applications, discover the available QA environment, start the actual stack, install/launch where applicable, interact with reachable controls and product-specific journeys, monitor runtime logs, test failure paths, and record objective evidence.

Use `workflows/device-interactive-qa.md` and `templates/DEVICE_INTERACTIVE_QA.md`. Distinguish IMPLEMENTED, AUTOMATED TESTED, EMULATOR/SIMULATOR TESTED, PHYSICAL DEVICE TESTED, and LIVE PROVIDER VERIFIED. Unknown remains UNKNOWN; blocked remains BLOCKED; not tested remains NOT TESTED. No silent dead controls.


## Production security, privacy, store and edge hardening
For production/security audits use an evidence-first sequence: **AUDIT → THREAT MODEL → ATTACK TEST → IDENTIFY → PLAN → FIX → TEST → RETEST → DOCUMENT → RELEASE GATE**. Establish the canonical deployed architecture before changing security-sensitive backend or infrastructure. Documentation describes implemented controls, not assumptions.

Apply `workflows/abuse-cost-controls.md`, `workflows/account-deletion-data-retention.md`, `workflows/app-store-release.md`, and `workflows/cloudflare-origin-security.md` when relevant. Use `templates/SECURITY_CONTROL_MATRIX.md` and `templates/APP_STORE_RELEASE_CHECKLIST.md` for evidence. Legal/platform requirements must be checked against current authoritative requirements for the relevant jurisdiction/platform; uncertain interpretations remain LEGAL REVIEW REQUIRED or BLOCKED/NOT TESTED rather than being invented.

For infrastructure-sensitive changes follow **AUDIT → BACKUP → PLAN → VERIFY RECOVERY → APPLY → TEST → VERIFY → DOCUMENT**. Do not modify DNS, firewalls, certificates, production databases, credentials, payment/auth architecture or provider callbacks without a recovery/rollback path and verification evidence.


## Strict workflow applicability gate
The workflow library is **mandatory-by-applicability**, not optional guidance. At discovery and again before every phase lock/release, evaluate every workflow in `workflows/` against the accepted PRD/TRD, architecture, platforms, data, providers, risk, distribution targets, and current phase.

For each workflow record exactly one status:
- **REQUIRED** — applies and must be executed before the dependent phase/release can lock;
- **EXECUTED** — required work was performed and evidence recorded;
- **BLOCKED** — applies but cannot be completed because of an external/resource/access blocker;
- **NOT APPLICABLE** — does not apply, with a concrete reason.

There is no silent **SKIPPED** state. A workflow may not be ignored because it is inconvenient, unfamiliar, time-consuming, or because another workflow partially overlaps it. Overlapping workflows are composed; they do not cancel one another.

### Mandatory workflow families
Always evaluate the complete workflow set, including discovery/requirements/project identity, PRD/process flows/TRD, capability analysis/toolkit, phased GitHub/infrastructure, UX/UI/frontend/adaptive/mobile/web/foldables, API/backend/database/auth/payments, notifications/integrations where required, UI quality/accessibility, testing/device interactive QA/debugging/build-quality, security/supply-chain/abuse-cost controls, performance/reliability, legal/regulatory/account deletion/store compliance, deployment/infrastructure/Cloudflare where applicable, test personas/admin where applicable, tool orchestration, and GitHub/handoff/state documentation.

Platform/provider-specific workflows such as foldables, payments, app-store release, Cloudflare origin security, test-admin, or account deletion are not forced onto irrelevant products; they must instead be explicitly marked NOT APPLICABLE with the reason. If they apply, they become mandatory.

### Phase lock enforcement
Before locking a phase:
1. enumerate workflows relevant to that phase;
2. execute every REQUIRED workflow;
3. attach verification/evidence;
4. mark external blockers BLOCKED with exact remediation;
5. record NOT APPLICABLE decisions with reasons;
6. run the workflow coverage check;
7. refuse to mark the phase complete if any applicable workflow remains unevaluated or required-but-unexecuted.

Before production release, repeat the applicability audit across the **entire** workflow directory. Production readiness cannot be claimed while an applicable workflow is missing evidence, an unexplained workflow is unevaluated, or a release-blocking workflow remains BLOCKED/FAIL.

### Strict evidence rule
A workflow is not “used” because its file exists, is referenced in documentation, or code appears compatible with it. **Used means evaluated, executed where applicable, tested, and evidenced.** Never fabricate execution status. If tooling/access cannot perform a required workflow, mark BLOCKED rather than weakening the gate.

## Mandatory consumer trust and anti-deception gate
Apply `workflows/consumer-trust-privacy.md` during PRD, TRD, app flow, design brief, background schema, documentation planning, implementation, testing and release. Prohibit deceptive reviews/likes/AI claims, spam, hidden analytics leakage, unjustified biometric collection, missing required privacy notices, unlawful children's-data processing and obstructive subscription cancellation. Require appropriate marketing unsubscribe/opt-out, truthful disclosures, data minimization, lawful consent/basis, end-to-end tests and documented evidence. Block release for applicable unresolved violations; mark jurisdictional interpretation LEGAL REVIEW REQUIRED. Never claim lawsuit-proof status.

## Mandatory legal, privacy, accessibility and transparency checklist
At planning, build, QA and release, apply all 20 controls in `workflows/consumer-trust-privacy.md`: accurate privacy policy and terms, truthful reviews/claims, refund policy, accessible alt text, contrast and keyboard navigation, cookie/tracking disclosures and consent where required, valid form consents, verified business details, data minimization, children's privacy, third-party SDK audits, working marketing unsubscribe, no dark patterns, asset/font/image licensing, transparent fees and actionable data-deletion requests. Verify behavior end-to-end, not just documentation. Applicable material failures block release; jurisdiction-specific questions require legal review.
