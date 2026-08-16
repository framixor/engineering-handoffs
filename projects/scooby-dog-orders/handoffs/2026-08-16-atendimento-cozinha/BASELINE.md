# Baseline

- Target repository: `framixor/scooby-dog-orders`
- Target branch: `main`
- Validated baseline: `d884a93bd021dabb209c4ede18881e549aa6c5fc`
- Artifact type: deterministic UI reconciliation
- Approved source: local QA worktree reviewed by the product owner
- Remote comparison at handoff creation: `0 ahead / 0 behind`

Run a new fetch and comparison before execution. A changed target branch does not invalidate the
handoff automatically, but requires file-by-file reconciliation and preservation of non-conflicting
remote changes.
