# Tool Orchestration

Treat connected tools as capabilities with explicit permissions and evidence, not as magic infrastructure.

## Order of operations

1. Confirm project identity and accepted PRD/TRD.
2. Ask for or confirm the target GitHub repository URL.
3. Inspect the repository and establish the working branch/checkpoint strategy.
4. Build the Service Dependency Matrix from actual requirements.
5. Determine which connected providers are actually required.
6. Configure/provision supported resources.
7. Mark unsupported/manual resources as blockers and guide the developer through them.
8. Verify each resource before relying on it.
9. Implement the application against the verified resources.
10. Run post-build test-admin verification where an admin role exists.
11. Run production-readiness gates and verify deployment evidence.

## Provider selection

Typical provider capabilities may include:
- GitHub — source, branches, commits, CI/CD
- Supabase — PostgreSQL, Auth, Storage, RLS, functions/webhooks
- Vercel — web deployment, preview/production environments, domains and runtime configuration
- Cloudflare — DNS, CDN/WAF, Workers/Pages and edge controls
- AWS — infrastructure, IAM, storage, compute, queues, secrets, monitoring and other cloud services
- OneSignal — push notifications and messaging
- payment providers — checkout, payment verification, webhooks, refunds
- email/SMS providers — transactional/marketing delivery and suppression
- Figma — design workflows
- browser/device tooling — runtime verification

Only use a provider when it satisfies an accepted requirement or architectural decision.

## Missing capability protocol

When a required action is not supported by the connected tool:
- do not pretend it happened;
- identify the exact missing resource/action;
- state the required provider and minimum permission;
- provide step-by-step instructions from the current official provider documentation;
- mark the matrix item BLOCKED;
- offer to continue step by step;
- resume automated setup and verification once the developer confirms.

## Secrets

Never expose or commit secret values. Use provider secret stores or environment-variable managers. Record secret names and scopes, not values.

## Evidence

For every external action record enough evidence to prove:
- what resource was changed;
- which environment;
- when/which commit;
- resulting resource ID/link where safe;
- verification result.

Never claim an external resource was created, deployed, or configured without tool evidence.
