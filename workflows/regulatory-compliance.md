# Regulatory, Platform, and Policy Applicability

This is an engineering applicability and implementation workflow, not legal advice.

## Applicability matrix

For each project identify:
- country/state/region of operation;
- user locations where material;
- user age groups;
- personal/sensitive data categories;
- payments/financial data;
- health data;
- education/children;
- employment/workforce data;
- location data;
- user-generated content;
- AI/model processing;
- advertising/marketing;
- regulated or safety-sensitive functionality;
- applicable app-store/platform distribution.

Then create a matrix:

| Area | Potential requirement | Why it may apply | Technical control | Owner-only action | Evidence | Status |
|---|---|---|---|---|---|---|

Do not state that a law applies without establishing jurisdiction and product facts.

## Privacy/data governance
Where applicable implement:
- data minimization;
- purpose limitation;
- collection notices;
- consent/preferences where required;
- access/export/correction/deletion workflows;
- retention and deletion jobs;
- account deletion;
- processor/subprocessor inventory;
- regional hosting/data-transfer considerations;
- privacy-safe test data;
- breach/incident escalation workflow.

## Consumer/commerce
Where applicable verify:
- pricing/fees/taxes;
- subscription renewal/cancellation;
- refunds/chargebacks;
- promotional claims;
- marketing consent and suppression;
- transactional versus marketing messaging;
- required disclosures.

## Payments
Keep payment-card handling within the intended provider's supported compliance boundary. Do not store card secrets unless the architecture explicitly requires it and the necessary controls are established. Verify webhook signatures and idempotency.

## Accessibility
For web products use WCAG 2.2 as an engineering baseline where appropriate. For mobile, use platform accessibility APIs and assistive-technology testing.

## App-store/platform rules
If distributed through an app store or platform:
- identify current review/distribution requirements;
- check permission declarations;
- privacy/data-safety declarations;
- billing/payment rules;
- account deletion requirements;
- age/content rating requirements;
- background activity/location/notification policies;
- developer-account requirements.

Record owner-only submissions or declarations separately from code changes.

## AI products
Where AI is used, assess:
- user disclosure where appropriate;
- privacy/data use;
- model/provider terms;
- prompt injection/tool abuse;
- sensitive data handling;
- output safety;
- human escalation;
- auditability;
- model/version changes;
- usage/cost controls;
- applicable AI-specific regulation/policy.

Never claim legal or regulatory compliance solely from code checks.
