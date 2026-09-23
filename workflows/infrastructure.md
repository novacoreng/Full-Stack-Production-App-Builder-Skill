# Infrastructure and Service Orchestration

Treat infrastructure as part of the application, not as a manual afterthought.

## 1. Service discovery

After the PRD and TRD are accepted, derive a Service Dependency Matrix from actual requirements. Do not enable or provision a provider merely because it is connected.

For each capability identify:
- capability (database, auth, storage, hosting, DNS, CDN/WAF, email/SMS, push, payments, queues, cron/jobs, analytics, observability, search, AI/model provider, object storage, backups)
- selected provider
- environment(s): development, test/staging, preview, production
- required resource
- required permissions
- secret/config names
- owner
- status
- verification evidence
- manual blocker, if any

## 2. GitHub-first repository handshake

Before implementation, when GitHub access is available:
1. Ask for or confirm the target repository URL.
2. Confirm owner/repository, default branch, working branch/strategy, and whether the agent is authorized to commit/push.
3. Inspect the repository before creating files.
4. Never assume an empty repository is safe to overwrite.
5. Create a project-state checkpoint before substantial changes.
6. Commit meaningful milestones as authorized.
7. Verify the remote branch after pushes.

If no repository exists and the user wants one created, state the exact repository name/visibility/organization required and use the connected GitHub capability if it supports creation. If repository creation is unavailable, give the smallest manual creation steps and pause only for that blocker.

## 3. Environment topology

Prefer explicit environments:
- local/development
- preview/PR
- test/staging
- production

Use separate credentials and data for each environment. Production credentials must never be used for ordinary development or automated tests.

Record:
- application URL
- API URL
- database/project identifier
- storage buckets
- notification credentials
- webhook endpoints
- DNS records
- deployment target
- secret names
- environment-variable scope
- rollback target

## 4. Provider provisioning

For every required connected provider:
1. Discover the exact resource required.
2. Check whether the connected tool can create/configure it.
3. Provision only what the PRD/TRD requires.
4. Configure security boundaries, access policies, regions, retention, webhooks, domains, and environment separation.
5. Capture resource identifiers and links in project state without exposing secret values.
6. Verify the resource with a safe health/configuration check.
7. Add the dependency to the Service Dependency Matrix.

Examples:
- Supabase: project/environment, schema migrations, auth providers, storage buckets, RLS/policies, database functions/triggers, webhooks, seed/test data, backups/restore configuration where supported.
- Vercel: project linkage, framework/build settings, preview/staging/production environments, environment variables, domains, deployment protection, build/runtime settings, observability.
- Cloudflare: DNS, zones/records, SSL/TLS, WAF/rules, Workers/Pages when used, redirects, caching, security settings.
- AWS: account/region selection, IAM least privilege, resources actually required, secret/config management, logs/metrics, backups, lifecycle policies, cost controls.
- OneSignal: app/project, platform credentials, environment separation, notification configuration, templates/segments only when required, consent and opt-out behavior.
- Payments/email/SMS/analytics/AI providers: provision only the capabilities required by the accepted product contract and verify webhook/signature/security configuration.

Provider-specific capabilities differ. Never claim a resource was created unless the connected tool returns evidence.

## 5. Missing resource or manual dependency rule

If the application requires a project, folder, bucket, database, domain, DNS record, API key, OAuth client, webhook, app registration, signing credential, billing account, or other resource that the connected tools cannot create:

- mark it BLOCKED in the matrix;
- explain exactly what must be created, where, and why;
- identify the minimum permission/role required;
- provide step-by-step instructions using the provider's current official documentation;
- do not invent a URL, ID, secret, credential, or success state;
- offer to work through the setup step by step;
- resume automated configuration and verification after the developer confirms completion.

Never silently replace a required integration with a mock and call the product complete.

## 6. Secrets and configuration

Use provider secret stores/environment-variable managers. Separate public configuration from secrets.

Rules:
- never write secret values into source control;
- never put credentials in README, screenshots, test fixtures, logs, analytics, or handoff documents;
- use different secrets per environment;
- prefer short-lived/rotatable credentials;
- record secret *names* and owners, not secret values;
- verify that client bundles contain only intentionally public values;
- scan Git history and current files for leaked credentials before release.

## 7. Infrastructure verification gate

Before an environment is considered configured, verify:
- resource exists;
- correct environment/project is targeted;
- application can authenticate using the intended mechanism;
- database migrations are applied;
- RLS/authz works;
- storage permissions work;
- webhooks reach the correct endpoint and signatures are verified;
- DNS/TLS resolves correctly where relevant;
- deployment succeeds;
- health/readiness checks pass;
- logs and alerts are receiving expected events;
- backup/restore capability is configured where required;
- rollback path is documented and tested where practical.

A failed mandatory check blocks the environment from being declared ready.
