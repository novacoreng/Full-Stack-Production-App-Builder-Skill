# Production Security Hardening and Release Gate

Use a risk-based application-security process aligned where applicable with OWASP ASVS and NIST SSDF. Security is an engineering release gate, especially for authentication, money, identity/KYC, private data, admin capabilities, messaging, uploads, and other high-impact systems.

## Security model: never trust the client

Assume web/mobile clients are hostile and inspectable. Local/session storage, AsyncStorage, persisted state, route parameters, request bodies, IDs, JavaScript bundles, APK/IPA contents, and API calls can be read, changed, replayed, or issued outside the UI.

**The client may request. The server decides.**

Server-authoritative controls must determine identity, role, permissions, ownership, verification/KYC state, approval/moderation state, payment status, wallet/ledger state, withdrawal status, financial amounts, bank/provider verification, sender/author identity, and other privileged state.

Do not treat UI hiding, route guards, obfuscation, endpoint renaming, client-side role checks, encrypted client role state, or disabling developer tools as authorization.

## Canonical architecture gate

Before security-sensitive changes, determine the canonical/current frontend, backend, API target, database, deployment environment, workers, and production path. If multiple stale or competing backend implementations exist, determine which the application actually calls and which is intended for production. Backend ambiguity affecting security is a release blocker; do not duplicate/weaken controls across stale implementations.

## Attack-surface inventory

Before hardening, map relevant:
- web/mobile/admin entry points;
- API/auth/OTP/KYC/payment/webhook/wallet/withdrawal/messaging/upload endpoints;
- databases, sensitive tables, RLS/access policies, database functions;
- storage buckets and public/private access;
- service-role/privileged credentials;
- background/scheduled workers and queues;
- third-party integrations/providers;
- secrets/configuration and environment boundaries;
- CI/CD, deployment, DNS, hosting, cloud IAM, dependencies and supply chain.

Maintain a `SECURITY_ATTACK_SURFACE.md` or equivalent when appropriate. Never put secret values in it.

## Required security domains

Audit applicable domains:
1. authentication and session lifecycle;
2. authorization, privilege escalation, IDOR/BOLA and ownership;
3. API validation, output filtering, injection and mass assignment;
4. payments, wallet/ledger, payouts/refunds and financial integrity;
5. database, RLS/access policies and privileged/service-role usage;
6. admin/moderation authorization and auditability;
7. KYC/identity and highly sensitive identifiers;
8. file/media upload, storage and download authorization;
9. messaging/comments/privacy and server-derived authorship;
10. mobile reverse engineering, secure storage and client secret exposure;
11. web security: XSS, CSRF where applicable, cookies, CORS, redirects, clickjacking, CSP/headers;
12. infrastructure, dependencies, CI/CD, supply chain and environment configuration.

Cross-cutting review includes business-logic abuse, replay/idempotency, race conditions/concurrency, privacy/data minimization, logging, rate limits, secrets, transport security, error handling, recovery, and production configuration.

## Authentication

Audit signup/login/logout, OTP, refresh/recovery, token/session storage, invalidation, expiry/revocation and returning sessions. Where OTP exists, use secure server verification, short expiry, single-use where architecture permits, attempt/resend/rate limits, and avoid account enumeration. Never log OTPs, passwords, session tokens, refresh tokens, or other authentication secrets.

## Authorization / IDOR / BOLA

Derive identity from a verified authenticated session/token and retrieve/check server-authoritative permissions. Client-stored role or ownership is never authoritative.

For sensitive resources test:
- no token, invalid/expired token;
- ordinary user vs privileged operation;
- User A accessing/modifying User B;
- changed resource/user/account/organization IDs;
- client role/permission/verification tampering;
- direct API access without the UI.

Use appropriate 401/403 and, when intentionally avoiding disclosure, 404 behavior. Frontend route guards are supplementary only.

## API security

Every sensitive endpoint should have appropriate authentication, authorization, schema/input validation, explicit allowlists/DTOs, output filtering, request-size controls, rate/abuse limits, safe error handling and audit logging.

Reject unexpected privileged fields and prevent mass assignment. Use parameterized data access and defend applicable SQL/NoSQL/command/path/header/template injection classes. Do not return fields merely because they exist in the database.

## Financial integrity

Financial state is server-authoritative. Never trust client `success`, payment status, amount, balance, recipient, approval, screenshot, callback redirect, or transaction status.

Typical authoritative flow:

