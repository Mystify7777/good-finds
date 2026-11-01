# Roadmap

The roadmap is a sequence of outcomes, not a promise of calendar dates. Work is tracked in GitHub Issues.

## Phase 0 — Product and domain decisions

- Resolve product/variant identity and rating subjects.
- Define rating aggregation, sample thresholds, and verdict semantics.
- Define submission lifecycle and category immutability.
- Validate marketplace API access, terms, and data permissions.
- Define review provenance and moderation policies.

**Exit:** domain decisions are recorded as ADRs and provider integration is feasible.

## Phase 1 — Foundation

- Establish Next.js/TypeScript application structure.
- Configure formatting, linting, type checks, and tests.
- Provision PostgreSQL/Supabase environments.
- Define schema, migrations, and database access policies.
- Implement authentication, email verification, invitations, and registration mode.
- Build responsive public navigation and basic page shells.

**Exit:** visitors can browse the shell; invited users can authenticate; access rules are tested.

## Phase 2 — Product and marketplace ingestion

- Implement safe URL validation and marketplace resolver.
- Implement first permitted marketplace adapter.
- Normalize provider metadata and preserve provenance.
- Design canonical products, variants, and marketplace listings.
- Implement duplicate matching and ambiguity handling.
- Add background refresh and cached detail pages.

**Exit:** a supported product URL can be safely ingested, matched, reviewed, and displayed.

## Phase 3 — Community workflows

- Gems and Avoid submissions with controlled reasons.
- Wishlist submissions and purchase-state transition.
- Ratings and reviews with provenance distinctions.
- Community verdict and sample-size treatment.
- Wishlist discussion threads and replies.
- Search, filters, and pagination.

**Exit:** core member contribution and public discovery journeys work end-to-end.

## Phase 4 — Trust, safety, and operations

- Content reporting and moderation queue.
- Moderation actions and audit trail.
- Rate limiting and abuse detection.
- Admin membership and registration controls.
- Account deletion and privacy workflows.
- Observability, backups, restore rehearsal, and operational runbooks.

**Exit:** the platform can be operated safely by administrators.

## Phase 5 — MVP release

- Functional, integration, and end-to-end tests.
- Security review, especially URL ingestion and access policies.
- Accessibility and responsive checks.
- Production deployment and environment verification.
- Invite first community members and collect feedback.

**Exit:** MVP acceptance criteria in the PRD are met.

## Later, not MVP

- Additional marketplace adapters.
- Price history analytics and alerts.
- Product comparison.
- Helpful-review voting.
- Reputation systems.
- Recommendations.
- Native mobile clients.
- Public API.

Do not pull future work into MVP without an explicit scope decision.
