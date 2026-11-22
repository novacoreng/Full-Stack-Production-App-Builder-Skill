# Mandatory Phased Build, User Acceptance Testing and On-the-Go Debugging

## Non-negotiable phase workflow
Every app build follows the accepted PRD -> TRD -> App Flow -> Design Brief -> Background Schema -> Documentation Plan gates, then an explicit numbered implementation roadmap. Each implementation phase has scope, acceptance criteria, applicable workflow/control coverage, implementation, automated checks, interactive preview verification, security/privacy/accessibility regression, documentation update, GitHub checkpoint, ZIP handoff and user-facing status. No silent skipping or merging phases merely to claim completion.

A phase can be marked [x] only after required acceptance criteria and applicable tests have passed and required approval is recorded. A build that compiles but fails its acceptance tests remains IN PROGRESS or BLOCKED.

## Mandatory controls per phase
Evaluate the strict workflow coverage matrix and at minimum the relevant controls from:
- `workflows/production-engineering-foundations.md`: auth, data, infrastructure, observability, resilience and operations.
- `workflows/security.md` and `workflows/security-audit-methodology.md`: threat boundaries, least privilege, secrets, tenant isolation and defensive validation.
- `workflows/post-build-security-compliance-regression.md` and `workflows/video-20-point-predeploy-security.md`: applicable attack classes, business logic abuse and video-derived 20-point security gate.
- `workflows/consumer-trust-privacy.md`: legal disclosures, consent, data minimization, accessible interfaces, truthful claims, transparent billing and user rights.
- `workflows/device-interactive-qa.md` and `workflows/expo-eas-simulator-testing.md` where relevant: real device/simulator interaction, safe-area insets, mobile navigation, forms and errors.
- `workflows/secure-email-verification-cross-device.md` where email/password registration is supported.
- `workflows/blueprint-branding-zip-handoff.md`: approved branding and phase ZIP artifacts.

Mark each control PASS, FAIL, BLOCKED, NOT TESTED or NOT APPLICABLE with evidence. The presence of a checklist is not proof of a tested implementation.

## Full-test checkpoint after each build
After the automated and available interactive checks, explicitly offer the user a **full end-to-end test of the current preview build**. Provide a verified preview URL or installable test artifact only if it exists; provide a compact test plan with critical user journeys, expected outcomes and synthetic test accounts or setup instructions where safe. Never fabricate a link, deployment, user account or test result.

The user may choose to test now, request an agent-led full test, report an issue, or defer optional user acceptance testing. Do not imply that optional user participation replaces mandatory engineering tests. When explicit user acceptance is required by the project, mark the phase AWAITING USER ACCEPTANCE until approval; otherwise document deferred user testing and enforce the existing release gates.

## Debugging on the go
For every reported issue:
1. Record phase/build/commit, device/browser/OS, route or screen, reproduction steps, expected and actual result, screenshots/logs when available, severity and impact.
2. Reproduce in authorized preview/staging or isolated tests, find root cause and fix only the relevant scope.
3. Add a regression test where feasible, rerun impacted automated, interactive, security and accessibility checks.
4. Provide a fresh verified preview/test build and ask for retest if the issue needs user confirmation.
5. Track OPEN -> REPRODUCED -> FIXED -> RETESTED -> VERIFIED or BLOCKED, with actual evidence. Do not call an issue fixed based on a commit alone.
6. Preserve unrelated projects, production data, branding and infrastructure.

## Every-phase response format
- Phase number/name and implementation summary
- Build/preview availability, verified link or artifact if available
- Automated and interactive test outcomes with evidence
- Security, privacy, accessibility and data-control coverage status
- Defects, fixes, blockers and known limitations
- Full-test offer and concise user test scenarios
- GitHub commit, ZIP delivery status and environment
- **Entire numbered phase roadmap** with [x] for verified accepted phases, [ ] for pending phases and clear IN PROGRESS / BLOCKED / AWAITING USER ACCEPTANCE labels
- Next phase and production release gate status

Do not proceed to production with unresolved critical security vulnerabilities, material applicable legal failures, or mandatory acceptance tests marked NOT TESTED/BLOCKED. Preview-first testing and explicit production approval remain required where the project policy demands it.
