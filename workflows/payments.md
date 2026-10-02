# Payments
Use real provider integrations for production. Verify payments server-side, verify signed webhooks, use idempotency and duplicate protection, model transaction states, handle retries/refunds/failures, preserve transaction history, and recover from interrupted payment flows.


## Financial runtime QA
Financial state is server-authoritative. Client callbacks/UI success are not proof of payment. In sandbox/non-production, test amount validation, duplicate/idempotent requests, insufficient balance, reservation/settlement, signed webhook/provider verification, interruption/retry/reversal/reconciliation, ledger conservation, and concurrency where applicable. Never fake payment, wallet credit, withdrawal, refund, settlement, donation, or payout success. Classify untestable provider steps as PROVIDER BLOCKED.
