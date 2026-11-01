# Good Finds — Product Requirements Document

**Version:** 1.0  
**Status:** Baseline for implementation planning  
**Date:** 2026-11-01

## 1. Product overview

Good Finds is a community-driven shopping intelligence platform. Members submit product links, share their purchasing and usage experiences, rate products, and ask the community for advice. Public visitors can browse the product knowledge base without creating an account.

### Problem

Marketplace descriptions, promotional content, and aggregate seller ratings do not reliably answer whether a product is worth buying. People need contextual, independent experiences: what worked, what failed, how long it lasted, and whether it represented good value.

### Product proposition

Build a shared, searchable record of products and community experiences, with clear provenance and distinct workflows for recommendations, warnings, and pre-purchase questions.

### Core principles

- Genuine experiences over promotional content.
- Transparent provenance and uncertainty.
- Canonical product identity across marketplace listings.
- Separate ownership experience from unverified opinion.
- Preserve history rather than silently rewriting community context.
- Keep the MVP small and operationally understandable.

## 2. Audience and access

### Initial audience

A small private community of invited users. The architecture should permit later public registration and broader public participation.

### Roles

**Visitor**
- Browse product lists and details.
- Search and filter.
- Read reviews and Wishlist discussions.
- Cannot submit, rate, comment, or report.

**Registered member**
- Submit products.
- Rate products and write reviews.
- Create and reply to Wishlist discussions.
- Edit their own content where allowed.
- Report content.

**Administrator/moderator**
- Manage invitations and registration mode.
- Review reports and moderate content.
- Suspend accounts.
- Inspect administrative audit history.
- Manage platform configuration.

Role checks must be enforced server-side and, where supported by the data platform, reinforced at the database layer.

## 3. Product domain

### 3.1 Canonical product

A canonical product represents a distinct product/model within Good Finds. A canonical product is not a marketplace listing and must not be duplicated just because it is sold by multiple merchants.

### 3.2 Marketplace listing

A marketplace listing represents an offer or catalog page on a marketplace. It stores marketplace identity, external product identifier, URL, available metadata, and refresh state.

Different models, generations, and materially distinct variants must not be merged. Variant identity and rating granularity are an explicit design decision to resolve before implementation.

### 3.3 User submissions

A submission records a member's decision to add a product to Gems, Avoid, or Wishlist, including category-specific reason/context and creation time. Multiple users may submit the same canonical product. A product may have submissions in multiple categories. Original submission categories are immutable in the MVP unless an explicit correction workflow is designed.

## 4. Product sections

### 4.1 Gems

Purpose: surface products members recommend.

Required:
- Product URL submission.
- One predefined positive reason.
- Optional explanation.
- Retrieved product metadata.
- Community ratings and reviews.
- Original submitter and submission timestamp.
- Current community verdict, when enough feedback exists.

Initial reason catalogue:
- Excellent value for money.
- Better quality than expected.
- Durable and long-lasting.
- Works as advertised.
- Excellent performance.
- Better than expensive alternatives.

### 4.2 Avoid

Purpose: surface products members would not recommend.

Required:
- Product URL submission.
- One predefined negative reason.
- Optional explanation.
- Retrieved product metadata.
- Community ratings and reviews.
- Original submitter and timestamp.
- Current community verdict.

Initial reason catalogue:
- Poor build quality.
- Misleading product description.
- Overpriced for its quality.
- Stopped working prematurely.
- Poor after-sales service.
- Missing advertised features.

Moderation must distinguish subjective dissatisfaction from factual allegations of fraud, counterfeit goods, or misconduct. Reports and evidence must be reviewable.

### 4.3 Wishlist

Purpose: collect products a member is considering and request advice.

Required:
- Product URL submission.
- Optional question/context.
- Discussion threads and replies.
- Original creator and timestamps.
- Ability for creator to mark the item as purchased.

Wishlist discussion must not count as an ownership review or rating. After purchase, a member may create a separate Gems or Avoid submission and an owner-experience review.

## 5. Product URL ingestion

The normal submission flow begins with a URL; users do not manually author the canonical product catalog.

Workflow:
1. Accept URL over an authenticated server endpoint.
2. Validate scheme, host, and URL shape.
3. Resolve supported marketplace and external item identifier.
4. Retrieve metadata through a permitted integration.
5. Normalize the provider response.
6. Match an existing canonical product and variant, or flag ambiguous matches.
7. Present retrieved metadata to the user for confirmation.
8. Create a submission in the chosen section.
9. Preserve provider provenance and metadata refresh timestamps.

Metadata may include title, brand, images, description, specifications, marketplace, external identifier, canonical URL, price, currency, availability, marketplace rating/count, variant information, and last successful update.

