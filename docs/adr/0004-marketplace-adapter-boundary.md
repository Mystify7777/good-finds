# ADR-0004: Isolate Marketplace Providers Behind Adapters

- Status: Accepted
- Date: 2026-11-01

## Context

Provider APIs, terms, data shapes, quotas, and failure modes differ. Domain logic should not become coupled to provider-specific schemas.

## Decision

Each marketplace integration implements a defined adapter contract and returns a normalized internal candidate. Provider-specific response types remain inside the adapter. Build only integrations whose access and data usage are permitted.

## Alternatives considered

- Provider logic scattered throughout application modules: rejected due to coupling.
- One generic adapter with provider-specific conditionals everywhere: rejected because it obscures provider differences and failure semantics.

## Consequences

- Easier testing with provider fixtures.
- A stable domain boundary.
- Each adapter requires its own capability/terms review and operational limits.
- No assumption that scraping is permitted.

## Follow-up work

Define adapter contract and provider feasibility gate before selecting the first production provider.
