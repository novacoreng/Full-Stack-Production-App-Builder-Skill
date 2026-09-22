# WorkSync Application Source

This directory contains the WorkSync application source associated with the production builder project.

## Source package

The complete Phase 37 application source is packaged as:

- WorkSync Phase 37 archive: `worksync-phase37.zip`
- SHA-256: `86754e57484fe85fa8629ace786251b65d98eb682c94295ffae44240b7d9813b`

The application consists of:

- `backend/` — Fastify + TypeScript API
- `frontend/` — Next.js 16 + React application
- `supabase/migrations/` — cumulative database schema and RLS migrations
- `scripts/` — project validation and QA tooling

The canonical application package is maintained from the Phase 37 release archive so the exact tested source tree can be reproduced without silently omitting files.

## Build loop

Build → Test → Verify → Fix → Lock → Move to next phase.

## Important

Environment files contain placeholders only. Supabase service-role credentials, Paystack secrets, AI provider secrets, communication-provider credentials, and worker secrets must never be committed.
