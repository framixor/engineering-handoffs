# Falcon 9 — Frontend parity and review evidence

2026-10-18, America/New_York. **READY for code review; CONDITIONAL for independent STAGING homologation; NOT READY for Marley cutover.**

## Baseline identity

| Reference | Branch / commit / version |
|---|---|
| Golden Reference, local read-only source | Prime `main@0d05ae1caf4271ea4c91f207d290ba95a1016ad9`, application **1.33.1** |
| Earlier Framixor frontend base | `main@52ae656703c6d831c3d42794a67dd8af655429c9` |
| This V2 candidate | `codex/falcon9-parity-local-20261018`; implementation commit `884320b2`; own prerelease label **2.0.0-falcon9** |
| Backend | `framixor/framixor-supabase`, same feature branch, isolated `v2/` stream |

The initial candidate mixed the older base with selective ports. Business pages and their component dependencies now use the current 1.33.1 baseline, with native contract adapters. `src/version.ts`, Settings → About and the sidebar identify the V2 separately from its Prime reference. This is a **local source baseline**, not proof of what Marley published in production.

## Pages, navigation and workflows

| Area | What was aligned / validated | Evidence limits |
|---|---|---|
| Navigation | Current Directory, Operations, Customer Billing, Expenses, Reports, Financial and Owners & Capital groups; Framixor shell and mobile menu retained | 28 compiled routes load, but route count is not a visual or workflow certification |
| CRM / Properties / Catalog | Current list and detail pages and catalog picker; client create/edit tested with real dialogs | Property/catalog create/edit via native API plus UI reads; all form variants remain UAT |
| Estimates | Current filters/families, header, ten editor tabs, Scope/Overview, pricing, client discount note, itemization visibility, revision and Share layout | Real create-and-continue, rich Scope save, display controls and native revision cloning exercised; not every pricing/CT variant |
| Public estimate | Current document component with Falcon token/acceptance semantics | Anonymous UI selected and accepted **$1500**; persisted and frozen totals agree; internal discount note absent from page |
| HIC / Jobs | Current project/change-order presentation and CT/generic documents; native HIC lifecycle retained | Compiled draft/ready, two signatures, down-payment and signed-copy PDF exercised; all scheduling controls remain UAT |
| Invoices / Documents | Current wizard, readiness, payment and public print document | Actual issue-without-email, payment, anonymous PDF and privacy checks pass |
| Expenses / Purchases / Vendors / Banking | Current entry screens, allocation destinations, line calculations, catalog picker and reconciliation dialogs | Relevant pages load and purchase/expense presentation reviewed; complete banking reconciliation remains UAT |
| Capital / Closing / Distribution | Current company result, partner positions, equalization and detailed printable reports | Compiled screens visually reviewed and monthly report loads. Completed financial audits are reused, not repeated |
| Settings / Admin / Recovery | Current grouped navigation; native company, team, branding and recovery screens; own About metadata | Team directory and tenant archive/preview/cancel exercised. V1-only UI branches removed |

Essential presentation references: `src/lib/navigation.ts`, authenticated `estimates.$id.tsx`, `estimates.index.tsx`, `configuracoes.tsx`, `distribuicao.tsx`; `EstimateScopeSection`, `EstimatePricingSection`, `DistributionLayeredOverview` and `ProjectDistributionDetailSection`.

## Visual evidence

The browser captured **21 synthetic views** at desktop 1440px and mobile 390px, plus the anonymous acceptance page. Review inspected the current editor Scope/Pricing, purchase entry, distribution and About desktop/mobile images for structure, readability, navigation and Framixor identity. The highlighted total's contrast and the NON-PROD banner's spacing were corrected. Captures wait for responsive transitions to settle.

This is visual and interaction evidence for the V2, compared with the Golden Reference's page/component structure. **No Marley production browser session or pixel-by-pixel production comparison occurred.** Fonts/providers were blocked or mocked; hosted fonts, printers, all device variants and complete business UAT remain unverified.

