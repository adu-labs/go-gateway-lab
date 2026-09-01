# ADR-0002: Develop publicly under Apache-2.0

## Status

Accepted

## Date

2026-09-01

## Context

The project is intended to demonstrate not only its final implementation but
also the sequence of requirements, decisions, experiments, and revisions that
produces it. Keeping development private until a runnable release would hide
the early decision record and would consume the limited GitHub Actions quota
available to private repositories on the organization plan.

Public development is irreversible in practice: a later visibility change
cannot retract clones, forks, indexes, or previously visible history. The
project therefore needs a clean-room boundary that is safe from the first
commit rather than a final sanitization pass.

Public source also needs an explicit license. Infrastructure users benefit from
a permissive license with an express patent grant.

## Decision

Develop `go-gateway-lab` publicly from the project charter onward and license
the repository under Apache License 2.0.

Every commit must be independently publishable and pass identity, secret, and
clean-room review before push. Public visibility does not imply that an early
commit is stable, secure, compatible, or production-ready; release tags and the
README state the actual maturity.

## Alternatives considered

### Keep the repository private until the first runnable slice

- Advantage: mistakes can be removed before public exposure.
- Cost: early reasoning is not observable, private CI uses plan quota, and a
  final cleanup can create false confidence about historical safety.
- Rejected because the project goal includes transparent engineering history.

### Use the MIT License

- Advantage: short, familiar, and permissive.
- Cost: it does not include the same express patent grant and termination terms
  as Apache-2.0.
- Rejected because infrastructure adoption benefits from explicit patent terms.

### Publish source without a license until v0.1

- Advantage: postpones the license decision.
- Cost: public visibility alone grants no general right to use, modify, or
  redistribute the work.
- Rejected because the project is intended to be open source from the start.

## Consequences

- All staged changes require privacy and clean-room review before push.
- Accidentally published material must be treated as exposed even if removed
  from later commits.
- Standard GitHub-hosted Actions can be used without private-repository minute
  quota, subject to GitHub policy and runner choice.
- Apache-2.0 contribution and redistribution conditions apply from the first
  public version.
- Maturity claims remain tied to tests, evidence, and releases rather than
  repository visibility.