**Client → Server creates intent/reference → Provider → Server verifies signed/provider evidence → Server independently verifies transaction/context → Atomic settlement → Auditable ledger → Client receives server-authoritative status**

Verify reference, amount, currency, intended account/recipient/context, provider state, and webhook authenticity before settlement.

Financial mutations must be authenticated, authorized, idempotent, atomic, auditable, and safe under concurrency. Use integer minor units or another proven exact monetary representation; never use floating point for authoritative money.

Prevent replay, duplicate settlement/payout, reference reuse, amount/recipient substitution, double spend, negative balances, race-condition balance creation and concurrent overspend. Ledger entries and balances must not be ordinary client-editable CRUD state.

For withdrawals/payouts test destination substitution, duplicate requests, concurrent withdrawal, KYC/identity gates, provider ambiguity, failure/reversal/release and retry. Do not mark payout successful without authoritative provider evidence.

Do not run destructive attack tests with real production funds.

## Database / RLS / privileged keys

Classify sensitive data (for example PUBLIC, AUTHENTICATED, OWNER-ONLY, SERVER-ONLY, ADMIN-ONLY, FINANCIAL, IDENTITY/KYC). Test actual policies as anonymous, User A, User B, privileged/admin/backend service. Enabling RLS alone is not proof that policies are correct.

Normal clients must not directly change role/permissions/admin state, verification/KYC state, wallet/ledger, payout approval, moderation state, settlement/provider verification, or equivalent privileged fields.

Service-role keys, payment/provider secrets, private keys, database credentials and other privileged credentials must never ship in public web/mobile bundles, public environment variables, committed source, public config, analytics, crash reports, or logs. If a real secret is discovered in source/history, treat it as compromised and require rotation; deleting the current file alone is insufficient. Never print the secret in the report.

## Admin security

Discovering an admin URL provides zero privilege. Every admin API/action independently enforces server-side authorization. Sensitive admin actions should record who, what, target, when, and result without logging unnecessary secrets or highly sensitive data. Test normal users directly against admin endpoints and self-escalation paths.

Any approved bootstrap/exemption mechanism must be server-controlled, identity-bound, centralized and auditable; it must not become an authentication, authorization, payment, or provider-compliance bypass.

## Identity/KYC and sensitive identifiers

Verification state must originate from authoritative server/provider processing. Prevent forged success, replay, reference/account substitution and client-controlled verified flags. Validate provider callbacks/results per provider requirements.

Treat government/identity identifiers as highly sensitive. Avoid raw values in logs, analytics, URLs, crash reports, public responses and unnecessary client caches. Enforce uniqueness without disclosing another person's identity. Prefer provider references, fingerprints/tokenization, or other privacy-preserving representations supported by the architecture.

Bank-account resolution alone is not necessarily proof of ownership. Where product rules require identity matching, mismatches/review states must fail closed.

## Files/media

Validate allowed MIME/type and, where feasible, file signature; size; generated safe names; destination; authorization; public/private access; and download authorization. Do not trust extensions alone. Prevent traversal, overwrite, executable/script upload execution, dangerous active content, oversized uploads, and unauthorized private-file access. Identity/KYC/private documents must not inherit public-media access rules.

## Messaging/comments/privacy

Scope conversations/comments/resources to authorized participants/context. Server derives sender/author identity; do not trust client `senderId`/`authorId`. Test changed conversation/resource IDs, spoofed authors, locked/terminal states, and cross-user access. Public profile/campaign data must use explicit safe response shapes and must not expose unrelated private account, identity, financial, contact, token, or bank data.

## Mobile/web client security

Assume APK/IPA and JavaScript bundles are inspectable. Keep privileged secrets server-side; obfuscation is not secret storage. Use appropriate native secure storage for sensitive client tokens and do not log them.

For web surfaces evaluate XSS (stored/reflected/DOM), CSRF where applicable, cookie attributes, redirects, clickjacking, injection, CORS, unsafe HTML, dependencies, CSP and appropriate security headers. Credentialed/sensitive APIs must not use indiscriminate production origins. CORS never replaces authentication/authorization.

Production transport must use HTTPS and must not silently fall back to localhost, LAN, temporary tunnels, or insecure HTTP.

## Rate limiting and abuse

Apply server-side limits to sensitive endpoints such as login, signup, OTP request/verify, recovery, content/message creation, uploads, payment initialization, withdrawals, KYC initiation and admin authentication. Use appropriate account/IP/device/risk dimensions without creating trivial denial-of-service against legitimate users.

