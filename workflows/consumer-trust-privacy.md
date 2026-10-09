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

## Mandatory launch checklist: legal, consent, accessibility and transparency

Evaluate every item during planning, implementation, runtime QA and release. Record PASS / FAIL / BLOCKED / NOT TESTED / NOT APPLICABLE, evidence, owner and required remediation. A policy page alone does not prove the control works.

1. **Privacy policy:** Publish an accessible, accurate, current notice that matches actual collection, processors, SDKs, analytics, retention, transfers and rights. Link it at relevant collection points and app/store surfaces.
2. **Authentic reviews:** Remove fabricated, purchased, misleading or undisclosed incentivized reviews and fake engagement; verify published testimonials/metrics against real evidence.
3. **Terms of service:** Provide review-ready terms appropriate to the product, transaction model and jurisdiction; link at meaningful signup/contracting points, record acceptance where required and version changes.
4. **Unsupported claims:** Remove or substantiate claims about AI, results, security, health, financial outcomes, user counts, ratings, endorsements, certifications and product features.
5. **Refund policy:** Publish accurate refund/return/cancellation rules, eligibility, timing, exceptions and contact process as applicable; ensure checkout and support behavior match the policy. Do not invent refund rights or waive mandatory protections.
6. **Accessibility alt text:** Give informative images meaningful alternatives; mark purely decorative images appropriately; provide accessible names for icon-only actions and media alternatives where needed.
7. **Cookie/tracking policy:** Disclose cookies and similar identifiers, purposes, durations and providers where applicable; distinguish essential from optional tracking.
8. **Color contrast:** Test text, controls, focus indicators and important non-text UI states against applicable WCAG requirements; fix failures without changing approved branding unnecessarily.
9. **Cookie consent banner/preferences:** Where consent is required, obtain valid granular consent before optional tracking starts, allow refusal as easily as acceptance where required, persist and honor choices, and provide withdrawal/change controls. Do not add a meaningless banner where consent is not required.
10. **Keyboard navigation:** Test complete keyboard-only journeys, logical focus order, visible focus, dialogs, menus, form errors, skip/navigation mechanisms and no keyboard traps.
11. **Form consents:** Audit checkboxes, toggles and notices; avoid prechecked optional marketing consent, separate distinct purposes, log consent evidence where required, and ensure withdrawal propagates.
12. **Business details:** Provide accurate legal/operator identity, business contact/support channels and required registration/address details appropriate to jurisdiction and commerce model; never fabricate addresses or registrations.
13. **Data minimization:** Collect only necessary data; justify each field, SDK event, permission and retention period. Avoid hidden analytics payloads and unnecessary sensitive identifiers.
14. **Children's data:** Determine age-related applicability and verify age-appropriate consent/parental authorization where required, safe defaults, limited tracking, restricted ads and deletion rights. No universal age threshold is assumed.
15. **Third-party SDK audit:** Inventory analytics, ads, crash reporting, session replay, social login, payment, KYC and other SDKs; inspect data sent, SDK initialization, consent gating, processors, retention, permissions, transfers, security and version risks. Remove unnecessary SDKs.
16. **Email unsubscribe:** Include functional unsubscribe/opt-out links or required mechanisms in marketing email; verify suppression, provider synchronization and separation from transactional notices.
17. **Dark patterns:** Reject manipulative consent prompts, misleading urgency/scarcity, disguised ads, forced continuity, hidden cancellation, confusing toggles, obstructive account deletion and deceptive pricing.
18. **Fonts and images licensing:** Record the source, license, permitted uses, attribution and distribution rights for fonts, stock images, icons, video and other assets; do not assume internet availability grants a commercial license. Do not redistribute restricted font files.
19. **Hidden fees:** Disclose mandatory charges, platform fees, renewal terms, taxes and other material costs before final commitment; reconcile UI totals with server/provider charges.
20. **Data deletion request:** Provide an accessible request path and authenticated processing workflow where applicable; verify identity, revoke sessions as needed, handle processor deletion, document lawful retention exceptions and test completion.

### Acceptance and regression evidence
- Inspect deployed legal pages, footer/signup/checkout links and mobile/store links.
- Exercise cookie consent accept/reject/change and confirm actual network/SDK behavior.
- Inspect analytics network events and consent state before/after choices.
- Run automated accessibility checks **and** manual keyboard/screen-reader checks where feasible; automated checks alone are insufficient.
- Test marketing opt-out, consent withdrawal, deletion requests and refund/cancellation flows end-to-end.
- Verify real asset licenses, business identity, fee calculations, published reviews and claims with supporting records.
- Record legal review required for jurisdiction-specific interpretation and block release on unresolved applicable material violations.
