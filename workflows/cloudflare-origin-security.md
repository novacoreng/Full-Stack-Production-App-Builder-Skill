# Cloudflare Edge, Origin Lockdown, and TLS

Apply only when the discovered production architecture actually uses Cloudflare and the control is compatible with the hosting model. Do not install certificates/firewall rules on the wrong component.

## Architecture first
Determine whether the application uses Workers/Pages, a conventional VPS/dedicated origin, managed/serverless hosting, or a combination. Identify DNS, public hostnames, origin reachability, management paths, health checks, provider callbacks and recovery access before changes.

## Conventional Cloudflare-proxied origin
Where a directly reachable origin is intended to be accessible only through Cloudflare:
- proxy relevant production DNS records;
- minimize origin-IP exposure;
- allow public HTTP(S) to origin only from Cloudflare's **current official** IPv4/IPv6 ranges when architecture permits;
- retrieve current ranges during implementation rather than hardcoding them in the skill;
- document range-update procedure;
- keep database/Redis/internal management ports private/non-public;
- preserve narrow management/monitoring/provider exceptions only when required.

Before firewall changes: export/backup current rules, document rollback, confirm console/out-of-band/recovery access, identify SSH/management requirements, and avoid an unrecoverable lockout. Prefer keys plus private/VPN/Zero Trust/tightly allowlisted management access where appropriate.

## TLS
Where applicable use strict origin validation (for Cloudflare, Full (strict), not Flexible). Origin CA certificates may be appropriate for Cloudflare-to-origin TLS on conventional proxied origins; their private keys stay only on the origin/approved secret store. Origin CA is not a public direct-client trust mechanism.

Use modern supported TLS and do not invent custom cryptography.

## Trusted client IP
Trust CF-Connecting-IP/X-Forwarded-For/X-Real-IP or equivalent proxy metadata only when the request is proven to arrive through the trusted proxy path. This affects rate limiting, bans, auditing and abuse detection.

## Defense in depth
Edge DDoS/WAF/bot/rate controls are additive and do not replace application rate limiting, authentication, authorization, validation, RLS/data controls or webhook authentication. Admin edge protection/Zero Trust may be an additional boundary; backend RBAC remains mandatory.

Origin restriction does not authenticate Paystack/KYC/other webhooks. Continue cryptographic provider verification.

## Verification
Test, where applicable:
- official hostname through Cloudflare → valid application;
- direct internet → origin HTTP/HTTPS → blocked;
- unauthorized origin ports → blocked;
- management/recovery path → works;
- health/monitoring → works;
- mobile/web/admin → works;
- provider callbacks/webhooks → work and remain cryptographically authenticated;
- database/internal ports → not publicly exposed.

If authenticated infrastructure access is unavailable, report **BLOCKED — INFRASTRUCTURE ACCESS REQUIRED** and provide exact required actions. Never claim implementation from configuration prose alone.
