# Scooby Dog Orders — start here

> **Operational mirror.** This directory makes the minimum Framixor governance available to agents
> that cannot read `/home/andreloiola/framixor`. It does not replace canonical workspace governance,
> the private GitHub issue, or the official product repository.

Official product repository: [`framixor/scooby-dog-orders`](https://github.com/framixor/scooby-dog-orders).
GitHub and that repository remain authoritative for promoted code and behavior. If this mirror
conflicts with current Git, deployment evidence or canonical Framixor governance, stop and report
the conflict.

## Mandatory reading order

Before editing product code, read completely:

1. [`governance/PORTABLE_GUARDRAILS.md`](governance/PORTABLE_GUARDRAILS.md)
2. [`governance/MIRROR_MANIFEST.md`](governance/MIRROR_MANIFEST.md)
3. [`STATE.md`](STATE.md)
4. [`CURRENT.md`](CURRENT.md)
5. the active slice linked by `CURRENT.md`
6. [`execution/AGENT_BOOTSTRAP.md`](execution/AGENT_BOOTSTRAP.md)
7. `AGENTS.md`, `BRAND.md`, `REUSE.md`, `STATE.md` and other applicable contracts in the product repo

Then report repository, branch, HEAD, worktree state, upstream, environment, bounded stream and the
allowed/forbidden scope. Do not edit until that preflight is complete.

## Historical handoffs

Directories under [`handoffs/`](handoffs/README.md) are immutable historical evidence. They are not
current merely because they contain a complete patch. Execute one only when `CURRENT.md` explicitly
activates it.

Agents execute Framixor governance; they do not redefine it. This mirror never grants permission to
commit, merge, deploy, mutate a database or touch PROD. Those actions require explicit authority in
the current execution round.
