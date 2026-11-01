# ADR-0003: Product Variant and Rating Subject Semantics

- Status: Proposed
- Date: 2026-11-01

## Context

Material variants can affect purchase experience. For example, RAM/storage configurations, sizes, regional models, and generations may differ materially. A single aggregate rating can hide variant-specific problems, while fully independent ratings can fragment feedback.

## Decision

Open. The preferred direction is to model variants explicitly and support variant-level feedback where a difference materially affects experience. Product-level roll-up may be shown only with a transparent aggregation rule and sufficient sample size.

## Alternatives considered

1. All feedback attaches to a parent product.
2. All feedback attaches only to a specific variant.
3. Feedback attaches to an explicit rating subject, which may be product-wide or variant-specific, with optional parent roll-up.

## Consequences to evaluate

- Identity matching and deduplication complexity.
- User submission friction when selecting variants.
- Handling legacy reviews where exact variant is unknown.
- Minimum sample size and aggregation semantics.
- Avoiding misleading roll-ups across materially different products.

## Required follow-up

Resolve via domain issue before final schema constraints and rating implementation. Document treatment of unknown variant as well as product-level aggregate.
