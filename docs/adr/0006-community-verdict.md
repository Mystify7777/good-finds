# ADR-0006: Community Verdict Aggregation Policy

- Status: Proposed
- Date: 2026-11-01

## Context

A summary verdict is useful but can be misleading with low sample sizes, duplicate votes, or mixed product variants.

## Decision

Open. Verdicts will derive only from eligible active Good Finds ratings. External marketplace ratings and Wishlist discussion sentiment are excluded. The UI must show rating count and represent insufficient feedback rather than implying confidence.

## Questions

- How many distinct raters are required before a verdict appears?
- Which rating dimensions contribute to the headline verdict?
- Are ratings weighted equally?
- Are variant ratings rolled up to parent product, and under what conditions?
- What are the exact positive/mixed/negative thresholds?
- How are rating edits, deleted accounts, and suspicious ratings treated?

## Follow-up work

Resolve after ADR-0003 and create deterministic aggregation fixtures and tests.
