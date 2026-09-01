# Project charter

## Objective

Build a small but production-minded API gateway in Go that demonstrates how
requirements, constraints, and operational evidence shape infrastructure
design. The resulting repository should be useful both as executable software
and as a traceable engineering case study.

## Primary audience

- Backend engineers learning how an HTTP request moves through a gateway.
- Platform engineers evaluating routing, resilience, and observability trade-offs.
- Maintainers reviewing whether AI-assisted code was designed and verified by a
  responsible human.

## Core problem

Gateway tutorials often present isolated features without the invariants,
failure modes, and revisions that make a gateway trustworthy. Large production
projects provide working implementations but can obscure why a particular
trade-off was made.

This project makes the reasoning and evidence part of the product.

## v0.1 outcome

A user can run the gateway locally, configure routes to synthetic upstreams,
and observe deterministic behavior for normal traffic and selected failures.
The repository contains enough tests, traces, and decisions to explain what the
gateway guarantees and what it deliberately does not guarantee.

## Planned capability sequence

1. One correct HTTP request path.
2. Declarative routes and atomic configuration replacement.
3. Middleware ordering and API key identity.
4. Single-node rate limits and quotas.
5. Timeout, cancellation, retry safety, and circuit breaking.
6. Structured observability and failure experiments.
7. Performance profiling and reproducible benchmarks.
8. A publication review and first tagged release.

The sequence may change only when evidence changes the priority. A revision
must update the roadmap or add a superseding decision record.

## System boundaries

The gateway may:

- accept and proxy HTTP requests;
- select an upstream using an immutable route snapshot;
- apply request-scoped policy and middleware;
- enforce bounded resource and reliability policies;
- expose request-level telemetry.

The initial gateway does not:

- own business workflow state;
- plan or execute Agent tasks;
- act as a service registry or Kubernetes ingress controller;
- provide a general plugin marketplace;
- claim multi-region or production readiness without corresponding evidence.

## Clean-room rules

1. Implement from public specifications, standard-library behavior, published
   references, and independently written reasoning.
2. Do not copy or mechanically rewrite employer or non-public source code,
   schemas, configurations, tests, dashboards, incidents, or documentation.
3. Use synthetic names, topology, traffic, timings, traces, and failures.
4. Do not use employer-specific terminology, paths, hostnames, usernames, or
   operational numbers.
5. Record the public source and independent decision when external behavior
   materially influences an implementation.
6. Run a full working-tree and Git-history privacy review before publication.

## Evidence policy

Claims require evidence appropriate to their type:

| Claim | Required evidence |
| --- | --- |
| Correctness | Deterministic unit or integration test |
| Concurrency safety | Race-enabled test and stated invariant |
| Resilience | Fault injection with expected state transition |
| Performance | Reproducible benchmark method and environment |
| Compatibility | Contract test against the named public behavior |
| Security | Trust boundary, abuse case, and negative test |

Benchmark results must state environment, workload, sample size, limitations,
and whether the result changed a design decision.

## Change policy

- Behavior changes start with an issue containing acceptance criteria.
- Expensive-to-reverse decisions receive an ADR before implementation.
- Work is delivered in small, reviewable increments.
- Refactoring and behavior changes are separated when practical.
- Every milestone ends with a short retrospective: result, evidence, surprises,
  and revisions.

## Public development and release gate

The repository is developed publicly from its clean-room charter. Public
visibility is evidence of an open process, not a production-readiness claim.
The first tagged release is withheld until all of the following are true:

- a new user can follow the quick start without private dependencies;
- one end-to-end request path works and has deterministic tests;
- the repository remains covered by an explicit open-source license;
- no commit exposes a real identity, employer email, secret, or non-public
  material;
- README limitations match the implemented behavior;
- security and contribution policies are inherited or explicitly present;
- the complete Git history passes a clean-room and secret review.

## Success measures

The first release is successful when it provides:

- a runnable and explainable gateway rather than a feature scaffold;
- at least one design revision driven by tests or measurements;
- reproducible evidence for correctness and concurrency claims;
- a coherent series of technical articles derived from public project work;
- a credible portfolio artifact that can be reviewed commit by commit.
