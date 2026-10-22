---
name: judo-bank-account-data-sharing
description: >-
  Read a consenting Judo Bank customer's accounts, balances and transactions
  through the Consumer Data Right (CDR) Banking API. Only an accredited CDR data
  recipient (ADR) holding a valid consent can run this skill.
api: openapi/judo-bank-banking-accounts-api-openapi.yml
apis:
  - openapi/judo-bank-banking-accounts-api-openapi.yml
  - openapi/judo-bank-banking-account-balances-api-openapi.yml
  - openapi/judo-bank-banking-account-transactions-api-openapi.yml
operations: [listBankingAccounts, getBankingAccountDetail, getBankingBalance, listBankingBalancesBulk, listBankingTransactions, getBankingTransactionDetail]
---

# Read consented Judo Bank account data (CDR)

**Gate:** these operations are not public. They need CDR accreditation, a
customer consent obtained through the CDR OAuth2/OIDC + FAPI flow (brokered by
the CDR Register), and mTLS. Judo Bank does not publish the authenticated
data-holder base URL in these specs; the `servers[]` value
(`mtls.dh.example.com`) is the DSB placeholder. See
`authentication/judo-bank-authentication.yml`.

## Conventions (required)

- Send `x-v` (endpoint version) on every call, plus `x-fapi-interaction-id`
  (a UUID that is echoed back for correlation).
- Errors use the CDS ErrorV2 envelope `{ "errors": [ { "code", "title", "detail" } ] }`.
  See `errors/judo-bank-problem-types.yml`.
- Every operation here is a read. The POST `...SpecificAccounts` variants are
  reads that filter by an account-ID list sent in the body, not writes.

## Steps

1. **List accounts**: `listBankingAccounts` (`GET /banking/accounts`). Page
   through the results with `page` and `page-size`.
2. **Account detail**: `getBankingAccountDetail` (`GET /banking/accounts/{accountId}`).
3. **Balances**: `getBankingBalance` (`GET /banking/accounts/{accountId}/balance`)
   for one account, or `listBankingBalancesBulk` (`GET /banking/accounts/balances`)
   for all consented accounts.
4. **Transactions**: `listBankingTransactions`
   (`GET /banking/accounts/{accountId}/transactions`), optionally filtered by
   `oldest-time` / `newest-time`. Then call `getBankingTransactionDetail`
   (`GET /banking/accounts/{accountId}/transactions/{transactionId}`) for
   the extended data.