If a URL is unsupported, inaccessible, ambiguous, or cannot be retrieved, display a useful error. Do not fabricate metadata or create a misleading partial product record. A retry path may be offered.

URL retrieval is a security boundary. The implementation must defend against SSRF, redirects to private networks, DNS rebinding, unsafe schemes, oversized responses, and hostile content. Do not fetch arbitrary user-provided URLs from privileged network context.

## 6. Ratings, reviews, and verdicts

### 6.1 Ratings

- Only authenticated members may rate.
- One active rating per member per rating subject.
- A member may update their rating; the active aggregate must use only the latest active value.
- Historical changes may be retained for auditability.
- Wishlist opinions do not affect product ratings.
- Marketplace ratings and Good Finds ratings are displayed separately.
- Show the rating count and sample-size context.

Initial dimensions:
- Overall experience.
- Value for money.

Use a five-star scale. Whether ratings attach to canonical product, variant, or both is an open domain decision. Support product-level aggregation only where it is meaningful and transparent.

### 6.2 Review provenance

Distinguish:
- **Verified purchase:** evidence has actually been checked through a defined process.
- **Owner experience:** member claims to own/use the product; evidence has not been checked.
- **Community opinion:** member does not claim personal ownership.

Do not label an unverified claim as verified. MVP may initially support Owner experience and Community opinion; a verified-purchase mechanism must not be implied until built.

### 6.3 Review content

Optional fields:
- Personal experience.
- Duration of use.
- Positive aspects.
- Negative aspects.
- Would purchase again?
- Additional explanation.

### 6.4 Community verdict

Calculate from eligible active Good Finds ratings. The verdict must not be manually set by ordinary users.

Requirements:
- One active rating per member per subject.
- Rating edits replace the previous active rating.
- Historical changes remain auditable.
- Wishlist discussion sentiment is excluded.
- Display contributing-user count.
- Indicate insufficient feedback at low sample sizes.
- Support positive, mixed, and negative states.
- Never overwrite the original submission category with the current verdict.

Thresholds, minimum sample size, weighting, and variant roll-up rules must be specified in an ADR before implementation.

## 7. Wishlist discussions

- A Wishlist entry supports multiple discussion threads.
- Threads support replies.
- Authors may edit their own comments under an explicit edit policy.
- Users can report content.
- Display timestamps.
- Notify the Wishlist creator of replies when notifications are implemented.
- Publicly readable without authentication.
- Creating threads and replies requires authentication.

Discussions remain distinct from reviews and ratings.

## 8. Lifecycle and history

- Multiple submissions can point to one canonical product.
- A product can have submissions in different sections.
- Original submission category remains preserved.
- Users may edit their own review subject to audit/history policy.
- Wishlist creator can mark the entry purchased.
- Product metadata refreshes independently from community content.
- An unavailable marketplace listing does not delete the canonical product or community history.
- Product merge/split and mistaken duplicate correction need explicit audited workflows.

## 9. Authentication and invitations

MVP:
- Email registration and verification.
- Secure authentication/session handling.
- Account recovery.
- Account suspension.
- Account deletion request handling.
- Invite-only registration by default.
- Administrators can create, revoke, and inspect invitations.
- Invitations have expiry and single-use semantics by default.

The registration policy must be configurable between invite-only and public registration without code changes or schema migration. Public browsing remains available in either mode.

## 10. Moderation and abuse

Reportable content:
- Incorrect product information.
- Duplicate products.
- Spam.
- Abusive reviews/comments.
- Suspicious rating activity.
- Misleading claims.
- Inappropriate discussion content.

Administration:
- Review and triage reports.
- Resolve/dismiss reports with reason.
- Hide/remove content.
- Suspend accounts.
- Restore content when appropriate.
- Record moderation actions in an audit log.

Abuse controls:
- Per-account and per-IP rate limits.
- Endpoint-specific limits for submissions, ratings, and comments.
- Duplicate and repeated-content detection.
- Suspicious rating pattern detection.
- CAPTCHA only when risk signals warrant it.
- Do not rely solely on IP limits or invasive device fingerprinting.

## 11. Marketplace integrations

Use independent marketplace adapters. Each adapter returns a normalized internal representation; application/domain code must not depend on provider response formats.

Potential targets include Amazon India and Flipkart, subject to actual API access, terms, data permissions, quotas, and technical feasibility. Do not assume scraping is permitted or stable.

Refresh metadata in the background where integrations permit it. Initial target cadence is daily, not real-time. Record last attempt, last success, and failure state. Provider failure must not make cached product pages unavailable.

Maintain price history only where permitted and sufficiently reliable. Lowest/highest/average price and alerts are future features.

## 12. UX and discovery

Primary navigation:
- Gems.
- Avoid.
- Wishlist.