## Replay, idempotency and race conditions

Explicitly test repeated and concurrent payment/webhook, financial mutation, withdrawal, verification callback, unique-registration and other high-risk operations. Database constraints, transactions, locking/serialization and idempotency must preserve invariants. A prior `if balance >= amount` check followed by an independent later update is not sufficient.

## Client-storage tampering

Where relevant, modify client-accessible role, admin, verification, balance and permission state, then attempt privileged operations. UI may temporarily display incorrect local state, but no server privilege or authoritative financial/verification state may change. Any protected server operation succeeding due to client tampering is a critical failure.

## Fail closed

If authorization, verification/KYC, provider/payment evidence, wallet/ledger mutation, or other security-critical state cannot be determined, do not guess success. Use appropriate PENDING/PROCESSING/UNKNOWN/FAILED or equivalent states. Ambiguity is not success.

## Errors, logging and privacy

Production client errors must not expose stack traces, SQL/database internals, filesystem paths, tokens, secrets, provider credentials, or infrastructure details. Keep useful sanitized server observability.

Apply data minimization and explicit safe response shapes. Audit logs/telemetry for passwords, OTPs, identity numbers, JWTs/refresh tokens, service-role keys, payment/KYC secrets and full sensitive bank data. Use correlation/request IDs where appropriate and preserve auditable financial/admin/security events.

## Infrastructure and supply chain

Review dependencies/lockfiles, CI workflows, deployment/build configuration, environment handling, debug flags, source maps where relevant, cloud/provider configuration and production logging. Use secret scanning, SCA/dependency checks, SAST, SBOM/inventory, container scanning and license review where appropriate.

Do not blindly run destructive dependency upgrades. For a finding, determine affected package, severity, exploitability/reachability, safe compatible upgrade and regression risk; then patch and retest.

CI/CD uses least privilege and protected secret stores. Untrusted PR code must not trivially gain production secrets. Separate development/staging/production credentials. Search current tree and history for exposed credentials where practical.

## Security test workflow

For every security-sensitive fix:

**PLAN → IMPLEMENT → STATIC CHECK → UNIT/INTEGRATION TEST → NEGATIVE SECURITY TEST → RUN → ATTACK THE CONTROL → OBSERVE → FIX → RETEST → REGRESSION TEST → VERIFY**

Add automated regression tests where practical for privilege escalation, IDOR/BOLA, protected fields, verification spoofing, replay, duplicate settlement, overspend/concurrency, RLS/access policy, messaging/comment/upload authorization, rate limits, uniqueness and secret/config validation.

Perform attack testing only in authorized development/test/sandbox environments. Never use real money or real-user sensitive identity/KYC data for destructive security testing.

## Severity and release gate

Classify findings CRITICAL, HIGH, MEDIUM, LOW or INFORMATIONAL using impact/exploitability and project context. Do not downgrade findings to make a report look better.

Unresolved CRITICAL vulnerabilities block production. Unresolved HIGH findings affecting authentication, authorization, financial integrity, KYC/PII, admin or payments also block production unless an explicitly reviewed/documented mitigation and risk acceptance exists.

If a required provider credential/configuration is unavailable, mark the test **PROVIDER BLOCKED**, not PASS. **UNKNOWN = NOT VERIFIED. NOT TESTED = NOT SECURELY VERIFIED.**

Security hardening must not silently redesign or remove approved product functionality merely to make tests pass.

## Security evidence and reporting

Never report `unhackable`, `100% secure`, or `perfectly secure`. Report tested scope and evidence.

For substantial/high-risk products maintain a `SECURITY_AUDIT_REPORT.md` containing:
- executive summary and canonical architecture;
- attack surface and environments;
- findings by applicable security domain;
- vulnerabilities fixed/remaining;
- provider-blocked and not-tested areas;
- regression/security tests added;
- runtime/device/API attack tests;
- dependency/secret/supply-chain results;
- files changed and verified commit SHAs;
- production blockers and remaining risk;
- overall recommendation: **BLOCKED** or **SECURITY GATES PASSED FOR CURRENT TESTED SCOPE**.

Maintain a scorecard for applicable domains using **PASS / FAIL / BLOCKED / NOT TESTED**. At minimum cover authentication, authorization, API, financial integrity where applicable, database/RLS, admin, identity/KYC, files/media, messaging/privacy, mobile secret exposure, web security, infrastructure/dependencies, privacy, concurrency, and replay/idempotency.
