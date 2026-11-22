# Video-Derived 20-Point Pre-Deployment Security Gate

Source: user-provided 53-second video titled "Claude vs Codex, which AI actually builds a more secure website". The video presents a 20-point checklist, not a reproducible benchmark comparing AI models. Do not infer that any model is more secure from this video. Its "100% Secure" ending is a marketing claim, not proof or a permissible guarantee.

## The 20 controls shown in the video

### 01 Injection and input
1. SQL injection: use parameterized queries and safe ORM boundaries; validate untrusted SQL fragments.
2. XSS: context-aware output encoding, safe rendering and sanitization where needed.
3. CSRF protection: protect state-changing cookie-authenticated actions with appropriate CSRF mitigations and cookie policy.
4. File uploads: validate content/type/size, authorization, isolation, safe storage and retrieval.
5. SSRF protection: restrict outbound destinations and redirects, block internal/metadata targets, and apply egress controls.

### 02 Auth and access
6. BOLA/IDOR: enforce ownership and tenant boundaries on every server-side object access.
7. Rate limiting: protect authentication, APIs and high-cost endpoints with appropriate limits and abuse controls.
8. Password hashing: use a reputable adaptive password hash with correct parameters, never reversible encryption or plaintext.
9. MFA protection: enforce verification, replay prevention, recovery security and step-up where applicable.
10. Server-side permissions: never rely on client UI to enforce roles, entitlements or actions.
11. RLS (row-level security): use and test RLS where supported and applicable; prevent bypass through privileged database views/functions or unsafe service-role exposure.

### 03 Secrets and tokens
12. JWT secret/key management: strong keys, validated algorithms/claims, rotation and secure storage.
13. API keys: keep server-side secrets off clients and source control; scope and rotate credentials.
14. No local-storage tokens: avoid persisting sensitive auth tokens in browser localStorage; prefer suitable secure session/cookie or platform-protected storage designs, with threat-model justification.
15. Default credentials: remove or disable vendor/example credentials, demo accounts and initial passwords before release.

### 04 Config and hygiene
16. CORS policy: allow only required trusted origins and methods; do not use wildcard origins with credentials.
17. Webhook signatures: verify provider signatures against raw payload as required, timestamps/replay protection and idempotent handling.
18. Source maps: assess production source-map exposure and avoid publicly distributing sensitive debug artifacts; source maps are not themselves secrets, so apply context-sensitive restrictions.
19. Clean production logs: redact tokens, personal data and secrets; retain useful structured operational logging and audit evidence rather than deleting logs.
20. Dependencies: inventory, scan, patch and monitor vulnerable or unmaintained dependencies, including transitive packages.

## Mandatory evidence-based execution
- After each build, evaluate all 20 items with PASS, FAIL, BLOCKED, NOT TESTED or NOT APPLICABLE, rationale, implementation reference and evidence. Prioritize impacted controls and critical regression tests after every change.
- Before deployment, complete the full applicable 20-point gate against the actual target build and environment. Use authorized, isolated test systems, synthetic accounts and bounded tests; do not attack production or third parties.
- Do not mark a control PASS solely because a code pattern exists or a checkbox was ticked. Verify real behavior and negative cases where feasible.
- Record defects, fixes and retests. Block release for unresolved critical vulnerabilities or material applicable security failures under existing release policy.
- A 20/20 checklist result means only that those 20 evaluated controls met their specified tests. It never means 100% security, zero vulnerabilities or immunity from attacks.
- Link results to the existing security matrix and post-build regression report. Do not duplicate conflicting requirements or force irrelevant technologies into a product.

This checklist supplements `workflows/security.md`, `workflows/security-audit-methodology.md`, `workflows/post-build-security-compliance-regression.md` and `templates/SECURITY_CONTROL_MATRIX.md`.
