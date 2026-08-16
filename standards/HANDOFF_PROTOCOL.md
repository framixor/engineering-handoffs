# Handoff protocol

## Authority

A handoff is an execution contract tied to a target repository and verified commit. It does not
replace the target repository as the source of truth for code, domain or runtime behavior.

## Required package

Each active handoff should contain:

- `BRIEF.md`: objective, scope, invariants, file responsibilities and acceptance criteria;
- `BASELINE.md`: target repository, branch and verified commit;
- a deterministic artifact such as an approved patch or complete file contents;
- `ACCEPTANCE.md`: gates and behavior to verify;
- `SHA256SUMS`: integrity of deterministic artifacts.

## Reconciliation rule

The executor must compare the target remote with the recorded baseline. If unchanged, apply the
approved artifact as a coherent unit. If changed, preserve non-conflicting remote work and report
semantic conflicts before deciding. An approved artifact is a reference implementation, not an
invitation to redesign.

## Lifecycle

Dated packages are historical and immutable. `CURRENT.md` is the sole pointer to the active
handoff. Superseding a package requires a new directory and an explicit pointer update.
