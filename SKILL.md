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
- tests passed;
- documentation updated;
- acceptance criteria passed;
- GitHub checkpoint created and verified.

All other workflows and capability registries in this repository remain applicable, including UX/UI, accessibility, skeleton loaders, semantic colors, clutter audits, testing, security, reliability, regulatory/compliance, AI, integrations, payments, and deployment.