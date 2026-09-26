# Capability Analysis Workflow

The builder must analyze required capabilities before selecting implementation technologies. This workflow is architecture-neutral and does not force a framework, backend, database, authentication provider, or hosting platform.

## Capability domains

Evaluate only domains relevant to the product:

- frontend/UI
- data/entities/CRUD
- database and migrations
- backend/domain logic
- authentication/authorization
- realtime/collaboration
- integrations/OAuth/APIs/webhooks
- files/media/import/export
- payments/subscriptions
- communications/email/SMS/push/in-app
- AI/models/agents/tools
- workflows/automation/scheduling
- analytics/observability/audit
- public APIs/SDKs/MCP
- deployment/infrastructure
- security/privacy/accessibility

## Implementation process

1. Extract capability requirements from the accepted PRD/TRD.
2. Check the existing repository for capabilities already implemented.
3. Determine whether native/platform functionality is sufficient.
4. Evaluate suitable libraries/services/providers.
5. Compare material alternatives.
6. Record the decision in a Dependency Decision Record when a third-party dependency is introduced.
7. Implement the smallest appropriate solution.
8. Test the capability in its real runtime context.
9. Verify security, accessibility, performance, failure, and lifecycle behavior where relevant.
10. Record the result in the Capability Coverage Matrix.

## Capability coverage gate

Each required capability must map to:

`Requirement → Architecture → Implementation → Integration → Test → Verification Evidence → Release`

A capability is not complete merely because its library was installed or its UI exists.

## External services

For services such as payment, OAuth, ads, notification, analytics, storage, AI, MCP, or external APIs:

- use sandbox/test environments when available;
- keep credentials server-side;
- configure webhooks and signature verification where applicable;
- implement retries/idempotency where needed;
- document provider limits and failure modes;
- verify the actual integration at runtime;
- never invent a successful connection.

## Optional library policy

Libraries in `references/capability-library-registry.md` are suggestions only. The agent may select an alternative when the project's architecture or requirements make another implementation more appropriate.

Do not install multiple libraries that solve the same problem without documenting the reason.
