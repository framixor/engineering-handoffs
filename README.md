# Framixor Engineering Handoffs

Versioned implementation and reconciliation contracts for Framixor projects.

This repository is **not** the canonical source of product code and is not a Lovable sync target.
Each handoff points to a target repository and verified baseline, then provides deterministic
artifacts for an implementation agent to reconcile into that repository.

## How to consume a handoff

1. Open the target project under `projects/`.
2. Read its `CURRENT.md`; do not assume the latest directory name is active.
3. Read every file referenced by `CURRENT.md` before changing product code.
4. Fetch the target repository and verify its current baseline.
5. Preserve non-conflicting remote work and stop on genuine semantic conflicts.
6. Reconcile the approved artifact faithfully; do not treat it as design inspiration.
7. Run the target repository's own gates and acceptance checks.

See [HANDOFF_PROTOCOL.md](standards/HANDOFF_PROTOCOL.md) and
[GIT_SYNC_GUARDRAILS.md](standards/GIT_SYNC_GUARDRAILS.md).

## Projects

- [Scooby Dog Orders](projects/scooby-dog-orders/README.md)

## Security

This is a public repository. Never publish secrets, environment files, production identifiers,
customer data, database dumps or private operational notes. See [SECURITY.md](standards/SECURITY.md).
