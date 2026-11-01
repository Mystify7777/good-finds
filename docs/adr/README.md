# Architecture Decision Records

ADRs capture decisions that materially constrain implementation. Accepted decisions should not be casually contradicted by code; supersede them with a new ADR.

## Status vocabulary

- **Proposed** — under discussion.
- **Accepted** — selected direction.
- **Rejected** — considered and declined.
- **Superseded** — replaced by a later decision.

## Decision register

| ADR | Decision | Initial status |
|---|---|---|
| [0001](0001-modular-monolith.md) | Start with a modular monolith | Accepted |
| [0002](0002-canonical-product-and-listing.md) | Separate canonical products from marketplace listings | Accepted |
| [0003](0003-product-variant-and-rating-subject.md) | Product variant and rating subject semantics | Proposed |
| [0004](0004-marketplace-adapter-boundary.md) | Isolate marketplace providers behind adapters | Accepted |
| [0005](0005-review-provenance.md) | Make review provenance explicit | Accepted |
| [0006](0006-community-verdict.md) | Community verdict aggregation policy | Proposed |

## How to add an ADR

1. Copy the template below into a numbered file.
2. State the context and constraints.
3. List real alternatives, not strawmen.
4. Describe consequences and migration impact.
5. Update this register.
6. Link the ADR from the relevant implementation issue.

### Template

```md
# ADR-NNNN: Title

- Status: Proposed
- Date: YYYY-MM-DD

## Context
## Decision
## Alternatives considered
## Consequences
## Follow-up work
```
