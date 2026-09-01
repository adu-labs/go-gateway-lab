# Repository instructions

These instructions apply to humans and AI coding agents working in this
repository.

## Before changing anything

1. Read `README.md`, `docs/PROJECT_CHARTER.md`, and relevant ADRs.
2. Identify the issue and its observable acceptance criteria.
3. State the invariant, trust boundary, or failure behavior affected.
4. Add an ADR before implementing a decision that is expensive to reverse.

## Implementation workflow

1. Work on one independently verifiable slice.
2. Prefer a failing test or executable reproduction before behavior changes.
3. Implement the smallest change that satisfies the acceptance criteria.
4. Run focused verification, then the repository-wide checks.
5. Review the staged diff for scope, secrets, identity leaks, and unrelated
   formatting.
6. Commit one logical outcome with an intent-oriented message.

Once a Go module exists, the minimum verification set is:

```bash
go test ./...
go test -race ./...
go vet ./...
```

Benchmark and fault claims require the project-specific reproducible command in
the pull request.

## Clean-room boundary

Never add or send to an external model:

- employer source code, schemas, configurations, documentation, or prompts;
- internal hostnames, usernames, paths, topology, metrics, traces, or incidents;
- copied or mechanically rewritten proprietary behavior;
- secrets, credentials, private keys, cookies, or production endpoints.

Use synthetic fixtures and public sources. If public material materially shapes
a decision, record the source and the project's independent reasoning.

## AI assistance

- Treat generated code as untrusted until read, explained, and tested.
- Disclose material assistance in the pull request.
- Do not submit dependencies or copied snippets without checking provenance and
  licensing.
- Document concise rationale, alternatives, and evidence; never publish private
  chain-of-thought.
- Stop when a requirement, ownership boundary, or safety property is unclear.

## Git discipline

- Keep `main` releasable and use short-lived branches.
- Separate refactoring from behavior changes when practical.
- Do not force-push shared branches.
- Do not commit build output, local environments, secrets, or editor state.
- Preferred commit types are `feat`, `fix`, `test`, `perf`, `refactor`, `docs`,
  `build`, `ci`, `chore`, and `experiment`.

## Documentation

- Explain why and boundaries; do not restate obvious code.
- Update the README when user-visible commands or guarantees change.
- Supersede old ADRs instead of rewriting history.
- End each milestone with result, evidence, surprises, and revisions.
