# Git synchronization guardrails

Before every audit, plan or implementation against a target repository:

```bash
git status --short --branch
git fetch --all --prune
git rev-parse --abbrev-ref HEAD
git rev-parse HEAD
git rev-parse <upstream>
git rev-list --left-right --count HEAD...<upstream>
```

Report branch, local HEAD, upstream HEAD, ahead/behind/diverged and clean/dirty state.

`git fetch` updates references only. Do not automatically run pull, merge, rebase, reset, stash,
force-push or destructive checkout. If local and remote diverge, stop mutation until the working
source and preservation strategy are explicit.

Never rewrite history published to a Lovable-connected branch.
