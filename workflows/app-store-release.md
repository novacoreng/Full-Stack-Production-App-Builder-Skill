# App Store and Distribution Release Audit

Use current official platform requirements during final release preparation. Store/policy rules change; never rely on remembered myths or unverified rejection statistics.

For each target distribution platform verify, as applicable:
- application completeness and no unintended placeholder/dead functionality;
- accurate screenshots/metadata that represent real implemented functionality;
- working support/privacy/legal URLs;
- review access/instructions or safe review credentials/mechanism;
- account creation and deletion requirements;
- privacy/data-safety disclosures;
- permission declarations and contextual purpose strings;
- authentication/provider requirements such as Sign in with Apple when applicable;
- payments, donations/fundraising, digital-goods and financial-service rules based on the actual transaction category;
- KYC/financial documentation where applicable;
- content moderation/user-generated-content requirements;
- production API availability and real-device testing;
- age/content ratings and other required declarations.

Do not assume every payment requires store IAP. Classify the transaction (digital goods/features, physical goods/services, donations/fundraising, person-to-person transfers, wallet funding, fees, etc.) and verify the current official rule before changing payment architecture.

Permission purpose strings should explain what is requested, why the product needs it and the user-facing function/benefit. Do not request unused permissions.

Do not add AI disclosures merely because AI tools helped develop the app. Assess disclosure/transparency/moderation requirements when the shipped product itself generates or materially transforms user-visible content using AI.

Separate code-verifiable items from owner-only submissions/declarations. Use PASS / FAIL / FIXED / BLOCKED / NOT IMPLEMENTED / NOT TESTED / NOT APPLICABLE and attach evidence.
