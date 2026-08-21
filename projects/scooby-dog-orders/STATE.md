# Scooby Dog Orders — current snapshot

> Snapshot verified: **2026-08-21**. This file is dated evidence, not promotion authority. Recheck
> GitHub before execution; the official repository wins if any value has changed.

| Fact                       | Snapshot                                               |
| -------------------------- | ------------------------------------------------------ |
| Official repository        | `framixor/scooby-dog-orders`                           |
| Integration branch         | `develop`                                              |
| `develop` at review        | `74fd3cb6ad2cc0ad75ae55ab5a8a7c295e235596`             |
| `main` at review           | `a218bc2c8b5f6abfe7e51f44c1c29363b812701a`             |
| Recorded deployment        | Production success at the same `main` SHA              |
| Custom domain              | `scoobydogpc.com.br`, configured in Framixor Vercel    |
| Public accessibility       | DNS resolves; canonical HTTPS endpoint returns `200`   |
| Business go-live           | confirmed by maintainer                                |
| Active slice               | none; next task requires explicit selection            |
| Repo-scoped bootstrap      | `docs/AGENT_BOOTSTRAP.md` in the product repository    |
| PROD mutation authority    | deny-by-default                                        |

The product repo is the source of truth for code and domain behavior. The canonical shared backend
repo is `framixor/framixor-supabase`; the frontend repo does not own migrations, RLS, grants, RPCs,
policies, tables, functions or migration leases.

Lovable is the concrete repo-scoped integration validated in this snapshot, but the adapter is
agent-agnostic. Any agent is an executor, not an architectural authority. TEST, STAGING and PROD are
different environments. A branch or environment visible to an agent does not authorize promotion
or mutation.

| Issue | Implementation/Promotion Status | Issue Workflow Status |
| --- | --- | --- |
| #21 | anonymous PIX correction promoted | open |
| #25 | authoritative delivery pricing promoted | open |
| #26 | tracker/customer success promoted | closed |
| #27 | catalog/admin base promoted; real-content acceptance pending | open |
| #29 | domain/deployment and business go-live confirmed; remaining criteria not inferred | open |
| #40 | driver registry and order-association seam promoted | open |

Issue workflow and implementation/promotion are independent dimensions. Neither is inferred from
the other.

No secret, Supabase project ref or credential is recorded here. This snapshot does not authorize a
commit, a deploy, `develop → main`, database changes or PROD access.
