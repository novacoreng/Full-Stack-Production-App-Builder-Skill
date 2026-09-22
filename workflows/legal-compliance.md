# Legal, Privacy & Compliance Audit Workflow

Use this workflow during discovery, architecture, implementation, debugging, and the final production audit. It is based on the supplied September 2026 "The Prompt" legal-exposure checklist and preserves its six audit areas, while treating applicability as jurisdiction- and product-dependent. This is an engineering audit workflow, not legal advice.

## Required audit method

Inspect the actual repository. For every item:

1. Find where it applies, or prove that it does not apply.
2. Show evidence from code/configuration/data flows.
3. Make applicable engineering fixes directly.
4. Test the fix.
5. Document what the project owner still must do externally.
6. Do not mark the item resolved merely because a policy page exists.

## Six audit areas

### 1. Age gating / child privacy
Inspect every account-creation path:
- sign-up forms
- OAuth callbacks
- magic links
- mobile onboarding
- alternative account-creation APIs

Also inspect unauthenticated forms collecting personal data such as names, emails, or photos.

If applicable requirements require an age gate:
- enforce it server-side before account creation
- reject prohibited account creation
- avoid retaining prohibited data from the rejected attempt
- test every account-creation path

Do not assume a universal age threshold; determine the applicable rule from jurisdiction and product context.

### 2. Third-party fonts and remote resources
Search for:
- fonts.googleapis.com
- fonts.gstatic.com
- Typekit
- jsDelivr
- unpkg
- cdnjs
- other third-party fonts/CSS/JS loaded at runtime

Prefer self-hosting where appropriate. For resources that must remain, document:
- provider
- resource
- purpose
- data exposed
- whether consent is required
- alternative considered

### 3. Analytics and session replay
Inventory:
- PostHog
- Hotjar
- FullStory
- LogRocket
- Microsoft Clarity
- Mixpanel
- Sentry Replay
- heatmaps
- keystroke logging
- rage-click recording
- equivalent tools

Where applicable:
- keep session replay off by default
- require explicit, revocable consent before recording
- persist the consent choice
- mask text inputs
- never record passwords, payment secrets, or prohibited sensitive fields
- verify SDK initialization respects consent

### 4. Commercial email
Separate commercial/marketing mail from transactional mail.

For applicable marketing messages, inspect:
- one-click unsubscribe
- suppression list
- sender/physical address requirements
- List-Unsubscribe
- List-Unsubscribe-Post
- suppression checks before sending
- unsubscribe propagation
- transactional-email classification

Do not assume a universal statutory deadline; verify the applicable jurisdiction and current rule.

### 5. Subscriptions and automatic renewal
Inspect:
- pricing pages
- checkout
- subscribe buttons
- Stripe/Paddle/custom billing
- free trials
- renewal events
- cancellation
- refund flows

Where applicable, verify:
- price
- renewal interval
- automatic-renewal disclosure
- cancellation method
- affirmative consent
- cancellation path that is accessible
- confirmation email
- pre-charge reminder for applicable trials
- webhook/idempotency/state handling

### 6. User uploads and copyright
Inspect uploads for:
- avatars
- images
- posts
- files
- attachments
- generated content
- other user-submitted works

Where applicable:
- provide copyright/takedown policy
- provide notice contact information
- add a copyright-reporting path near user content
- define repeat-infringer handling
- document external designated-agent requirements separately where a US DMCA safe-harbor strategy applies

Code cannot itself prove that an external registration has been completed.

## Additional privacy/security checks

Inspect:
- privacy policy
- terms
- cookie/consent policy
- footer links
- signup links
- actual third-party processors used by the code
- tracking before consent
- stored/revocable consent state
- secrets in client bundles
- API keys in client bundles
- personal data in logs
- sensitive data in analytics/error reports
- source maps and public artifacts

## Required output

For every numbered item:

### Found
What was found in the repository, with evidence.

### Changed
What code/configuration/documentation was changed.

### You still need to
Actions requiring the project owner, lawyer, service provider, regulator, registration authority, or other external party.

### Applicability
Jurisdiction, product, data, and business-model assumptions; unresolved questions must remain visible.

### Verification
Tests and evidence proving the implemented control works.

Then provide a summary table:

| Area | Applies? | Found | Changed | Owner action | Verification | Status |
|---|---|---|---|---|---|---|

## Important boundary

This workflow does not provide legal advice. Penalty figures, statutory thresholds, deadlines, registration requirements, and applicability vary by jurisdiction and time. When those details affect implementation, verify them against authoritative current sources and record the jurisdiction and effective date. Have qualified legal counsel review material legal conclusions before launch.
