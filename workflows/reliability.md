# Reliability, Operations, and Recovery

Design for failure before production.

## Reliability controls
Where applicable implement and test:
- health/readiness/liveness checks;
- structured logs with correlation/request IDs;
- metrics/traces and actionable alerts;
- timeouts;
- bounded retries/backoff;
- idempotency keys;
- queues/background jobs;
- dead-letter/replay handling;
- rate limits and abuse controls;
- caching with invalidation strategy;
- graceful degradation;
- feature flags/kill switches;
- database transaction/concurrency controls.

## Recovery
Document:
- backup frequency and retention;
- restore procedure;
- recovery point objective (RPO);
- recovery time objective (RTO);
- rollback strategy;
- migration rollback/forward-fix strategy;
- incident severity levels;
- on-call/owner;
- incident communication path.

Run a restore or recovery exercise when practical for production-critical systems. Do not claim disaster recovery readiness solely because backups exist.

## Cost and capacity
Track provider quotas, expected usage, storage growth, database growth, notification volume, AI token/model usage, bandwidth, and estimated monthly cost. Add alerts/budgets where supported.

A system is not operationally ready if its expected failure modes have no owner, detection, or recovery path.
