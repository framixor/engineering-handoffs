# Portable mirror provenance

Status: **current; human-reviewed 2026-08-21**

Synchronized: **2026-08-21**

Engineering-handoffs base: `f1ea75c44cf6385136e248c3a0248fe24dd74d36`

This manifest records the sources used to derive the portable contract. Files under the canonical
workspace root are not in a Git repository, so SHA-256 identifies the reviewed content.

| Canonical source                                                         | Reviewed revision/hash                                                                                                                | Derived content                                                                           |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| `/home/andreloiola/framixor/AGENTS.md`                                   | `6954f34f6f88cb72298ecf6db30dc8762bbb241ba883009490dcbe031fdc6eab`                                                                    | authority, preflight, platform stop rules, agent interchangeability and portability       |
| `/home/andreloiola/framixor/governance/REPOSITORY_MAP.md`                | `914ebafba3db2563bc3fb3b3bca64bb7768194a6c6040e555ceafda3f6161303`                                                                    | official repos, canonicality, promotion and deployment-accessibility snapshot             |
| `/home/andreloiola/framixor/governance/AGENT_EXECUTION_CONTRACT.md`      | `c1b60828ac6e2ece5b3ab0a82b5cd38caf65fc6f963d57374874cd5a2e7f0212`                                                                    | execution flow, gates, context efficiency and firebreaks                                  |
| `/home/andreloiola/framixor/governance/FRONTEND_VISUAL_CONTRACT.md`      | `71bb965d0b492ee082487695158425e23d7aa9f05f1e6af59dabf3dcf5d909eb`                                                                    | existing-product-first visual process, foundation, discovery and modeling                 |
| `framixor/scooby-dog-orders#26`                                          | issue closed 2026-08-20T16:32:28Z                                                                                                    | historical scope; no longer active                                                        |
| `framixor/scooby-dog-orders`                                             | `main@a218bc2c8b5f6abfe7e51f44c1c29363b812701a`; `develop@74fd3cb6ad2cc0ad75ae55ab5a8a7c295e235596`                                | promoted product state, local governance and repo-scoped adapter                          |
| GitHub/Vercel deployment + custom domain                                 | deployment `6012816725`, Production `Ready` at `a218bc2c8b5f6abfe7e51f44c1c29363b812701a`; `scoobydogpc.com.br` configured, DNS resolving and HTTPS public `200`; business go-live confirmed by maintainer | commit alignment, public reachability and operational confirmation |
| `framixor/framixor-supabase/rules/migration-numbering.md`                | repo `main@b058fa93d0ca464a73df53c0a772ed8479c245c7`; file SHA-256 `31a1d5669aa07073534031c5895eb040426760661d3c0b8883ea55da22dfdbbe` | sibling streams and ownership ranges                                                      |
| `framixor/framixor-supabase/rules/migration-lease.md`                    | repo `main@b058fa93d0ca464a73df53c0a772ed8479c245c7`; file SHA-256 `a71672dad0d1b94deb5fde195924a523c38df1893966cc5217687df36fb76d6d` | lease must be consulted, never inferred from mirror                                       |

## Drift rule

Canonical maintainers compare these hashes/revisions during each mirror update. If a canonical hash
or Git revision differs, set this manifest to **review-required** and review the semantic delta.
Never copy changes automatically. A newer product branch alone does not invalidate stable
guardrails, but it does make `STATE.md` stale until reverified.

External agents that cannot run the hash comparison must report the recorded synchronization date
and validate all Git facts they can access. Conflict rule: canonical governance and official repos
win; the agent stops rather than improvising.
