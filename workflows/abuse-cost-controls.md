# Abuse, Bot, and Provider-Cost Controls

Treat cost exhaustion as a security concern whenever a public or authenticated action can generate third-party or infrastructure spend.

## Inventory billable actions
Identify SMS/OTP, email, KYC/identity checks, bank verification, payment-provider calls, storage/bandwidth/uploads, AI/model calls, push/provider operations, search/geocoding, and other metered services.

For each record provider, endpoint/event, cost dimension, attacker-controlled inputs, quota/budget, telemetry, alert threshold, fail/degrade behavior, and owner.

## Layered controls
Do not use one universal rate limit. Select endpoint-specific controls using appropriate IP, authenticated user, account, normalized phone/email, device/risk signal, endpoint and time window dimensions.

High-abuse flows normally require some combination of burst limits, sustained/daily quotas, resend cooldowns, attempt limits, provider budgets, anomaly alerts, temporary blocks and escalation. Avoid lockouts that make shared carrier/NAT/VPN addresses a single source of truth.

Evaluate risk-based CAPTCHA/bot challenges for public abuse-prone flows such as signup, OTP/recovery and suspicious high-volume forms. Do not challenge every legitimate user by default.

Return safe 429/abuse responses without exposing account existence or internal detection rules.

## Verification
Attack-test quota boundaries in authorized non-production environments. Verify that limits prevent unbounded provider spend, legitimate recovery remains possible, telemetry/alerts fire, and bypasses through alternate identifiers/routes are not available.
