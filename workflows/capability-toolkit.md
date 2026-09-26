# Capability and Library Toolkit

The builder maintains a capability catalog, not a mandatory technology stack. Select a library, platform feature, provider, or custom implementation only when the accepted PRD/TRD requires it and the choice passes architecture, security, accessibility, performance, licensing, maintenance, and compatibility review.

## Data layer capabilities
- Typed/schema-defined entities with fields, enums, defaults, dates, relations, indexes, and constraints.
- CRUD and bulk operations: list/filter/get/create/update/delete/bulk create/update/updateMany/deleteMany where supported.
- Pagination, sorting, search, optimistic updates, caching, and invalidation.
- Realtime subscriptions/WebSockets where required.
- Row-Level Security or equivalent per-record authorization.
- Multi-tenant isolation and role-based writes.
- Auth-backed User entity, invitations, roles, and access controls.
- Migrations, seeds, audit records, retention, deletion, export, archive, and restore.

## Backend logic capabilities
- Server-side HTTP handlers for external APIs, webhooks, and privileged operations.
- Secure server-side secrets and service identities.
- Reusable shared/domain modules; avoid duplicated business logic.
- Scheduled jobs, event triggers, queues, workflows, conditions, delays, branching, parallel paths, retries, idempotency, and failure recovery.

## Integrations
Support OAuth, API keys, SDKs, REST, GraphQL, webhooks, and provider-specific connectors where appropriate. Examples include Google Workspace services, Slack, GitHub, Notion, Salesforce, HubSpot, Linear, Jira, Dropbox, Airtable, Microsoft services, payment providers, messaging providers, AI providers, storage, analytics, and observability.

For every integration document purpose, auth mode, scopes, environment, data direction, webhook behavior, secret names, failure behavior, rate limits, and verification evidence.

## AI capabilities
- In-app agents with configuration, permissions, entity/data access, backend tools, and workflows.
- Tool-using/code agents.
- LLM orchestration with model selection, structured JSON/schema output, file context, retrieval/search, and web search where appropriate.
- Image generation, speech/TTS, transcription, and other model capabilities when required.
- Scheduled/event-triggered agents and channel delivery such as WhatsApp/Telegram where supported.
- Human approval gates, output validation, prompt-injection/tool-abuse defenses, model fallback, evaluation, cost controls, auditability, and version tracking.

## Authentication and access
Support the authentication provider and methods selected by the architecture: email/password, OTP, Google, Microsoft, Facebook, Apple, enterprise SSO, MFA, recovery, session management, protected routes, RBAC, ABAC where justified, organizations, teams, and invitations.

Authentication is identity; authorization must be enforced at backend/data boundaries as well as in the UI.

## Communication
- Transactional email with attachments/templates/sender identity.
- Marketing email with consent/suppression/unsubscribe controls where applicable.
- Native push notifications.
- In-app notification center and notification history.
- WhatsApp/Telegram/SMS where requirements and providers support them.
- Localization, delivery status, retries, rate limits, and deep links.

## Realtime and collaboration
Use WebSockets/realtime infrastructure only when required. Capabilities include live entity sync, chat, presence, rooms, typing indicators, collaborative editing, live cursors, optimistic updates, conflict handling, and reconnect/replay behavior.

## Observability and operations
- Analytics/custom events.
- Runtime error tracking and structured logs.
- Metrics/traces and alerts.
- Audit logs for security/business actions.
- API monitoring and release tracking.
- Security scans.
- Optional API/SDK exposure for third parties and MCP server/tool exposure for AI clients.
- Session recordings only when justified, with consent/privacy controls and sensitive-field masking.

## Deployment/platform capabilities
- Preview and production hosting.
- Native iOS/Android builds where mobile is required.
- Custom domains, TLS, DNS, redirects.
- CI/CD, environment separation, secrets, migrations, rollback, release artifacts, versioning, and OTA updates where appropriate.
- GitHub synchronization and repository workflows.
- App-store release preparation and platform-specific requirements.

## Ready-to-use UI/library patterns
These are optional candidates, not mandatory dependencies. Before adding one, check current compatibility, bundle/runtime impact, accessibility support, maintenance health, licensing, platform constraints, and whether native/browser primitives are sufficient.

