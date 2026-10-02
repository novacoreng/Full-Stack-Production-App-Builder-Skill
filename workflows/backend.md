# Backend
Implement business logic with validation, authentication, authorization, transactions, idempotency, rate limits, logging, errors, retries, concurrency controls, and real database/external-service integration. Keep secrets outside source control.


## Runtime/API QA
For backend/API-only or full-stack phases, execute real requests against the intended non-production environment where tooling permits. Test authentication, server-side authorization, invalid payloads, idempotency, concurrency, database state, provider boundaries, timeout/retry/restart behavior, and logs. Do not infer API success from frontend code or mocks. Follow `device-interactive-qa.md`.
