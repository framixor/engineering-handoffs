# Scooby Dog Orders — current snapshot

> Snapshot verified: **2026-08-19**. This file is dated evidence, not promotion authority. Recheck
> GitHub before execution; the official repository wins if any value has changed.

| Fact                       | Snapshot                                               |
| -------------------------- | ------------------------------------------------------ |
| Official repository        | `framixor/scooby-dog-orders`                           |
| Integration/Lovable branch | `develop`                                              |
| `develop` at review        | `6ac53a1271311153992c10d29a89288698dd2cb7`             |
| `main` at review           | `86269f0df528d9c313efa46033813487bb4f66e7`             |
| Active slice               | Issue #26 — Customer success + tracking polish         |
| Known Lovable backend      | Supabase STAGING, using existing client-safe contracts |
| PROD                       | deny-by-default                                        |

The product repo is the source of truth for code and domain behavior. The canonical shared backend
repo is `framixor/framixor-supabase`; the frontend repo does not own migrations, RLS, grants, RPCs,
policies, tables, functions or migration leases.

The known Lovable workspace is an executor on `develop`, not an architectural authority. TEST,
STAGING and PROD are different environments. A branch or environment visible to an agent does not
authorize promotion or mutation.

No secret, Supabase project ref or credential is recorded here. This snapshot does not authorize a
commit, a deploy, `develop → main`, database changes or PROD access.
