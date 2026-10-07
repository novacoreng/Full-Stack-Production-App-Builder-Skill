# Phased Build, GitHub Checkpoints, and Infrastructure Orchestration

## Pre-production gate sequence

Production implementation MUST NOT begin until the following artifacts have been created/audited, accepted, and locked in order:

**PRD → TRD → App Flow → Design Brief → Background Schema → Documentation Plan → Production**

Each gate must trace to the accepted requirements. Existing artifacts may be reused only after current-state audit and explicit lock. Material changes trigger downstream impact analysis and re-locking before production continues.

The Background Schema defines the backend/data model before production migrations: entities/tables, typed fields, relationships, constraints/indexes, ownership/tenancy, RLS/authorization, lifecycle states, audit fields, migration approach, retention and sensitive-data classification.

The Documentation Plan identifies living project documentation, update triggers, evidence, and ownership so documentation is maintained during the build rather than written only at the end.


## Mandatory phased delivery

Every project is built in explicit, numbered phases derived from the accepted PRD, TRD, process-flow matrix, capability matrix, and architecture decisions.

Before each phase, publish:
- phase number and name;
- objective;
- requirements/features covered;
- frontend work;
- backend/API work;
- database/migration work;
- integrations/infrastructure work;
- notifications/communication work where applicable;
- security/access-control work;
- tests and acceptance criteria;
- expected GitHub checkpoint.

After the phase, publish what was actually built, tests run, verification evidence, fixes, known limitations, and the next phase.

## Mandatory phase loop

**Build → Test → Verify → Fix → Lock → Commit → Move to next phase.**

A phase is not locked until all applicable acceptance criteria and required verification pass or a documented external blocker is explicitly accepted. If a blocker exists, record it and do not claim the phase is complete.

## GitHub checkpoint policy

GitHub is the source-of-truth history when a repository is connected and the user has authorized commits.

For every phase:
1. inspect the current repository state;
2. implement the phase;
3. test and verify;
4. fix failures;
5. update project state, handoff, changelog, and relevant architecture/docs;
6. create a meaningful checkpoint commit;
7. verify the commit SHA and changed files on GitHub;
8. only then lock the phase and start the next phase.

Never batch multiple completed phases into one final commit when the repository is available. The phase history must show the progression of the build.

Commit messages should identify the phase, for example:
- `Phase 01: project foundation`
- `Phase 02: authentication and onboarding`
- `Phase 03: core data and backend`
- `Phase 04: notifications and integrations`

Never claim a commit or push happened without tool evidence.

## TRD-driven backend configuration

The TRD is the authoritative source for infrastructure and backend requirements. During each phase, compare the work against the TRD and configure every backend service that is required by that phase, not only the frontend.

The builder must consider, where applicable:
- database and migrations;
- authentication/authorization;
- RLS/access policies;
- storage buckets and access rules;
- server functions/API routes;
- queues/background jobs;
- scheduled jobs;
- webhooks;
- payment configuration;
- email/SMS providers;
- push notifications;
- OneSignal or another selected notification provider;
- analytics and observability;
- error tracking;
- file processing;
- search;
- realtime channels;
- AI/model providers;
- DNS/domains;
- hosting/deployment environments;
- environment variables and secret names;
- backups and recovery;
- rate limits and usage controls.

Do not wait until the final phase to discover that required backend infrastructure is missing.

## Connected-provider execution

When a required provider is connected/logged in and the available tooling supports the required action, configure it during the relevant phase and verify the resulting resource/configuration.

Examples:
- connected Supabase → configure project/database/schema/RLS/storage/functions as required;
- connected Vercel → configure project/environment/deployment settings as required;
- connected Cloudflare → configure Workers/DNS/edge resources as required;
- connected AWS → configure only the AWS resources justified by the TRD and available permissions;
- connected OneSignal → configure app/platform credentials, notification channels, and environments as required;
- connected GitHub → commit each locked phase and verify remote history.

Use the least privilege required. Never expose or commit provider secrets.

## Missing-provider / missing-resource protocol

If the TRD requires a provider, project, folder, bucket, database, DNS record, OAuth application, webhook, credential, notification app, or other resource that is not connected or cannot be created by the available tooling:

1. mark the exact item `BLOCKED` in the infrastructure matrix;
2. explain why it is required and which phase depends on it;
3. tell the developer exactly what connection/permission/resource is needed;
4. provide concise step-by-step setup instructions using the provider's current official documentation where appropriate;
5. offer to guide the developer through the setup step by step;
6. resume configuration immediately after the connection/resource is available;
7. verify the resource before marking the phase ready.

Never invent resource IDs, URLs, credentials, deployment status, or successful configuration.

## Notifications are infrastructure

Treat notifications as a complete backend capability, not a UI-only feature. Where notifications are required, configure and verify:
- provider/app/project;
- iOS and Android credentials where applicable;
- development/staging/production separation;
- notification permissions;
- device token registration;
- token refresh/revocation;
- server-side send authorization;
- templates/content;
- deep links;
- preference/opt-out controls;
- delivery/error handling;
- retries where appropriate;
- analytics/receipts where supported;
- rate limits;
- test delivery;
- failure recovery.

Do not mark a notification feature complete because a notification button renders. Verify the complete event → backend → provider → device → tap/deep-link flow.

## Backend verification gate

Before locking a phase that changes backend behavior, verify as applicable:
- migration applied;
- schema matches the TRD;
- authorization/RLS enforced server-side;
- API contract matches frontend usage;
- secrets are server-side;
- webhook signatures verified;
- idempotency/retry behavior tested;
- error and timeout paths tested;
- logs/observability available;
- required external services reachable;
- notification/payment/email integrations tested;
- production and non-production environments are not accidentally mixed.

## Infrastructure evidence

Record for each configured resource:
- provider;
- environment;
- resource type/name;
- resource ID or safe reference;
- configuration performed;
- permission scope;
- verification result;
- phase;
- related commit SHA;
- owner/manual action if applicable.

Do not record secret values.

## Final release history

At completion, the final document must include a phase-by-phase GitHub history showing:
- phase;
- implementation summary;
- infrastructure/backend changes;
- test/verification result;
- checkpoint commit;
- deployment/version evidence;
- remaining limitations, if any.

The final release must be traceable from requirements → phase → code → infrastructure → tests → verification → GitHub commit → deployment.