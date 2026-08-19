# Issue #26 — Customer success + tracking polish

## Identity and source

- Issue: `framixor/scooby-dog-orders#26`
- Title: **Customer success + tracking polish**
- Bounded stream: **Framixor Commerce / Scooby Dog**
- Type: frontend / UX / customer success / tracking polish
- Mirror synchronized: **2026-08-19**
- Product base observed: `develop@6a1e8752e47684ae82cd4f4636e773e0c9def183`

This is the public execution mirror for a private GitHub issue that Lovable cannot read directly. It
does not replace the private issue or the product repository. The functional issue text plus the
explicit Tech Lead/product decisions synchronized in this contract form the current execution
scope. If a later private issue update, explicit product decision or current Git state conflicts,
report it before implementation; do not choose silently.

The SHA above is a dated observation, not a permanent implementation base. Recheck `develop` before
the implementation round.

## Outcome and invariants

Polish post-order success and public tracking so the customer immediately understands the current
stage, completion and next useful action.

Preserve without change:

- `OrderStatus`, lifecycle and transition semantics;
- token-scoped public tracking;
- backend/Supabase contracts and server authority;
- delivery pricing, Pix, Google Maps and order creation behavior;
- cancellation as a distinct terminal state;
- existing ports/adapters and shared Commerce architecture;
- no customer account/history capability invented by this slice.

## Functional scope

- Improve the order-success experience and public tracker.
- Keep **Acompanhar meu pedido** as the primary post-creation action.
- Keep WhatsApp visually secondary and truthful; opening it does not prove message delivery.
- Keep **Fazer outro pedido** subordinate.
- Refine the full journey: Recebido → Confirmado → Na chapa → Pronto → A caminho → Entregue.
- Preserve the appropriate pickup terminal copy/state.
- Delivered must visually terminate the journey; no forward-looking state or ETA follows it.
- Preserve readable labels, timestamps, status semantics and `prefers-reduced-motion`.

## Approved visual direction

These are requirements, not loose inspiration.

### Progress rail

- Timeline remains horizontal, including mobile.
- Base rail is neutral gray; reached progress is yellow while the order is active.
- Nodes and icons render in front of the rail; the line never crosses over them.
- Future stages remain neutral.
- Preserve readable labels and journey context. Do not proportionally shrink the whole tracker until
  type, nodes or timestamps become illegible; adapt spacing/composition while staying horizontal.

### Active-stage hero

- The decorative hero is directly associated with the active stage and sits above its corresponding
  node.
- No giant standalone hero card and no illustration floating disconnected from the rail.
- Textual status and node semantics remain the source of truth.

### Na chapa

- Hot dog is the protagonist.
- Strong visual emphasis and an unmistakable preparation feeling.
- Motion/steam is restrained and never required to understand the stage.

### Pronto

- Use package, wrapping or packed-order language.
- Communicate readiness, not travel.

### A caminho

- Use motorcycle/scooter/delivery language with a subtle sense of travel.
- Motion is decorative, short/restrained and disabled under reduced motion.
- It has no Maps, GPS or live-driver meaning.

### Entregue

- Celebratory terminal state.
- Do not create or require a new Scooby-Doo asset for this slice.
- Reuse the existing animated/pulsing hot dog as the terminal hero.
- Add an unmistakable green success check/badge overlaid on or clearly associated with the hero.
- `public/logo.png` is an identity reference, not the tracker hero; do not use the complete logo as
  a substitute.
- Completed rail/nodes switch to success green, while the surrounding page/tracker surface remains
  light.
- Final node is dominant, contains a clear check and has no visual continuation after it.
- The hot dog success animation may be adapted, but must respect `prefers-reduced-motion`.
- Completion copy remains prominent and no visual continuation follows the final node.

**Dedicated Scooby-Doo delivery artwork is deferred future polish and is not required to close
Issue #26.** The tenant-specific Scooby Dog brand boundary remains valid; this decision only reduces
the acceptance scope of this slice.

### Avoid

- vertical tracker on mobile;
- solid/massive green background;
- giant hero cards;
- rail crossing icons;
- generic SaaS tracker styling;
- excessive confetti or permanent aggressive pulsing;
- WhatsApp dominating the hierarchy;
- illustrations disconnected from the active stage.

## Customer success after delivery

Only after terminal delivery, surface configured post-order engagement without competing with
tracking while the order is active.

### Google Business

Copy:

> ⭐ Gostou da experiência?  
> Estamos também no Google — nos avalie!

CTA: **Avaliar no Google**

The destination comes from store/tenant configuration. Do not hardcode the URL in a component and
do not invent review data. For this slice, use the current public Google Maps/Business listing URL
as client-safe product configuration:

`https://www.google.com/maps/place/Scooby+Dog/@-21.7870899,-46.5501441,748m/data=!3m1!1e3!4m14!1m7!3m6!1s0x94c9dd91c06844d5:0x301d9576ae3133d0!2sScooby+Dog!8m2!3d-21.7870949!4d-46.5475692!16s%2Fg%2F11ms7lx0yr!3m5!1s0x94c9dd91c06844d5:0x301d9576ae3133d0!8m2!3d-21.7870949!4d-46.5475692!16s%2Fg%2F11ms7lx0yr?entry=ttu&g_ep=EgoyMDI2MDgxNi4wIKXMDSoASAFQAw%3D%3D`

This is a public listing URL, not a direct-review URL. Do not invent or claim a direct-review link.
It may later be replaced by an official Google Business Profile review URL. This remains product
configuration: do not create a migration, column, schema or backend contract for it.

### Instagram

Copy:

> 📸 Siga a Scooby Dog no Instagram

CTA: **Ver Instagram**

The destination also comes from store/tenant configuration, not structural component hardcoding.
If the required value is absent from an existing client-safe contract, report that gap; do not add a
database field in this slice.

## Accessibility and QA

- No meaning conveyed only by color or motion.
- Use active-step semantics such as `aria-current="step"` where applicable.
- Preserve readable contrast, labels and timestamps.
- Respect `prefers-reduced-motion` without losing stage comprehension.
- Validate success and tracker states at mobile and tablet sizes, keyboard/screen-reader semantics,
  loading/retry/error states and horizontal overflow.

## Supabase boundary for Lovable

Lovable may:

- consume existing client-safe data and contracts;
- query STAGING through the already configured frontend runtime;
- use existing public/authenticated projections within their current authorization.

Lovable may not:

- create or allocate a migration;
- change schema, tables, functions, RLS, grants, RPCs, policies or migration leases;
- use service-role credentials;
- mutate Supabase PROD.

If the frontend appears to require a backend/database change, implement only independent
frontend-safe work, report the contract gap and stop the blocked portion.

## Git and promotion boundary

This file grants no Git mutation authority. In a later implementation round, direct commit to
`develop` is allowed only if André explicitly authorizes that exact action for that round. Otherwise
use the repository's approved branch/PR flow.

- `main`: forbidden without a separate promotion authorization.
- `develop → main`: forbidden in this slice.
- PROD and PROD deploy: forbidden.
- Supabase PROD: forbidden.
- Do not merge an existing PR or rewrite published/Lovable-connected history by inference.

## Required gates and evidence

Run the product repository gates in order:

```text
bun run format:check
bun run lint
bun run typecheck
bun run test
bun run build
```

Report actual results, visual evidence for every material state/viewport, reduced-motion evidence,
files changed, branch/HEAD and the exact stop point required by the implementation authorization.
