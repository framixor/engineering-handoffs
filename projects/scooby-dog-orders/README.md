# Scooby Dog Orders — start here

> **Governed portable mirror.** This directory records reviewed derived context. It does not replace
> canonical workspace governance, the source issue, or the official product repository.

Official product repository: [`framixor/scooby-dog-orders`](https://github.com/framixor/scooby-dog-orders).
GitHub and that repository remain authoritative for promoted code and behavior. If this mirror
conflicts with current Git, deployment evidence or canonical Framixor governance, stop and report
the conflict.

Repo-scoped external agents must be able to bootstrap from `docs/AGENT_BOOTSTRAP.md` inside the
product repository without reading this sibling repository. This mirror supports review,
provenance and richer handoffs; it is not a runtime dependency of that bootstrap.

## Generated engineering entrypoint

- [`HANDOFF_ENGINEERING.json`](HANDOFF_ENGINEERING.json) is the machine-readable derived contract.
- [`HANDOFF_ENGINEERING.md`](HANDOFF_ENGINEERING.md) is generated deterministically from that JSON.

External executors may start with either representation and then load only the task-relevant
authoritative references it identifies. Neither artifact grants authority to modify Git, product
code, environments or data.

The manual `MIRROR_MANIFEST.md`, `PORTABLE_GUARDRAILS.md`, bootstrap and dated handoffs remain
preserved for historical reconciliation and active-slice workflows. They are planned for later
deprecation as the general external entrypoint, but are not removed or rewritten in this slice.

## Mandatory reading order for mirror consumers

Before editing product code, read completely:

1. [`governance/PORTABLE_GUARDRAILS.md`](governance/PORTABLE_GUARDRAILS.md)
2. [`governance/MIRROR_MANIFEST.md`](governance/MIRROR_MANIFEST.md)
3. [`STATE.md`](STATE.md)
4. [`CURRENT.md`](CURRENT.md)
5. the active slice linked by `CURRENT.md`, if one exists
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
