# go-gateway-lab

A clean-room Go API gateway built from first principles through explicit
requirements, architecture decisions, executable tests, fault experiments, and
reproducible benchmarks.

The project exists to preserve engineering judgment, not merely to accumulate
gateway features. Each meaningful change should connect a real problem to a
documented decision and observable verification evidence.

## Status

Private project bootstrap. The first runnable request path is scheduled for the
`M0: One correct request path` milestone.

## First vertical slice

```text
Client
  -> HTTP listener
  -> route match
  -> reverse proxy
  -> synthetic upstream
  -> response to client
```

The first slice must define and test:

- request and response header behavior;
- client cancellation propagation;
- upstream timeout behavior;
- deterministic route matching;
- error ownership and stable external semantics;
- synthetic logs and metrics that reveal the request path.

## Scope

The initial project focuses on:

- Go HTTP serving and transport behavior;
- declarative routing and atomic configuration replacement;
- reverse proxy correctness;
- middleware ordering and caller identity propagation;
- rate limiting, quotas, resilience, and observability;
- concurrency tests, race detection, failure injection, and benchmarks.

## Non-goals

- Reconstructing or publishing an employer's gateway.
- Copying an existing open-source gateway and renaming its components.
- Supporting every gateway protocol or deployment environment in the first
  release.
- Adding LLM- or Agent-specific behavior before the traditional request path is
  correct and measurable.
- Treating feature count or benchmark headlines as proof of production quality.

## How decisions are recorded

Every substantial change should expose this chain:

```text
Problem
-> Constraints
-> Decision
-> Alternatives
-> Implementation
-> Verification
-> Revision
```

Architecture decisions live in [`docs/decisions`](docs/decisions). The project
charter and publication gates are defined in
[`docs/PROJECT_CHARTER.md`](docs/PROJECT_CHARTER.md).

## AI-assisted development

AI assistance is allowed for exploration, implementation, tests, review, and
documentation. It does not replace authorship or judgment.

- The maintainer must understand and verify every submitted change.
- Material assistance is disclosed in the pull request.
- No employer code, prompts, data, logs, paths, incidents, or internal designs
  may be sent to external models or added to this repository.
- The repository records concise decision rationale and evidence, not private
  model chain-of-thought.

## Quick start

There is no runnable gateway yet. Quick-start commands will be added with the
first executable slice rather than documenting an interface that does not
exist.

## License

The license will be selected and committed before this repository becomes
public. Apache-2.0 is the current infrastructure-oriented candidate because it
includes an express patent grant; the decision remains explicit and reversible
until publication.
