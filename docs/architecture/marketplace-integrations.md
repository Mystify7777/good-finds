# Marketplace Integrations

## Purpose

Marketplace adapters isolate provider-specific behavior from catalog and submission workflows. The MVP should ship only an adapter whose API access, usage terms, data permissions, quotas, and reliability have been confirmed.

Do not assume scraping is permitted, stable, or acceptable.

## Adapter responsibilities

Each adapter should:
- Recognize supported product URLs.
- Parse stable marketplace identifiers.
- Retrieve metadata using permitted mechanisms.
- Normalize provider data to an internal contract.
- Expose provider attribution and source timestamps.
- Classify transient, permanent, authorization, quota, and not-found failures.
- Respect quotas and retry guidance.
- Avoid leaking provider secrets into logs or client responses.

## Conceptual normalized result

```ts
type MarketplaceProductCandidate = {
  marketplaceKey: string;
  externalProductId: string;
  sourceUrl: string;
  retrievedAt: string;
  sourceUpdatedAt?: string;
  product: {
    title: string;
    brand?: string;
    description?: string;
    images: Array<{ url: string; alt?: string }>;
    specifications: Record<string, string>;
    modelNumber?: string;
  };
  variant?: {
    externalVariantId?: string;
    attributes: Record<string, string>;
  };
  listing: {
    price?: { amount: string; currency: string };
    availability?: "available" | "unavailable" | "unknown";
    canonicalUrl: string;
  };
  marketplaceRating?: {
    value: string;
    scale: string;
    reviewCount?: number;
  };
};
```

This is an illustrative contract, not committed application code. Preserve raw provider payload only when terms permit and apply appropriate retention controls.

## Ingestion safety

- Permit HTTPS only unless a narrowly justified exception exists.
- Use an explicit host allowlist; do not fetch arbitrary domains.
- Resolve DNS and reject loopback, private, link-local, multicast, and reserved destinations.
- Revalidate each redirect target and cap redirect count.
- Defend against DNS rebinding and IP representation tricks.
- Apply connection/read timeouts and response size limits.
- Validate content type and parse as untrusted input.
- Never forward internal credentials or ambient cloud metadata credentials.
- Avoid logging secrets or full URLs containing sensitive query tokens.

## Reliability

- Run refresh in background jobs.
- Use idempotency keys for listing/provider identity.
- Persist last attempt, last success, and sanitized failure classification.
- Use bounded retries with backoff and jitter.
- Respect provider rate limits and retry-after headers.
- Serve cached product data if provider is unavailable.
- Expose metadata freshness to users.

## Provider feasibility gate

Before building a production adapter, record:
1. Official API or permitted integration route.
2. Terms and allowed storage/display of fields/images/prices/ratings.
3. Authentication and secret management.
4. Quotas, costs, and attribution requirements.
5. Regional/product coverage for India.
6. Rate limit and outage behavior.
7. Whether price history/periodic refresh is permitted.

A provider that fails this gate must not be silently replaced with scraping.
