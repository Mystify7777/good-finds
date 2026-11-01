# ADR-0002: Separate Canonical Products from Marketplace Listings

- Status: Accepted
- Date: 2026-11-01

## Context

The same physical product may be sold through multiple marketplaces and listings. Reviews and community history should not fragment merely because a listing URL differs.

## Decision

Represent a canonical product separately from marketplace-specific listings. Listings reference the canonical product and preserve provider identifiers, URLs, metadata snapshots, and refresh state. Product variants are modeled as a separate concern and must not be merged without confidence.

## Alternatives considered

- One product row per URL: rejected because cross-marketplace duplicates fragment community information.
- One product row per brand/model text only: rejected because titles and model names are inconsistent and may collapse distinct variants.

## Consequences

- Community data can be shared across listings for the same canonical product.
- Matching and merge/split correction require careful rules and auditability.
- Variant identity remains unresolved and is covered by ADR-0003.

## Follow-up work

Implement identity matching only after variant semantics and confidence/ambiguity handling are specified.
