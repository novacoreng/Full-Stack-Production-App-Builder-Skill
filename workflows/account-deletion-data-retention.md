# Account Deletion and Data Retention

If users can create accounts, evaluate whether the product/platform/jurisdiction requires an in-product account-deletion initiation path. Deactivation is not automatically equivalent to deletion.

A deletion workflow should, where applicable:
- re-authenticate or otherwise strongly verify the requester;
- clearly confirm intent and consequences;
- handle active orders/campaigns/subscriptions/wallets/payouts/disputes safely;
- revoke sessions/tokens;
- delete or anonymize data no longer required;
- preserve only data that has a documented legal/security/financial retention basis;
- document retained categories, purpose, retention period/trigger and eventual deletion/anonymization;
- propagate deletion/retention obligations to processors/providers where required;
- provide safe states for pending/manual review.

Do not erase immutable financial/security evidence merely to satisfy a deletion request when retention is legally required; do not retain everything indefinitely merely because deletion is complex.

Test request, cancellation if supported, session revocation, cross-service propagation, retained-vs-deleted data, re-registration behavior, and failure/retry paths.

Legal interpretation must be verified for the relevant jurisdiction and marked LEGAL REVIEW REQUIRED when unresolved.
