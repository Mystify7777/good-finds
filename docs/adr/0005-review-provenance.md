# ADR-0005: Make Review Provenance Explicit

- Status: Accepted
- Date: 2026-11-01

## Context

A claimed owner experience, a general opinion, and a verified purchase are not equivalent evidence. Mislabeling these erodes trust.

## Decision

Every review has an explicit provenance class. Initial classes are owner experience, community opinion, and verified purchase. The verified-purchase label is usable only after a verification mechanism has actually checked evidence. MVP may launch without verified-purchase support.

## Alternatives considered

- Treat all reviews as equivalent: rejected because evidence quality becomes opaque.
- Allow self-selection of verified purchase: rejected because it implies a check that did not occur.

## Consequences

- Review UI can communicate evidence level.
- Verification workflow may be deferred.
- Moderation must handle false or misleading provenance claims.

## Follow-up work

Define review editing, ownership claim, and account deletion behavior in implementation design.
