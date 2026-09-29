# Production Debugging Methodology

## Purpose

Debug the entire system, not only the file where an error appears. Trace failures across UI, state, API, authentication, backend logic, database, integrations, infrastructure, build tooling, deployment, and runtime.

## Mandatory debugging loop

**Reproduce → Isolate → Trace → Identify Root Cause → Fix → Test → Build → Deploy → Verify → Regression Test → Commit.**

Never describe a problem as fully fixed solely because the source file changed.

## Verification states

Keep these states distinct:

1. Code fixed
2. Local test passed
3. Production build passed
4. Deployment verified
5. Runtime/environment verified

Do not claim a higher state without evidence.

## Deep Debug Mode

When normal diagnosis is insufficient, trace the failure line-by-line and boundary-by-boundary:

```text
File → Line → Function/Component → Inputs → State → API Call → Response → Database Operation → Error Propagation → UI Result
```

Inspect the root cause before applying a patch. Avoid symptom-only fixes and repeated speculative changes.

## Frontend/backend debugging

For integration failures verify:
- frontend request shape;
- API route/function;
- authentication/session;
- authorization/RLS;
- server validation;
- database query/mutation;
- response shape/types;
- error handling;
- loading/empty/error/success UI;
- environment variables;
- external provider response.

Nullable and asynchronous data must be handled safely; do not assume objects such as `data.user` exist before loading/authorization state is known.

## Build and deployment debugging

For web/Next.js/Vercel or equivalent deployments verify:

```text
Install → Type Check → Lint → Compile → Build → Prerender/Route Generation → Environment Validation → Deployment → Runtime Verification
```

For monorepos additionally verify:
- workspace/package manager detection;
- root dependencies;
- application-directory dependencies;
- framework detection;
- correct build command;
- correct output directory/artifact;
- deployment project root;
- generated production artifact.

A deployment that finishes quickly without executing the intended application build is not considered successful.

## Environment-variable debugging

Compare required environment variables across local, preview, staging, and production. Check names, values/references, scope, server/client exposure, URLs, provider credentials, and accidental secret exposure. Never place secrets in source code or Git history.

## Database and migration debugging

When database behavior fails, inspect:
- schema;
- migration history/order;
- duplicate/conflicting migrations;
- actual target database state;
- indexes/constraints;
- RLS/policies;
- seed/test data;
- application queries and mutations.

Do not assume a migration file existing in the repository means it was successfully applied to the target environment.

## Regression prevention

After every fix:
- rerun the failing test;
- run relevant neighboring tests;
- run type/build checks;
- verify the affected process flow;
- inspect for regressions;
- update the phase record;
- commit after the phase verification gate passes.

## Evidence rule

Record the error, reproduction path, root cause, changed files, tests run, build/deployment evidence, and final verification state. Never claim Vercel, GitHub, database, provider, or production success without direct evidence.