Homepage also contains search, recently added products, product submission entry point, account access, and community activity.

Product cards may show:
- Product image/name.
- Current price/currency.
- Marketplace.
- Marketplace rating.
- Good Finds community rating.
- Community verdict.
- Number of community ratings.

Product detail page:
1. Product/variant information.
2. Marketplace listings and outbound links.
3. Price and metadata update timestamp.
4. Marketplace rating.
5. Good Finds rating and count.
6. Community verdict and confidence/sample context.
7. Original submissions and reasons.
8. Reviews.
9. Wishlist discussions where relevant.
10. Report action.

Search:
- Product name and brand.
- Marketplace.
- Category.
- Community verdict.
- Sort by recently added, highest rated, and most discussed.

Pagination is required for lists. Search must not create products.

## 13. Technical direction

Initial direction:
- Next.js + TypeScript.
- PostgreSQL through Supabase.
- Supabase Auth.
- Tailwind CSS.
- Vercel or equivalent hosting.
- Scheduled jobs/lightweight workers for metadata refresh.

Architecture: modular monolith. Do not introduce microservices in the MVP.

Suggested modules:
- Identity and invitations.
- Products and variants.
- Marketplace listings and adapters.
- Product submissions.
- Ratings and reviews.
- Community verdicts.
- Wishlist discussions.
- Moderation.
- Price history.
- Notifications.
- Administration.

Security:
- Server-side authorization.
- Database-level access policies.
- Input validation.
- SSRF-safe URL ingestion.
- XSS and SQL injection protections.
- Secret management.
- Rate limiting.
- Administrative audit logs.
- Backup and recovery.

## 14. Non-functional requirements

- Responsive mobile and desktop layouts.
- Keyboard-accessible interactions and adequate contrast.
- Paginated public listings.
- Marketplace retrieval never blocks the whole application.
- Provider outages do not break cached browsing.
- Retry failed background work with bounded backoff.
- Retain reviews when listings disappear.
- Public pages expose no unnecessary private account data.
- Never publish email addresses.
- Retain IP/security data only as needed for abuse prevention.
- Provide an account deletion process.
- Maintain backups and a recovery procedure.

## 15. MVP scope

Included:
1. Public homepage and navigation.
2. Gems, Avoid, Wishlist.
3. Supported product URL submission.
4. At least one marketplace integration with confirmed permitted access.
5. Product normalization and deduplication.
6. Canonical product and marketplace listing records.
7. Registration, verification, invite-only mode.
8. Configurable invite-only/public registration.
9. Ratings and reviews with provenance labels.
10. Predefined reasons and optional explanations.
11. Basic Wishlist discussions and replies.
12. Product search and pagination.
13. Basic moderation and reports.
14. Admin dashboard.
15. Rate limiting and security controls.
16. Automated tests and deployment pipeline.

Excluded:
- Recommendation engine.
- Automated verified-purchase integrations.
- Reputation scoring.
- Price-drop notifications.
- Advanced comparisons.
- Real-time monitoring.
- Public API.
- Native mobile app.
- AI-generated recommendations.

## 16. Delivery phases

1. **Product/domain decisions:** close open questions on variants, ratings, identity, moderation, and provider feasibility.
2. **Foundation:** app setup, database, auth, invitations, policies, navigation.
3. **Product management:** URL ingestion, adapter, normalized metadata, matching/deduplication, product detail.
4. **Community:** submissions, reasons, ratings, reviews, verdicts, Wishlist discussions.
5. **Trust and operations:** reports, moderation, rate limits, audit, admin configuration.
6. **Release:** functional/security/accessibility testing, deployment, backups, private-community feedback.

## 17. MVP acceptance criteria

The MVP is ready when:
1. Visitors browse without an account.
2. Visitors cannot perform member-only actions.
3. Invited users register and verify.
4. Admin controls registration mode.
5. Members submit supported URLs.
6. Metadata comes from a permitted integration and preserves provenance.
7. Duplicate URLs resolve to one canonical product/variant where matching is confident.
8. Ambiguous variant matches are not silently merged.
9. Multiple users can submit the same product independently.
10. Different categories can reference the same product.
11. Original categories are preserved.
12. Members rate and update ratings without duplicate active votes.
13. Community verdicts handle insufficient sample sizes.
14. Wishlist discussions support replies.
15. Reports can be triaged and moderated.
16. Provider failures do not break browsing.
17. Metadata freshness is visible.
18. Application works on mobile and desktop.
19. Authorization and URL-ingestion security tests pass.
20. Backup and recovery procedures are documented.

## 18. Guiding principle

Good Finds does not claim to determine objective product quality. It helps people make better decisions by presenting real experiences, transparent community opinions, product context, and historical information. Its value depends on the trustworthiness of the information, not the number of products listed.
