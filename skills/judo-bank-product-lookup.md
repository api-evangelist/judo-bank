---
name: Look up Judo Bank product reference data
description: >-
  Retrieve Judo Bank's publicly available banking products and their full detail
  from the CDR Product Reference Data API - no authentication required. Use to
  browse product categories (residential mortgages, term deposits, business loans)
  and read fees, rates, features, constraints and eligibility for a product.
api: openapi/judo-bank-cds-banking-products-openapi.yml
operations: [listBankingProducts, getBankingProductDetail]
---

# Look up Judo Bank product reference data

Judo Bank is an Australian CDR data holder. Its Product Reference Data (PRD)
endpoints are **public and unauthenticated** - no API key or OAuth token is
needed.

Base URL: `https://public.open.judo.bank/cds-au/v1`

## Conventions (required)

- Send the CDS version header on every request: `x-v: 3` for the products list,
  `x-v: 4` for product detail. Omitting it returns HTTP 400
  (`urn:au-cds:error:cds-all:Header/Missing`); an unsupported version returns
  HTTP 406 (`urn:au-cds:error:cds-all:Header/UnsupportedVersion`).
- Optionally send `x-fapi-interaction-id` (an RFC 4122 UUID); it is echoed in the
  response for request correlation.
- Errors come back as a CDS ErrorV2 list: `{ "errors": [ { "code", "title",
  "detail" } ] }`. See `errors/judo-bank-problem-types.yml`.

## Steps

1. **List products** — call `listBankingProducts` (`GET /banking/products`) with
   header `x-v: 3`. Optional query params: `product-category` (e.g.
   `RESIDENTIAL_MORTGAGES`, `TERM_DEPOSITS`, `BUSINESS_LOANS`), `effective`,
   `updated-since`, `brand`, `page`, `page-size`. Paginate with `page` /
   `page-size`; read `meta.totalRecords` / `meta.totalPages` and `links.next`.
2. **Pick a product** — take a `productId` from the `data[]` array of step 1.
3. **Get full detail** — call `getBankingProductDetail`
   (`GET /banking/products/{productId}`) with header `x-v: 4`. The response
   composes `features`, `constraints`, `eligibility`, `fees`, `depositRates`,
   and `lendingRates` (with rate `tiers`). See the entity graph in
   `data-model/judo-bank-data-model.yml`.

## Notes

- This surface is read-only. Account, balance, transaction and payment data are
  **not** available here - they require accreditation as a CDR data recipient
  (OAuth2/OIDC + FAPI consent flow brokered by the CDR Register).
