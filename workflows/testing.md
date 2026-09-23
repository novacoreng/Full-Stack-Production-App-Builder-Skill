# Testing

Use layered testing and verify real runtime behavior.

## Required layers where applicable

- unit
- component
- integration
- API
- database/migration
- E2E
- browser
- device
- visual regression
- accessibility
- performance
- security
- smoke/synthetic post-deploy

## Test data and environments

Use realistic but synthetic test data. Never copy production personal data into development/test environments unless an approved, documented, privacy-safe process exists.

Maintain separate test/staging credentials and services from production.

## Admin verification

After a successful non-production build/deployment, if the product has an admin role:
- provision a dedicated test-admin account using the test-admin lifecycle;
- verify admin UI and direct API authorization;
- verify ordinary users cannot reach privileged operations;
- test session expiry, logout/revocation, MFA/recovery, destructive-action safeguards, and audit logs;
- clean up or rotate temporary credentials.

## Resilience

Test:
- empty/many/invalid/duplicate/deleted states;
- expired sessions;
- unauthorized access;
- offline/intermittent networks;
- timeouts/server errors;
- retries and idempotency;
- interrupted flows;
- rotation/fold/resize;
- payment/webhook interruption;
- notification delivery failure where relevant.

## Traceability

Map each test to one or more requirement IDs and record verification evidence. A green build alone is not a release gate.
