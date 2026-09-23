# Deployment

Separate development, preview/test, staging, and production environments.

## Pre-deployment

Verify:
- target commit/artifact;
- build and test status;
- dependency/security/secret checks;
- environment variables and secrets by name/scope;
- database migrations and rollback;
- storage and RLS/authz;
- webhooks and signature verification;
- domains/DNS/TLS where applicable;
- provider quotas/cost limits;
- backups and restore capability;
- observability and alerting;
- rollback strategy.

## Deployment

Use protected production environments and least-privilege deployment credentials. Do not deploy unverified working-tree changes.

## Post-deployment

Run:
- health/readiness checks;
- authenticated smoke tests;
- critical user-flow E2E tests;
- admin test account verification in non-production/staging where applicable;
- error/log checks;
- notification/webhook checks;
- performance sanity checks;
- database and storage verification.

Record the deployed commit/version and evidence.

## Failure

If any mandatory gate fails, mark the release **NOT PRODUCTION READY**, identify the blocker, and fix/retest. Never hide deployment failures behind a successful build command.
