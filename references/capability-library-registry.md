# Capability & Library Registry

This registry is a capability catalogue, not a mandatory dependency list. The builder must select technologies based on the accepted PRD/TRD, architecture, existing codebase, security, accessibility, performance, maintenance, licensing, and product requirements.

## UI / Frontend libraries

| Capability | Optional library | Use when |
|---|---|---|
| Rich text editing | `react-quill-new` | WYSIWYG editing is required and the selected web architecture is compatible |
| 3D / WebGL | `three.js` | Interactive 3D, models, scenes, visualization, or games are required |
| Maps / geolocation | `react-leaflet` | Interactive maps are required in a compatible React web application |
| Drag and drop | `@hello-pangea/dnd` | Sortable lists, boards, or Kanban interactions are required |
| Data fetching / caching | `@tanstack/react-query` | Server-state caching, retries, invalidation, optimistic updates, or query orchestration are useful |
| Forms / validation | `react-hook-form` + Zod | Complex forms and typed runtime validation are required |
| Date handling | `date-fns` / `moment` | Date/time manipulation is required; select one appropriate library rather than adding overlapping dependencies |
| PDF generation | `jsPDF` + `html2canvas` | Client-side PDF/export workflows are appropriate |
| DOM screenshots | `html2canvas` | Capturing compatible web DOM content is required |
| Celebration effects | `canvas-confetti` | A milestone/celebration interaction materially improves the experience |
| Command palette | `cmdk` | Keyboard/quick-action command search is useful |
| Bottom sheets / drawers | `vaul` | Mobile-style sheets are required in a compatible web application |
| Carousels | `embla-carousel-react` | A carousel is actually needed |
| Resizable panels | `react-resizable-panels` | Split/resizable desktop or workspace layouts are required |
| OTP input | `input-otp` | Code/OTP entry needs a dedicated accessible input pattern |
| Dark mode | `next-themes` | Theme switching is required in a compatible Next.js/web architecture |
| Date picker | `react-day-picker` | Calendar/date selection is required |
| Toasts | `sonner` / Radix Toast | Non-blocking feedback notifications are required |

## Platform / backend capabilities

The builder may evaluate and use, where justified:

- Stripe Checkout, subscriptions, and one-time payments
- Google Ads campaign creation/management where the product requires it and provider access permits it
- CSV, Excel, and JSON import pipelines
- private file uploads with signed, permission-gated URLs
- public file uploads with intentionally world-readable URLs
- application MCP servers exposing approved data/functions to AI clients
- application cloning/duplication
- workspace/team groups and role assignment
- session recordings and replay
- security headers and automated security scanning
- custom domains, TLS, redirects, and DNS
- GitHub two-way repository synchronization

For every external platform capability, verify provider terms, current APIs, scopes, permissions, environment separation, rate limits, webhook behavior, and secret handling.

## Workflow / automation capabilities

Support when required:

- event-triggered workflows
- scheduled/cron workflows
- entity-change triggers
- user-action triggers
- webhook triggers
- conditions
- branching
- parallel paths
- delays
- retries and bounded backoff
- failure/dead-letter handling
- human approval steps
- idempotency
- workflow audit history

## Selection rule

**Availability is not a reason to install a dependency.** Before adding a library or platform capability, confirm:

1. the product requirement that needs it;
2. architecture compatibility;
3. whether existing project capabilities already solve the requirement;
4. security/privacy implications;
5. accessibility implications;
6. bundle/runtime/performance impact;
7. maintenance and ecosystem health;
8. licensing implications;
9. version compatibility;
10. test and verification strategy.

Avoid overlapping libraries unless there is a documented reason. Prefer the smallest reliable dependency set that satisfies the requirements.
