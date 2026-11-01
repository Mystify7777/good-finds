# ADR-0001: Start with a Modular Monolith

- Status: Accepted
- Date: 2026-11-01

## Context

Good Finds is starting with a small invited community and a focused MVP. The domain has multiple areas, but they share transactional workflows and have no demonstrated independent scaling requirements.

## Decision

Build one deployable application with explicit internal modules and one primary PostgreSQL database. Background work may run in a separate process/runtime while remaining part of the same codebase and domain model.

## Alternatives considered

- Microservices: rejected for MVP due to operational overhead, distributed consistency, and deployment complexity without a demonstrated need.
- Unstructured monolith: rejected because it weakens domain boundaries and makes later change harder.

## Consequences

- Simpler development, testing, deployment, and transactions.
- Internal contracts and dependency direction still need enforcement.
- Extract a service only when measurable operational or organizational pressure justifies it.

## Follow-up work

Define module dependency rules and test boundaries during project setup.
