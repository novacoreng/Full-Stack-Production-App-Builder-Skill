# Mandatory Post-Build Security, Abuse, Functionality and Legal QA

## Enforcement
After EVERY build or phase implementation, perform applicable static checks, automated tests and authorized interactive regression tests before reporting the phase as complete. Repeat after fixes. Evaluate every control below with PASS, FAIL, BLOCKED, NOT TESTED or NOT APPLICABLE, evidence, affected code or environment, severity, owner and remediation. A committed build is not evidence that security tests passed. Do not probe production or third-party systems without explicit authorization. Use isolated test infrastructure, synthetic accounts and safe bounded cases. Never publish attack payloads, secrets or personal data in reports.

## A. Legal, privacy, accessibility and consumer trust
The user-provided screenshots explicitly list:
1. Privacy policy
2. Terms and conditions
3. Cookie policy
4. Cookie consent
5. Refund policy
6. Form consent
7. Only necessary data
8. Analytics tracking
9. Third-party embeds
10. Accessibility
11. Alt text
12. Color contrast
13. Keyboard-friendly forms
14. Clear button labels
15. Remove fake reviews
16. Unsupported claims
17. Business details
18. Image copyright
19. Applicable local laws
20. Other legal risks

Test that legal pages and notices accurately describe the real product; that optional trackers and embeds respect applicable consent before loading; that user data collection is minimized; that keyboard-only and assistive technology flows work; that image assets have appropriate license records; and that claims, reviews, prices and business details are authentic. Obtain jurisdiction-specific legal review when needed. A checklist is not a legal guarantee. Also cross-reference `workflows/consumer-trust-privacy.md`.

## B. Advanced technical attack classes
The screenshot titled "20 (pen-test level) ways a stranger hacks your vibecoded app" identifies:
1. HTTP/2 Rapid Reset and request/resource exhaustion
2. Oversized or boundary-length usernames (example: 52 characters)
3. SAML authentication bypass
4. Email spoofing due to missing or misconfigured authentication
5. GraphQL alias amplification
6. Two-factor code replay
7. ReDoS in regular expressions
8. JWT algorithm confusion
9. HTTP request smuggling
10. Cache poisoning
11. Spoofed IP or forwarded headers
12. Database views bypassing row-level security
13. Predictable tokens generated with Math.random
14. Timing side channels
15. Padding oracle weaknesses
16. Prototype pollution
17. Template injection
18. XXE and unsafe XML file parsing
19. WebSocket session hijacking
20. Unicode normalization or confusable-character account/identifier abuse

For each applicable class, inspect implementation/configuration and perform safe local or staging regression checks. Test boundaries and abuse resistance without uncontrolled load, real user targeting or production exploitation. Mark SAML, GraphQL, XML, WebSocket, JWT, HTTP/2 and other technology-specific checks NOT APPLICABLE when absent, with rationale. Use cryptographically secure randomness for secrets; validate identity and ownership at backend boundaries. Review server/proxy-specific mitigations rather than assuming application code alone can fix protocol-layer attacks.

## C. Direct application abuse and business logic
The screenshot titled "15 ways I'd hack your vibe coded app" identifies:
1. Change a link/resource ID: test IDOR/BOLA and ownership enforcement
2. Sign up as admin: test server-enforced role assignment and privilege escalation
3. Grab a master key: inspect exposed service-role/API keys, build artifacts and permissions
4. Go pro for free: test subscription entitlements against trusted server state
5. Pay twice at once: test concurrent payment idempotency and transaction integrity
6. Spam an AI button: test rate limits, quotas, abuse controls and cost ceilings
7. Trick a chatbot: test prompt injection, tool permissions and data isolation
8. Edit the price: reject client-controlled totals, verify server-calculated prices
9. Fake a payment: verify signed provider webhooks and server-side settlement state
10. Unlock the paywall: enforce server-side content and feature authorization
11. Sign up when closed: enforce registration policy at the backend
12. Skip login: test protected routes, APIs, sessions and access control
13. Download your code: prevent exposure of private source, source maps and secrets
14. Find .env in git: scan repository history and build artifacts for secrets
15. Read your database: validate RLS, tenant isolation, query permissions and backup/storage access

For payment and financial apps, test duplicate webhook delivery, retries, refunds, concurrent mutations, ledger consistency and reconciliation with non-live fixtures. For AI apps, test tool-call boundaries and sensitive-data exposure with synthetic content. Do not add payment or AI tests to apps that do not implement those capabilities.

## Required post-build sequence
1. Identify changed code and affected trust boundaries. Re-evaluate applicability of all three groups.
2. Run formatter/linter, type checking, dependency/security scans, secret scans and automated tests appropriate to the project.
3. Execute safe focused regression checks against changed features and critical auth, data and financial boundaries.
4. Test actual deployed preview or isolated staging flows where available, including mobile safe areas, keyboard, errors, and permissions.
5. Review logs, monitoring, cost and error signals without exposing secrets.
6. Fix confirmed issues, add regression tests, rerun impacted checks and record unresolved risks.
7. Publish the complete phase roadmap with verified ticks, test evidence, blockers, commit SHA and ZIP handoff status.
8. Block phase acceptance or release for unresolved critical security vulnerabilities and other material applicable violations. If tools or access are unavailable, mark BLOCKED/NOT TESTED and provide exact next action.

## Report format
For each build: build ID/commit; environment; changes; applicable tests; PASS/FAIL/BLOCKED/NOT TESTED/NOT APPLICABLE; evidence or links; confirmed findings with severity; fixes and retests; remaining risk; phase checklist; ZIP status. Do not assert that an audit, penetration test, simulator test or compliance review occurred unless actually performed.

Use together with `workflows/security.md`, `workflows/security-audit-methodology.md`, `workflows/device-interactive-qa.md`, `workflows/consumer-trust-privacy.md`, `templates/SECURITY_CONTROL_MATRIX.md` and `examples/phase-report.md`.
