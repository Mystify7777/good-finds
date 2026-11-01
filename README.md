# Good Finds

**Community-driven product discovery and shopping intelligence.**

Good Finds helps people make better purchasing decisions by collecting real product experiences from a trusted community. Users can recommend products, warn others about disappointing purchases, and ask for advice before buying.

## Product surfaces

- **Gems** — products community members recommend.
- **Avoid** — products community members would not recommend, with reasons and context.
- **Wishlist** — products users are considering and want the community to discuss.

Product identity is canonical inside Good Finds. Marketplace listings, user submissions, ownership experiences, ratings, and discussions are related records rather than competing copies of the same product.

## Project status

The repository begins with product and engineering documentation. Implementation has not started.

## Documentation

| Document | Purpose |
|---|---|
| [PRD](docs/product/PRD.md) | Product requirements and MVP acceptance criteria |
| [Architecture](docs/architecture/README.md) | Initial system boundaries and technical direction |
| [Domain model](docs/architecture/domain-model.md) | Core entities and relationships |
| [Marketplace integration](docs/architecture/marketplace-integrations.md) | Adapter and ingestion contract |
| [Security](docs/security/README.md) | Initial security requirements and threat areas |
| [Roadmap](docs/ROADMAP.md) | Delivery phases and MVP scope |
| [Decision register](docs/adr/README.md) | Architecture decisions and unresolved questions |
| [Contributing](CONTRIBUTING.md) | Development and contribution workflow |

## Initial technical direction

- Next.js application using TypeScript
- PostgreSQL via Supabase
- Supabase Auth
- Tailwind CSS
- Modular monolith
- Background jobs for marketplace metadata refreshes

These are initial direction choices, not evidence that implementation or provider feasibility has already been validated. Marketplace API access, terms, quotas, and permitted data usage must be confirmed before an adapter is committed to production.

## Principles

1. Preserve genuine user experiences and their provenance.
2. Separate canonical products from marketplace listings.
3. Never imply purchase verification without actual verification.
4. Keep marketplace-sourced ratings separate from Good Finds ratings.
5. Preserve submission history and original category.
6. Prefer a simple modular monolith over premature distributed infrastructure.
7. Treat safety, privacy, moderation, and data provenance as product requirements.

## Development

The first implementation milestone is to settle the unresolved domain decisions, establish the application foundation, and implement the canonical product and marketplace listing model. See [open issues](https://github.com/Mystify7777/good-finds/issues).

## License

No license has been selected yet. Until one is added, all rights are reserved by default.
