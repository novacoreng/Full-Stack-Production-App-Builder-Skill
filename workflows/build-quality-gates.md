# Build Quality Gates Workflow

Use this workflow for every implementation phase and for every release candidate. It extends the mandatory phase loop without replacing it.

## Phase loop

**Build → Test → Verify → Fix → Lock → Move to next phase.**

Never treat a successful compiler/build as sufficient verification.

## Gate 1 — Product and scope
Before implementation:
- Confirm the approved requirement IDs and acceptance criteria.
- Confirm the affected process flows.
- Perform change-impact analysis across UX/UI, frontend, API, database, integrations, security, tests, docs, and deployment.
- Confirm required infrastructure exists or mark the phase blocked.

## Gate 2 — UI quality
For every user-facing screen and state, verify:
- clear visual hierarchy and one obvious primary action
- consistent spacing, typography, iconography, borders, radii, elevation, and design tokens
- semantic color usage; do not communicate meaning by color alone
- readable text and sufficient contrast
- loading, skeleton, empty, error, success, disabled, permission-denied, and offline states where applicable
- no layout jumps caused by late-loading content
- no clipped, overlapping, orphaned, or inaccessible controls
- touch targets are usable on compact screens
- keyboard/focus behavior works
- dialogs, sheets, menus, tooltips, and popovers have correct focus and dismissal behavior
- long content, localization, dynamic text, and large accessibility text do not break layouts
- destructive actions are distinguishable and appropriately confirmed
- visual clutter is removed; secondary information is progressively disclosed

## Gate 3 — Responsive and adaptive behavior
Verify actual behavior at relevant window sizes, not only named devices:
- compact phone
- standard/large phone
- tablet
- desktop
- landscape
- split-screen/resizable windows
- foldable cover/inner displays and posture changes when relevant

Do not merely scale a desktop layout down. Recompose navigation, density, columns, sheets, and detail views according to available space.

## Gate 4 — Accessibility
Where applicable, verify:
- semantic HTML/native semantics
- keyboard navigation
- visible focus
- logical focus order
- screen-reader labels and names
- headings/landmarks
- form labels and errors
- status announcements for important async changes
- reduced motion support
- sufficient contrast
- non-color-only status communication
- accessible names for icon-only actions
- captions/transcripts/alternative text where required

Use automated accessibility checks plus manual interaction checks.

## Gate 5 — Functional and integration verification
Test the complete flow:

user action → UI validation → auth/authz → API → backend → database → external service → response → UI state.

Cover:
- success
- validation failure
- unauthorized/forbidden
- duplicate submission
- timeout
- retry
- partial failure
- offline/reconnect
- interrupted journey
- stale data/concurrency
- rollback/recovery

## Gate 6 — Production code quality
Run the appropriate checks:
- typecheck
- lint
- unit/component tests
- integration/API tests
- database/migration tests
- E2E/browser/device tests
- accessibility checks
- visual regression where configured
- performance checks
- dependency/SCA/SAST/secret scans

Inspect warnings as well as errors. Do not suppress a warning merely to make a gate pass without documenting the reason.

## Gate 7 — Security
Verify:
- authentication and session handling
- authorization at backend boundaries
- organization/tenant isolation
- RLS/access policies where supported
- input validation and output handling
- file-upload controls
- rate limits
- CSRF/CORS/XSS/injection protections as applicable
- webhook signature verification
- idempotency for sensitive mutations
- secrets are not committed, logged, bundled, or exposed to the client

## Gate 8 — Runtime verification
Run the real application where possible. Verify the deployed or local runtime rather than relying only on source inspection.

For web apps inspect:
- browser console
- network failures
- hydration/runtime errors
- route transitions
- auth redirects
- API responses
- responsive layouts
- accessibility tree/interaction

For mobile apps inspect equivalent device/runtime behavior.

## Gate 9 — Documentation and state
Before locking:
- update `PROJECT_STATE.md`
- update `AGENT_HANDOFF.md`
- update `CHANGELOG.md`
- record bugs and fixes
- record test commands/results
- record known limitations and external blockers
- record the exact deployment/build identifier when available

## Gate 10 — Lock and checkpoint
A phase may be locked only when every applicable gate passes.

The lock record must contain:
- phase and scope
- requirements completed
- files/systems changed
- tests and results
- UI/accessibility verification
- security verification
- runtime evidence
- known limitations
- checkpoint commit SHA
- next phase

Create a checkpoint Git commit when Git is available and authorized.

## Failure policy
If any gate fails:

**Fix → re-test → re-verify.**

Do not move to the next phase and do not label the phase complete until the gate passes or a genuine external blocker is explicitly recorded.

If a later change breaks a locked phase, perform change-impact analysis, document the regression, re-run affected gates, and create a new checkpoint commit.

## Release candidate gate
Before production release, repeat the applicable gates across the complete application and verify:
- frontend build
- backend build/startup
- database migrations
- authentication
- authorization/tenant isolation
- critical user journeys
- payments/integrations
- notifications
- accessibility
- responsive/adaptive behavior
- security scans
- observability/health checks
- backup/restore and rollback readiness
- production configuration

A build passing alone is never a production certification.