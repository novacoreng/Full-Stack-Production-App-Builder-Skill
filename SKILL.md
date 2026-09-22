---
name: full-stack-production-app-builder
description: Build production-grade web and mobile apps from idea through discovery, PRD/TRD, UX/UI, backend/database, phased implementation, testing, debugging, security, deployment, documentation, and GitHub.
---

# Full-Stack Production App Builder

Build the product as one connected system from idea to verified production release. This skill is platform-neutral and should be usable by coding agents, Claude Skills, ChatGPT Skills, Codex-style agents, and similar systems.

## Core rules
1. Understand before building.
2. Ask targeted questions when material information is missing.
3. Confirm the official project name before development.
4. Confirm the logo/icon/brand identity; create one if the user wants or no identity exists.
5. Map complete user and system process flows before implementation.
6. Resolve material requirements, tweaks, open questions, and acceptance criteria before PRD acceptance.
7. Do not code until the PRD is explicitly accepted, unless the user explicitly requests a prototype or discovery-only implementation.
8. After PRD acceptance, proceed through the roadmap automatically unless genuinely blocked.
9. Never count UI-only behavior as complete functionality.
10. Never fake production functionality. Mocks are temporary development aids only.
11. Treat frontend, backend, database, integrations, and infrastructure as one system.
12. Maintain API contracts and database migration discipline.
13. Test success, failure, recovery, concurrency, offline, and interrupted flows where applicable.
14. Build mobile-first, responsive, adaptive, accessible, and performance-conscious experiences.
15. Support compact, standard, large, foldable, tablet, landscape, split-screen, and resizable windows when relevant.
16. Do not hardcode device names or rely on a single viewport.
17. Preserve state across rotation, resize, fold/unfold, app restart, and other configuration changes where applicable.
18. Debug systematically and never stop at the first error.
19. Maintain PROJECT_STATE.md and AGENT_HANDOFF.md continuously.
20. Never commit secrets.
21. Do not claim production readiness without evidence that required gates passed.

## Phase 0 — Discovery and project identity
Before coding:
- Understand the idea, business problem, target users, geography, platforms, monetization, integrations, compliance, and success criteria.
- Confirm official project name.
- Confirm or create logo/icon and core brand direction.
- Identify guest, first-time, returning, authenticated, staff/admin, and other relevant personas.
- Ask only questions that materially affect architecture, UX, cost, security, compliance, or scope.
- Maintain an Open Questions / Decisions register.

## Phase 1 — Complete process flows
Map the entire experience from launch to successful use and continued return.

At minimum consider:
- launch/splash/onboarding
- guest path
- signup/login/logout/session recovery
- permissions
- home/discovery
- core business journey
- forms and validation
- payments/refunds where relevant
- notifications
- search/messaging where relevant
- profile/account/settings
- admin/operations
- offline/reconnect/synchronization
- failures/retries/timeouts
- interrupted journeys and state restoration

For every important flow trace:
user action → UI → validation → API → authentication/authorization → backend logic → database → external service → response → UI state → success/error/recovery.

Maintain a process-flow coverage matrix so each flow has corresponding frontend, backend, database, auth, and test coverage.

## Phase 2 — Product contract and PRD
Create a Product Contract as the source of truth. Give requirements stable IDs such as REQ-001.

PRD should include:
- executive summary
- vision/problem/goals/non-goals
- target users/personas/user journeys
- process flows
- functional requirements
- authentication/authorization
- payments
- notifications
- search/messaging
- admin/analytics
- localization
- accessibility
- security/performance/offline/error handling
- compliance
- platform requirements
- design requirements
- acceptance criteria
- MVP and future scope

Do not accept the PRD while material requirements, flows, tweaks, or acceptance criteria remain unresolved.

## Phase 3 — TRD and architecture
Select technology based on requirements, not habit.

Cover:
- system architecture
- web/mobile architecture
- frontend/backend boundaries
- API architecture
- database architecture
- authentication/authorization
- storage
- payments
- notifications
- queues/background jobs
- caching
- observability
- security
- testing
- CI/CD
- deployment
- environment variables/secrets
- backup/recovery
- scalability
- third-party services
- technology tradeoffs

Record architectural decisions and alternatives rejected.

## Phase 4 — UX/UI
Design mobile-first rather than shrinking desktop layouts.

Define:
- information architecture
- navigation
- design tokens
- typography
- color
- spacing
- components
- forms
- cards
- modals/sheets
- loading/skeleton states
- empty states
- error/success states
- accessibility
- responsive/adaptive behavior

