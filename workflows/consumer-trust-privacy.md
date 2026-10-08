# Consumer Trust, Privacy and Anti-Deception Release Gate

Evaluate these controls during PRD, TRD, app flow, design brief, data schema, documentation plan, implementation, QA and release. Applicability depends on the product, jurisdiction and current platform rules. Legal counsel must review uncertain requirements. This workflow reduces risk but cannot guarantee immunity from litigation.

## Prohibited or gated patterns
1. **No unsubscribe:** Marketing email/SMS/push must provide appropriate opt-out or unsubscribe mechanisms, honor requests promptly, and distinguish transactional/service messages from marketing. Track consent/preferences and suppression across providers.
2. **Leaky analytics:** No undisclosed or excessive collection/sharing of personal, sensitive, financial, health, biometric, children's or message data. Inventory SDKs/events, minimize payloads, redact identifiers, configure retention, consent/legal basis and processor controls, and verify privacy disclosures.
3. **Spam texts:** Do not send unsolicited promotional SMS/WhatsApp/email/push. Require appropriate permission/lawful basis, consent evidence where needed, frequency caps, quiet hours where required, sender identification, unsubscribe and provider compliance.
4. **Face scans/biometrics:** Do not collect face templates, liveness data, voiceprints or other biometrics by default. Require demonstrated necessity, lawful basis and any required explicit consent, purpose limitation, retention/deletion, strong protection, vetted processors, and alternative/manual review where appropriate. Never reuse biometric data for unrelated training/marketing.
5. **No privacy policy:** Products collecting personal information must have an accurate, accessible privacy notice describing collection, purpose, sharing, processors, retention, rights, contact and deletion. Verify notice matches actual SDKs/APIs/data flows and current jurisdiction/store requirements.
6. **Kids' data:** Determine whether minors may use the product or are likely to be affected. Apply age-appropriate design, data minimization, parental authorization where required, restrictions on profiling/ads, safe defaults, content protections, deletion/retention and relevant child-privacy laws. Do not assert universal age thresholds.
7. **Fake reviews:** Never fabricate, buy or misrepresent reviews, testimonials, ratings, endorsements, user counts or engagement. Disclose incentivized/paid relationships where required; moderate abuse without suppressing genuine criticism deceptively.
8. **Hard-to-cancel subscriptions:** Clearly disclose price, renewal, trial conversion and material terms before enrollment. Obtain required affirmative consent. Provide accessible cancellation consistent with applicable laws/platform rules; do not use obstruction, hidden cancellation, misleading buttons or unnecessary support-only hurdles. Confirm cancellation and billing status.
9. **Fake AI claims and likes:** Do not claim AI capabilities, accuracy, autonomy, safety, human review or outcomes that are not implemented and evidenced. Never generate fake likes, followers, donations, social proof, testimonials, endorsements or activity to deceive users. Disclose AI-generated/synthetic interactions or content when applicable.

## Mandatory verification
- Map each applicable risk to PRD requirements, data schema, UI flow, backend enforcement, provider configuration, tests and release evidence.
- Test unsubscribe and suppression end-to-end, including provider/webhook sync.
- Inspect actual analytics events, network traffic, SDK settings and logs for data leakage.
- Test messaging consent, opt-out, quotas and marketing/transactional separation.
- Audit biometric capture, vendor terms, storage, deletion and consent/alternative flows.
- Verify privacy notice against the actual data inventory and deployed product.
- Test age-related safeguards using safe test personas without real children's data.
- Review reviews/social metrics/AI claims against verifiable source data and disclosures.
- Test subscription signup, price/renewal disclosure, cancellation, confirmation, and post-cancellation charges in sandbox.
- Recheck current official laws/regulator guidance and app-store policies before release; mark uncertain legal interpretation LEGAL REVIEW REQUIRED.

## Release blocking
An applicable control with deceptive behavior, unlawful marketing, unauthorized sensitive-data collection, fabricated social proof, materially misleading AI claims, missing required privacy notice, or obstructed cancellation is a release blocker. Record PASS / FAIL / BLOCKED / NOT TESTED / NOT APPLICABLE with evidence. Never claim 'lawsuit-proof' or 'legally compliant' without appropriate review and evidence.
