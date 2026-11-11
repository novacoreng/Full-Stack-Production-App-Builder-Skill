# Production Engineering Foundations and Security Coverage

This workflow incorporates the topics explicitly visible in the four user-supplied screenshots. Treat them as serious engineering considerations, not a mandate to add every technology to every application. Assess applicability based on product risk, traffic, scale, data sensitivity, deployment architecture and approved TRD. Never invent implementation or test evidence.

## Mandatory assessment categories

### Infrastructure, scalability and resilience
- Load balancing, horizontal vs vertical scaling, stateless services, reverse proxies, API gateways, CDNs and caching: choose based on measured traffic, bottlenecks and architecture; do not add infrastructure without justification.
- Rate limiting, brute-force protection, account lockout, timeouts, exponential backoff, circuit breakers, connection pooling, read replicas, message queues, background jobs and cron jobs: specify limits, retry policies, duplicate prevention, failure recovery and operational ownership where relevant.
- Cache invalidation, health checks, graceful shutdown, backups, tested restores and disaster recovery: document consistency, readiness/liveness behavior, RPO/RTO and recovery exercises.
- Docker, CI/CD, staging environments, feature flags, infrastructure as code, code review, branching strategies, semantic versioning and deployment rollback: choose a reproducible, reviewable delivery process.
- Cost monitoring, performance budgets, load testing, memory leak detection, concurrency, race conditions and async/await: establish measurable thresholds and verify under realistic workloads.

### Backend, APIs and data
- Environment variables and secrets management: never hardcode or log credentials; restrict access, rotate and audit secrets.
- Authentication, authorization, role-based access control, least privilege, row-level security, session management, SSO, passkeys, magic links, MFA and password reset: use only applicable mechanisms; test privilege boundaries and lifecycle.
- Input validation and server-side data validation, HTTP status codes, error handling, API documentation and versioning: define typed contracts and safe failure responses; do not trust client validation.
- Database normalization, indexing, migrations, connection pooling, soft deletes and data retention: assess schema integrity, query plans, migration rollback and deletion semantics.
- Webhooks: authenticate source, handle replay, deduplicate and ensure idempotent processing.
- File uploads: verify type/content, size, permissions, storage isolation, malware risk and download access.
- Idempotency: protect payment, messaging, job and mutation retries from duplicate side effects.
- Character encoding: validate Unicode and safe output encoding for the supported locales.

### Security and privacy
- HTTPS/TLS, encryption at rest/in transit, hashing vs encryption, password salting, token expiration/refresh, secure cookie flags (HttpOnly, Secure, SameSite), secret rotation and audit logs.
- Defend against SQL injection, XSS, CSRF, SSRF, clickjacking, open redirects, path traversal, command injection, mass assignment, IDOR/BOLA and other applicable attack classes.
- Enforce content security policy and other relevant security headers; validate redirect and outbound request destinations.
- Review dependency vulnerabilities, software supply chain, third-party SDK behavior and principle of least privilege.
- Assess GDPR and other applicable privacy regimes, consent, minimization, retention and deletion rights; jurisdiction-specific rules require appropriate legal review.
- Conduct authorized, safe security testing and document findings with evidence. Do not equate a checklist with a completed penetration test.

### Observability, quality and usability
- Structured logging, monitoring, alerting, error tracking, uptime monitoring and distributed tracing: use privacy-safe instrumentation, actionable alerts and documented incident ownership.
- Unit, integration and end-to-end tests, automated testing, load tests and regression checks: cover critical flows and failures, not only happy paths.
- Accessibility, mobile responsiveness, platform safe areas and keyboard navigation: validate actual device/browser behavior.
- Technical debt: track risk, ownership and remediation; read official documentation and actual error messages before changing implementation.

## Phase gate and evidence
For each topic, record REQUIRED / NOT APPLICABLE / BLOCKED, with rationale, implementation location, test or review evidence, owner and follow-up. An applicable item must be implemented and verified before its acceptance gate, or explicitly marked BLOCKED. Never claim a technology is present solely because it is listed here.

Map this workflow to PRD risk assumptions, TRD architecture decisions, security control matrix, testing plan, infrastructure matrix and phase reports. In every phase report, summarize newly verified controls and carry forward open blockers. For production release, block unresolved critical risks and other material failures under the existing security and release rules.

## Source interpretation
The screenshots list engineering topics rather than instructions, configurations, implementation code or test results. The checklist above operationalizes those topics. The final screenshot contains a truncated word resembling "Penetra", so treat it as a prompt to assess penetration testing, not evidence that any testing occurred.
