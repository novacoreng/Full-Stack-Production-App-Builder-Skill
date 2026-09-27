# Test Personas & Credentials

## Build environment
- Environment: development / test / preview / staging
- Test auth bypass enabled: yes/no
- Production bypass disabled: yes/no

## Test personas

| Persona | Login identifier | Role | OTP bypass | Intended tests | Status |
|---|---|---|---|---|---|
| Test Admin | Securely supplied at handoff | Admin | Non-production only | Admin/RBAC/backend | |
| Test User | Securely supplied at handoff | User | Non-production only | Core user flows | |
| Test Moderator | Securely supplied at handoff | Moderator | Non-production only | Moderation | |
| Test Organization | Securely supplied at handoff | Organization | Non-production only | Organization flows | |
| Test Creator | Securely supplied at handoff | Creator | Non-production only | Creator/provider flows | |
| Test Guest | N/A | Guest | N/A | Public/unauthenticated flows | |

## Credential handling

Do not put passwords, tokens, OTP secrets, recovery codes, or private keys in this document or GitHub. Record only the secure location/reference used to deliver them.

## Production safety checklist

- [ ] Test auth feature disabled in production
- [ ] Production backend rejects test-only auth requests
- [ ] Test accounts excluded from production
- [ ] Production OTP/MFA remains mandatory where required
- [ ] Test credentials are not present in source or Git history
- [ ] Test secrets and production secrets are separated
- [ ] Negative authorization tests passed

## Final test evidence
- Admin login:
- User login:
- Role restrictions:
- Protected API checks:
- Session expiration:
- Production bypass check:
