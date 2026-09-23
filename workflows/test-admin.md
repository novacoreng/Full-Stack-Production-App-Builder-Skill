# Test Admin Account Lifecycle

A test administrator is a controlled test fixture, not a backdoor.

## When to create one

After a successful non-production build/deployment, create a dedicated test/admin account when the product has an administrative role and admin flows need verification.

Do not create a privileged account merely because the project has an "admin" table or role if the role is not part of the accepted product contract.

## Safety rules

- Create only in development, preview, or staging unless the owner explicitly authorizes a production test account.
- Never hardcode a universal admin username/password.
- Never commit the credential to GitHub.
- Never print the password/token in logs, screenshots, README, PR descriptions, or handoff files.
- Prefer a provider-supported invitation, temporary password, or generated random credential.
- Use least privilege: grant exactly the permissions required by the admin test plan.
- Require MFA where the environment/provider supports it and the admin flow supports it.
- Mark the account as TEST ONLY.
- Set an expiration/rotation date where the provider supports it.
- Revoke or disable the account after the test window when it is no longer required.

## Credential storage

Store generated credentials only in the approved secret manager/test vault or secure agent credential store available to the environment. The project documentation may contain:
- test account identifier/username;
- role;
- environment;
- creation time;
- expiry/rotation time;
- secret reference name;
- verification status.

It must not contain the secret value.

## Admin verification plan

Use the test account to verify:
- admin login and session handling;
- MFA/recovery where applicable;
- authorization boundaries;
- dashboard access;
- CRUD operations;
- moderation/approval workflows;
- user/account management;
- role/permission enforcement;
- audit logs;
- notifications;
- exports/reports;
- destructive-action confirmation;
- unauthorized access from a normal user;
- session expiry/logout;
- rate limits and error states.

For every admin capability, record the expected result, observed result, test evidence, and requirement ID.

## Failure conditions

Do not mark admin testing complete if:
- the account was created in the wrong environment;
- credentials are exposed;
- normal users can access admin endpoints;
- the UI hides an action but the API still permits it;
- RLS/authz is missing;
- the account cannot be revoked/rotated when required;
- destructive admin actions lack appropriate authorization and audit behavior.

## Cleanup

After verification:
1. revoke/disable the account if it is no longer needed;
2. rotate any temporary credentials;
3. remove test data that should not persist;
4. verify audit logs contain no secret values;
5. record the cleanup status.

If the project owner wants a persistent staging admin, document it as a managed operational account with owner, purpose, MFA, rotation, and recovery process.
