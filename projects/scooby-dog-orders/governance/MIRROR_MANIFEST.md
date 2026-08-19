# Portable mirror provenance

Status: **current**  
Synchronized: **2026-08-19**  
Engineering-handoffs base: `f1aff34521884b5e80fc06f0b346d08e40458665`

This manifest records the sources used to derive the portable contract. Files under the canonical
workspace root are not in a Git repository, so SHA-256 identifies the reviewed content.

| Canonical source                                                         | Reviewed revision/hash                                                                                                                | Derived content                                                                           |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| `/home/andreloiola/framixor/AGENTS.md`                                   | `7a370171930c09085e5a0ab4617aad2b334c4dba675009b4aeb11562b46636ab`                                                                    | authority, preflight, platform stop rules, environment safety                             |
| `/home/andreloiola/framixor/governance/REPOSITORY_MAP.md`                | `905d0387c02df0131459535dee4870f251165a21d4a578556277e48d77f9f185`                                                                    | official repos and canonicality principles; dated SHAs were not mirrored as current facts |
| `/home/andreloiola/framixor/governance/AGENT_EXECUTION_CONTRACT_PLAN.md` | `51aae32f0ebf85891f454ef65866c1beb7446910ec2287a8b62629e35ffb6402`                                                                    | product boundaries, gates and bounded slices                                              |
| `framixor/scooby-dog-orders#26`                                          | private issue synchronized 2026-08-19T21:39:51Z                                                                                       | active scope, terminal acceptance and customer-success configuration boundary             |
| `framixor/scooby-dog-orders`                                             | `develop@6a1e8752e47684ae82cd4f4636e773e0c9def183`                                                                                    | product architecture, branding and current integration snapshot                           |
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