### Rich text
- `react-quill-new` for WYSIWYG editing when a rich editor is required.

### 3D/WebGL
- `three.js` for 3D models, scenes, visualization, games, and WebGL experiences.

### Maps/geolocation
- `react-leaflet` for interactive maps, markers, routes, and map-based web experiences.
- For native mobile mapping, evaluate the appropriate platform/native map implementation instead of forcing a web map library.

### Drag and drop
- `@hello-pangea/dnd` for sortable lists, kanban boards, and drag-and-drop workflows where appropriate.

### Data fetching/caching
- `@tanstack/react-query` for server-state fetching, caching, retries, invalidation, optimistic updates, and query synchronization when the architecture calls for it.

### Forms and validation
- `react-hook-form` for form state/performance.
- `Zod` for runtime/schema validation and shared contracts where appropriate.

### Date/time
- `date-fns` or another maintained date/time solution selected by project requirements. Avoid introducing both `date-fns` and `moment` without a documented reason; prefer one consistent date/time strategy.

### PDF/export/screenshots
- `jsPDF` + `html2canvas` for client-side document/image export when suitable.
- For authoritative receipts, invoices, or sensitive documents, evaluate server-side PDF generation and data integrity requirements.

### Celebration/micro-interactions
- `canvas-confetti` for appropriate milestone celebration; respect reduced-motion preferences and do not use it in contexts where motion is distracting or inappropriate.

### Command palettes
- `cmdk` for keyboard/search command palettes where the product benefits from rapid actions.

### Bottom sheets/drawers
- `vaul` for web bottom sheets/drawers where compatible.
- On native mobile, prefer platform-native sheet behavior or the project's native-compatible component library when appropriate.

### Carousels
- `embla-carousel-react` for controlled carousels/sliders. Include keyboard, touch, focus, reduced-motion, and screen-reader behavior in verification.

### Resizable panels
- `react-resizable-panels` for desktop/web split views where resizing is part of the product model.

### OTP inputs
- `input-otp` for web OTP/code-entry UX. Verify paste, autofill, keyboard, screen reader, error, and timeout behavior.

### Themes
- `next-themes` for theme switching in compatible Next.js/web architectures. Do not introduce it into a non-Next architecture without a reason.

### Date pickers
- `react-day-picker` for web calendar/date selection where appropriate.

### Toasts
- `sonner` or an appropriate Radix-based toast system for web notifications. Verify focus, announcements, timing, dismissal, and non-color-only status communication.

## Platform/business features
Where requirements call for them, evaluate:
- Stripe Checkout/subscriptions/one-time payments or another regionally appropriate payment provider.
- Advertising/campaign management integrations where applicable.
- CSV, Excel, JSON import with validation, preview, mapping, deduplication, rollback/error reporting, and permission checks.
- Private file uploads using signed URLs and permission-gated access.
- Public files only when permanent public access is intentional.
- App MCP server/API exposure to AI clients.
- App cloning with tenant/security isolation and explicit ownership semantics.
- Workspace/team groups, invitations, roles, and permissions.
- Session recordings with privacy controls.
- Security headers and automated security scanning.
- Custom domains, redirects, TLS/DNS verification.
- Two-way GitHub repository synchronization where supported and authorized.

## Workflow and automation capabilities
Implement only when required:
- visual or code-defined multi-step workflows;
- event/scheduled triggers;
- conditions;
- delays;
- branching;
- parallel paths;
- scheduled/cron jobs;
- event-driven entity/user actions;
- retries and failure paths;
- idempotency and replay.

Every automation must define its trigger, inputs, permissions, side effects, failure behavior, observability, retry policy, and cancellation/disable mechanism.

## Capability selection gate
Before adding any library or platform feature:
1. Map it to a requirement or technical need.
2. Check whether an existing dependency already solves the problem.
3. Compare native/platform/browser primitives and viable alternatives.
4. Check current compatibility with the selected framework/platform.
5. Check accessibility and responsive/adaptive behavior.
6. Check security/privacy implications.
7. Check performance/bundle/runtime impact.
8. Check licensing and maintenance risk.
9. Add the dependency only when justified.
10. Test and document it.

The goal is **capability coverage without dependency bloat**.