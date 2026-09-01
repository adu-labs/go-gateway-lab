# ADR-0001: Start with a clean-room request path

## Status

Accepted

## Date

2026-09-01

## Context

The long-term project may cover routing, middleware, identity, rate limiting,
resilience, observability, and performance. Beginning with a broad architecture
or a large feature matrix would make it difficult to verify behavior, preserve
a comprehensible Git history, or distinguish independent design from familiar
production systems.

The first implementation must also strengthen knowledge of Go's HTTP lifecycle
instead of hiding it behind a framework.

## Decision

Begin with one executable HTTP request path built from the Go standard library:

```text
listener -> route match -> reverse proxy -> synthetic upstream -> response
```

The slice is complete only when tests cover the normal path, upstream timeout,
client cancellation, and defined header behavior. Configuration, middleware,
distributed state, and protocol expansion are deferred until this path is
correct and observable.

Implementation will be written clean-room from public specifications,
standard-library documentation and source, and independently recorded
reasoning. Employer code and non-public operational material are not inputs.

## Alternatives considered

### Design the complete gateway architecture first

- Advantage: produces an early component map and broad roadmap.
- Cost: decisions are made without executable feedback and create speculative
  abstractions.
- Rejected because the first milestone should test invariants, not architecture
  aesthetics.

### Start with configuration, plugins, and a management API

- Advantage: creates visible platform features quickly.
- Cost: delays the request path that every later feature must preserve.
- Rejected because control-plane breadth cannot compensate for an undefined
  data-plane contract.

### Fork or reduce an existing gateway

- Advantage: reaches feature breadth faster.
- Cost: weakens the learning objective, obscures authorship, and makes
  clean-room reasoning difficult to demonstrate.
- Rejected because this repository is intended to preserve independent
  judgment rather than maximize short-term feature count.

### Build a custom HTTP transport immediately

- Advantage: exposes low-level protocol and connection behavior.
- Cost: introduces complexity before the gateway contract and failure model are
  understood.
- Rejected for the first slice; a custom transport may be reconsidered if a
  measured requirement cannot be met by the standard library.

## Consequences

- The repository will look intentionally small during the first milestone.
- Tests and request-path documentation are first-class deliverables.
- Later components must name the invariant they preserve or change.
- Standard-library behavior becomes an explicit dependency that must be studied
  and contract-tested where it matters.
- The decision can be superseded if measured requirements justify a different
  transport or architecture.
