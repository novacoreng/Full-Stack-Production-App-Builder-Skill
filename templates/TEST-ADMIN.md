# TEST ADMIN ACCOUNT

## Purpose
Controlled non-production account used to verify administrative functionality.

- Environment:
- Account identifier/username:
- Role:
- Permissions:
- Created:
- Expires/rotation date:
- Secret reference:
- MFA:
- Status:
- Owner:

## Security checks
- [ ] Not hardcoded in source
- [ ] Credential not committed to Git
- [ ] Credential not present in logs/screenshots/docs
- [ ] Least privilege applied
- [ ] Environment is non-production
- [ ] MFA enabled where supported
- [ ] Expiration/rotation configured
- [ ] Audit logging verified

## Verification matrix

| Requirement | Admin action | Expected | Actual | Result | Evidence |
|---|---|---|---|---|---|
| | | | | | |

## Boundary tests
- [ ] Normal user cannot access admin UI
- [ ] Normal user cannot call admin API successfully
- [ ] Unauthorized role changes are rejected
- [ ] Session expiry works
- [ ] Logout/revocation works
- [ ] Destructive actions are authorized and audited

## Cleanup
- [ ] Account disabled/revoked when no longer required
- [ ] Temporary credentials rotated
- [ ] Test data cleaned where required
- [ ] No secret values in logs