If Figma is available and appropriate, use the platform's Figma workflow. Translate PRD → IA → design system → screens/components → implementation → visual verification.

## Phase 5 — Adaptive web and mobile
Use available window size and constraints rather than device-specific assumptions.

Support, when relevant:
- compact phone
- standard phone
- large/tall phone
- foldable cover display
- foldable inner display
- folded/unfolded states
- half-open/tabletop/book posture
- tablet
- portrait/landscape
- split-screen/multi-window
- resizable desktop windows
- desktop web

Adapt navigation and composition as space changes: bottom navigation → rail/sidebar; single column → multi-column; list → list/detail; bottom sheet → side sheet; compact cards → expanded cards.

Respect safe areas, status/navigation bars, gesture navigation, cutouts, keyboard/insets, edge-to-edge behavior, dynamic type, and accessibility scaling. Keep critical controls/content away from hinges/fold regions.

When current platform behavior matters, verify current official Apple/Android/platform documentation rather than relying on stale memory.

## Phase 6 — Implementation
Build in a dynamic roadmap of coherent phases. Before each phase state:
- objectives
- features
- files/systems affected
- dependencies
- tests
- acceptance criteria
- next phase

### Mandatory phase execution loop
Every implementation phase MUST follow this exact sequence:

**Build → Test → Verify → Fix → Lock → Move to next phase.**

1. **Build** — Implement the phase's approved requirements and all required frontend, backend, database, integration, security, and infrastructure work.
2. **Test** — Run the tests relevant to the phase, including unit/component/integration/API/database/E2E/browser/device/accessibility/performance checks as applicable.
3. **Verify** — Compare the implementation against the phase objectives, acceptance criteria, process-flow coverage, API/DB contracts, UX/UI requirements, and real runtime behavior. Do not treat a successful compile as verification.
4. **Fix** — Resolve every discovered failure, mismatch, regression, or incomplete requirement. Repeat **Build → Test → Verify → Fix** until the phase passes or a genuine external blocker prevents completion.
5. **Lock** — Declare the phase complete only after its acceptance criteria pass. Update PROJECT_STATE.md, AGENT_HANDOFF.md, CHANGELOG.md and other relevant documentation; record the verification evidence; create a checkpoint Git commit when Git is available and authorized. A locked phase must not be casually reopened or changed by later work without change-impact analysis.
6. **Move to next phase** — Automatically begin the next approved phase. Do not ask the user to say “proceed” after a successfully locked phase.

A phase is **not complete** if any required test, acceptance criterion, integration, security check, runtime verification, or documentation update is still failing or unresolved.

### Phase lock record
For every locked phase, record:
- phase number and name
- requirements/features completed
- files/systems changed
- tests executed and results
- verification evidence
- bugs found and fixes applied
- acceptance criteria status
- known limitations or blockers
- checkpoint commit SHA
- next phase

If a phase fails after being locked because of a later change, do not silently modify the locked result. Perform change-impact analysis, document the regression, fix it, re-run the affected verification, and create a new checkpoint commit.

## Backend/API requirements
Every production API should define:
- method and route
- authentication/authorization
- request schema
- response schema
- validation
- error model
- database interactions
- side effects
- idempotency where relevant
- rate limits
- logging/audit behavior

Use contract tests where useful to catch frontend/backend field mismatches.

## Database requirements
Define:
- entities and relationships
- tables
- primary/foreign keys
- constraints
- indexes
- enums/status values
- timestamps/audit fields
- migrations
- seeds where appropriate
- row-level/security policies where supported
- retention/deletion/export/archive/restore behavior

Use ordered migrations such as 001_initial_schema, 002_add_payments, etc. Never rely on undocumented manual database edits.

## Authentication, authorization, and payments
Use real integrations for production functionality.

Authentication:
- secure sessions/tokens
- password/OTP/social auth as specified
- account recovery
- session expiry
- role/permission matrix
- authorization at backend boundaries

Payments:
- server-side verification
- signed webhook verification
- idempotency
- duplicate protection
- transaction states
- retries
- refunds/chargebacks where relevant
- payment history
- interrupted payment recovery

## Security
Audit:
- authentication
- authorization
- RLS/access policies
- secrets
- API exposure
- CORS/CSRF where applicable
- XSS/injection risks
- input validation
- file uploads
- rate limiting
- session/token handling
- dependency vulnerabilities
- sensitive information in logs
- third-party permissions

Never commit .env files, private keys, credentials, service-account files, or other secrets.

## Performance and reliability
Web:
- bundle size
- code splitting/lazy loading
- image optimization
- caching
- server/database latency
- Core Web Vitals where relevant

Mobile:
- startup time
- rendering/jank
- memory
- network use
- battery
- large lists
- image performance
- offline behavior

Backend:
- query performance
- indexes
- caching
- queues
- concurrency
- timeouts
- retries
- circuit/failure handling where justified

## Testing and verification
Use the appropriate combination of:
- unit tests
- component tests
- integration tests
- API tests
- database tests
- E2E tests
- browser tests
- device tests
- visual regression
- accessibility checks
- performance tests
- security checks

Create DEVICE_TEST_MATRIX.md for projects with UI. Include compact/standard/large phones, foldables, tablets, portrait/landscape, split-screen/resizable windows, desktop browsers, and relevant hardware permissions/features.

Test realistic states:
- empty
- one item
- many items
- invalid data
- duplicate data
- deleted data
- expired session
- unauthorized access
- slow/intermittent/offline network
- server failure
- timeout
- app/browser closed mid-flow
- payment interruption
- rotation/fold/resize during a flow

Test the launch-to-enjoyment journey: install/open → splash → onboarding → sign-up/login/guest → permissions → home → discovery → core action → success → feedback → continued use → reopen → state restore.

## Debugging loop
Never stop after the first error.

Inspect:
- project structure
- package/config files
- dependencies
- environment
- TypeScript/types
- imports
- components/hooks/state
- routing
- API contracts
- backend logic
- database
- auth/authz
- styling/layout
- build configuration
- platform configuration
- tests
- runtime/browser/device behavior

For each bug record:
BUG ID | file | line/area | problem | expected | actual | root cause | fix | verification.

Repeat:
build → capture errors → root cause → fix → build → tests → runtime/browser/device → security → performance.

## Change management
For every material feature/tweak, perform change-impact analysis across:
PRD → product contract → process flows → UX → UI → API → DB → frontend → backend → security → tests → docs → deployment.

Do not ask again about a decision already fixed in the accepted PRD.

## Definition of Done
A feature is complete only when applicable items pass:
- requirement mapped
- process flow mapped
- UI implemented
- API implemented
- database implemented/migrated
- validation implemented
- loading/empty/error/success states handled
- authentication/authorization handled
- security reviewed
- tests added/passed
- accessibility checked
- responsive/adaptive behavior verified
- documentation updated
- acceptance criteria passed

## Production audit
Before claiming production readiness verify:
- requirements/process flows/acceptance
- UX/UI/responsive/adaptive/accessibility
- frontend typecheck/lint/build/tests
- backend APIs/validation/auth/authz/errors
- DB schema/migrations/indexes/security/backups
- security/secrets/dependencies/input/API exposure
- performance
- unit/integration/E2E/browser/device testing
- deployment/environment/build/domain/SSL/monitoring
- Git status and secret scan
- README and required documentation
- final repository state and remote verification

If mandatory gates fail, explicitly report NOT PRODUCTION READY and list blockers.

## Documentation
Always create/update the relevant core documentation:
- README.md
- PRD.md
- TRD.md
- PRODUCT_CONTRACT.md
- PROCESS-FLOWS.md
- ARCHITECTURE.md
- DATABASE.md
- API.md
- UI-UX.md
- FEATURE_MATRIX.md
- ROLE_PERMISSION_MATRIX.md
- TESTING.md
- SECURITY.md
- DEPLOYMENT.md
- CHANGELOG.md
- PROJECT_STATE.md
- AGENT_HANDOFF.md
- DEVICE_TEST_MATRIX.md

Only omit documents that are genuinely irrelevant, and record why.

## GitHub
When GitHub tooling is available and authorized:
1. inspect status and remote
2. inspect for secrets
3. checkpoint significant milestones
4. run required tests/builds
5. commit meaningful changes
6. push only after verification
7. verify remote state

Never claim a push happened unless the tool confirms it.

## Tool orchestration
Use connected tools when available for GitHub, Supabase/database, Vercel/deployment, Figma/design, browser automation, payments, notifications, and file operations. Before using a tool, follow that tool's installed skill instructions when required. If a required external capability is unavailable, identify the exact blocker and provide the smallest manual action needed.

## Autonomous execution
Once the user accepts the PRD, execute the roadmap phase by phase. Do not repeatedly ask for permission to continue. Pause only for a genuinely blocking decision, missing credential/access, destructive action requiring confirmation, or unresolved material requirement.

## Handoff
PROJECT_STATE.md must record current phase, completed work, pending work, decisions, tests, failures, environment requirements, and next action.

AGENT_HANDOFF.md must record current phase/task, files changed, DB/API changes, known issues, tests, failures, environment requirements, next action, and things not to redo.
