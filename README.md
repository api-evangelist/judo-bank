# Judo Bank (judo-bank)

Judo Bank (Judo Capital Holdings Ltd) is an Australian challenger bank founded in 2016 and headquartered in Melbourne, purpose-built to serve small and medium-sized enterprises (SMEs) with relationship-led business lending alongside personal and business term deposits. It was the first new domestically-owned bank in decades to be granted a full, unrestricted authorised deposit-taking institution (ADI) licence by APRA, in April 2019, and has been publicly listed on the Australian Securities Exchange (ASX: JDO) since November 2021 — a for-profit, shareholder-owned bank, not a customer-owned mutual. As a designated ADI and data holder under Australia's Consumer Data Right (CDR / Open Banking) regime, Judo Bank exposes a public, unauthenticated Product Reference Data (PRD) API conforming to the Data Standards Body (DSB) Consumer Data Standards.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/judo-bank/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/judo-bank/refs/heads/main/apis.yml)

## Tags

- Financial
- Banks
- Open Banking
- CDR
- Consumer Banking
- Australia
- SME Lending
- Product Reference Data

## Timestamps

- **Created:** 2026-07-20
- **Modified:** 2026-07-20

## APIs

### Judo Bank CDR Product Reference Data API

Public, unauthenticated Consumer Data Right (CDR) Product Reference Data API for Judo Bank, served at `https://public.open.judo.bank/cds-au/v1` and conforming to the DSB Consumer Data Standards (CDS) Banking API. The `GET /banking/products` endpoint (confirmed live — HTTP 200, `x-v: 3`, 12 products) returns the bank's publicly available product catalogue with paginated metadata; `GET /banking/products/{productId}` returns full product detail. No authentication or API key is required for this product-reference surface.

- **Human URL:** [https://www.judo.bank/open-banking/](https://www.judo.bank/open-banking/)
- **Base URL:** `https://public.open.judo.bank/cds-au/v1`

#### Tags

- CDR
- Open Banking
- Product Reference Data
- Banking Products
- Australia

#### Properties

- [Documentation](https://consumerdatastandardsaustralia.github.io/standards/)
- [API Reference](https://consumerdatastandardsaustralia.github.io/standards/#cdr-banking-api_banking_get-products)
- [OpenAPI](openapi/judo-bank-cds-banking-products-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

## Common Properties

- [Website](https://www.judo.bank/)
- [Documentation](https://www.judo.bank/open-banking/)
- [GitHub Organization](https://github.com/judobank)
- [LinkedIn](https://www.linkedin.com/company/judobank)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
