# SECURITY CONTROL MATRIX

Allowed statuses: PASS / FAIL / FIXED / BLOCKED / NOT IMPLEMENTED / NOT TESTED / NOT APPLICABLE.

| Control/domain | Threat / requirement | Implementation | Environment | Test / attack evidence | Status | Remaining risk / owner action |
|---|---|---|---|---|---|---|

Include applicable authentication, authorization/IDOR, RLS/database, secrets, OTP, rate limiting, cost abuse/bot controls, admin, identity/KYC, payments/webhooks, wallet/ledger/payouts, uploads, messaging/privacy, validation, web/CORS/headers, dependencies, logging/auditing, backup/restore, account deletion/retention, platform-store readiness, infrastructure/edge/origin/TLS and runtime QA controls.

Include the production foundations coverage in `workflows/production-engineering-foundations.md`, especially session/cookie security, token rotation, SSO/MFA/passkeys when applicable, CSP and security headers, SQLi/XSS/CSRF/SSRF, clickjacking, open redirects, traversal, command injection, mass assignment, IDOR, least privilege, dependency vulnerabilities, file uploads, webhook authentication, idempotency, rate limits, audit logs and restore validation. Record evidence, not assumed coverage.
