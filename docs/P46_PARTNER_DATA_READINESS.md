# KnockOff P4.6 — Partner Data Readiness

Status: **Preparation only — no authorised external feed connected**  
Public demo: https://crazypm26.github.io/knockoff-partner-demo/  
Version: P4.6 · 22 November 2026

## Purpose

This document defines what KnockOff needs from a prospective affiliate network or retailer before importing product records. It does not grant permission, establish an affiliate relationship, or certify a product price as current.

## Commission Factory access questions

1. Is a private-beta comparison application with a public interactive demonstration eligible for publisher approval?
2. Are automated product comparisons and price-beat discovery permitted promotional methods?
3. Does feed access require separate approval from each advertiser?
4. Which feed delivery methods are authorised: download, scheduled export, API or another mechanism?
5. What authentication, rate limits, refresh limits and retention rules apply?
6. Are prices, images, availability, delivery and deep links permitted to be displayed publicly?
7. May the publisher combine permitted catalogue observations with other independently sourced prices?
8. Are there restrictions on displaying a competing retailer's price or directing shoppers to a price-match/price-beat feature?
9. How are expired offers, stock changes and withdrawn permissions communicated?
10. What disclosures and attribution are required for approved affiliate links?

**Do not assume affirmative answers until confirmed in writing.**

## Feed acceptance contract (proposed; not a provider specification)

| Field | Purpose | Gate |
|---|---|---|
| source_id and advertiser_id | Permission and attribution | Required |
| source_record_id / SKU | Stable feed record key | Required |
| title and brand | Search and candidate matching | Required |
| manufacturer_model / GTIN | Exact identity matching | At least one strong identifier preferred; ambiguous matches quarantined |
| product_url | Retailer verification path | Required, allowlisted retailer domain |
| currency and price | Offer comparison | Required, positive AUD price |
| price_type | Advertised vs conditional vs checkout | Required, never infer conditional quote as shelf price |
| stock_status | Availability claim | Required before displaying in-stock claim |
| delivery_cost / method | Landed-price calculation | Missing means total not established |
| observed_at and imported_at | Freshness and provenance | Required |
| image_url | Optional visual | Display only when licensed/permitted |
| tracking_url | Approved referral path | Only when advertiser/network permits |
| source_file_hash | Audit and deduplication | Required for batch imports |

## Approval and data-flow gates

1. **Publisher approved:** Store approval date and network terms privately.
2. **Advertiser approved:** Check each retailer relationship independently.
3. **Permitted use recorded:** Document rights for price, image, deep link, comparison and caching.
4. **Credential handling:** Keep credentials outside the public repository and browser assets.
5. **Ingestion:** Import only via an approved interface; do not scrape login-gated or interactive price-check flows.
6. **Validation:** Check schema, URL domain, currency, timestamps, identifiers, stock and delivery.
7. **Quarantine:** Reject or hold stale, incomplete, ambiguous, conflicting or unauthorised observations.
8. **Product matching:** Require exact model/variant or GTIN confidence before cross-retailer comparison.
9. **Customer display:** Clearly distinguish advertised price, automated Price Check, manual quote and checkout price.
10. **Audit and withdrawal:** Retain provenance privately and remove offers when permission expires or is revoked.

## TGG Price Check handling

The Good Guys' interactive Price Check is a separate retailer-controlled offer mechanism. A historic user-observed quote is not a live feed. Unless an authorised integration exposes the current result, KnockOff should direct the shopper to the retailer's Price Check and require them to confirm the actual cart total. Do not derive a universal discount rule from the historical $992 monitored competitor price / $982 offer example.

## First authorised-import acceptance test

An initial import is successful only when:
- a written source permission and approved advertiser relationship are documented;
- at least one real, non-synthetic product record is obtained through the permitted interface;
- the record is mapped to a source and time, with an immutable batch fingerprint;
- product identity and price-type checks pass;
- missing stock or delivery evidence is clearly flagged;
- no unsupported claim of a guaranteed price beat or live saving appears on the public demo;
- the import report identifies accepted, quarantined and rejected records with reasons.

## Current evidence / status

- Public interactive demonstration: published and observed working by the project owner.
- Commission Factory eligibility and feed enquiry: sent by project owner; reply pending.
- Commission Factory publisher approval: not confirmed.
- Advertiser approvals: not confirmed.
- Authorised product feed: not received.
- TGG Price Check machine-readable access: not established.
- Live customer-ready offers: none verified.

## Security and public-demo boundary

The public GitHub Pages site is a static, sample-data demonstration. Do not commit tokens, credentials, applicant identity documents, publisher IDs, real feed exports, confidential contracts or unpublished retailer terms. Keep live ingestion and audit records in a separate private environment. This file is a public integration-readiness outline, not a production integration or provider endorsement.

## Next trigger

When Commission Factory replies, review the response against the ten access questions above. If approved, request a sample permitted export and field dictionary before changing the import adapter. If declined or additional requirements apply, update the readiness plan without falsely representing the existing demo as a live service.