## Exclusive native contracts and V1 boundary

- `framixor-env.ts` now refuses Apollo and incompatible schemas. Hosted environments require explicit `VITE_FRAMIXOR_BACKEND=falcon9`; native schema is `public`.
- `framixor-schema.ts` compatibility helper names both resolve to that native schema. The V1 admin/company/public-invoice branches and unused forced-password UI were removed.
- The tracked donor `.env` was deleted. Explicit independent endpoints and server-only credentials are required; no donor endpoint or key value remains in candidate files.
- Native FK aliases, session-derived member directory and tenant-prefixed Storage paths replace single-tenant query/path assumptions.
- Three additive local migrations close reproduced UI contract gaps: **4558** rich Project Details, **4559** optional client discount text/visibility, **4560** material/labor display flag. They change no existing financial calculation. Next Prime/Flooring number: **4561**; Platform **4007** remains reserved.
- **153 literal write contracts** were compared with the local native table catalog: no missing fields after corrections. This does not cover dynamically assembled objects or prove all RPC behavior.
- Explicit environment values can still be misconfigured by an operator. The local runtime's infrastructure isolation, rather than a banner, established safety for these tests.

Existing V1/Apollo checkouts and shared hosting configurations remain separate. **Never convert existing V1 STAGING by applying this migration stream.** Homologation needs a compatible independent destination and later authorization.

## Validation

- Compiled Nitro **node-server** build: PASS; all compiled source hashes match the implementation worktree.
- Typecheck: PASS. Vitest: **206 tests / 27 files PASS**.
- Changed TS lint: **310 files, 0 errors, 77 warnings**. The known full-repository formatting backlog was not reformatted or represented as a clean full lint gate. No Actions workflow is installed in this repository at this checkpoint.
- Endpoint firebreak tests: **9 PASS** (both backend test files).
- New frontend parity browser suite: **8 PASS**, including ten tabs, persisted Scope, client display controls, $1500 acceptance, rich revision, responsive views and native team directory; zero native API or unhandled page errors in its final run.
- Navigation: **28/28 PASS**. Client dialog create/edit: **1 PASS**. Property/catalog API + UI read and monthly closing: **2 PASS**.
- Compiled HIC: **3 PASS**; invoice/payment/public document/backup UI: **4 PASS**.
- Browser assets: **257 checked, 0 privileged-key matches**. No credential values published.

The existing import/RLS/financial/recovery audit remains in the consolidated handoff. It is not recounted as new frontend test evidence. QA used fresh synthetic tenants in the preserved internal Docker stack, with only loopback frontend exposure; no remote database, Marley runtime/Auth/Storage, real email, webhook or scheduler was used.

## Remaining differences and activation gates

- Branding, tenant identity/permissions, token semantics, team administration, backup/recovery and About use independent Framixor implementations. Donor global restore, Auth profiles, private email preview, migration journal and donor release changelog are not copied.
- **P2 local gap:** native alert feed implements the eleven business alerts; three scheduler/backup-monitor alerts remain unavailable and their preferences are visibly disabled. No scheduler is activated.
- Hostinger, Google and AI use existing own adapters. Mocked runtime works; real credentials, delivery, quotas, latency and hosted origins are unverified. No demonstrated gap requires Lovable Bridge. The existing Lovable build preset remains a build dependency; legacy connector opt-in stays unconfigured.
- Cutover still requires current consistent relational input, real user provisioning, historical Storage binaries and executed documents. The existing 2026-09-19 snapshot is older than the code baseline; no new PROD export was requested.
- Choose/validate hosting: Node runtime is proven locally; Cloudflare runtime is not certified. Configure origins, redirects, CORS/CSP and providers only after independent STAGING authorization.

The review branch disables its automatic Vercel Git deployment through `vercel.json`; unspecified branches retain their existing setting. [Vercel branch configuration](https://vercel.com/docs/project-configuration/git-configuration). No merge, deploy or remote migration/import is part of these PRs.
