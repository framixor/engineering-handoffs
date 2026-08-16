# Final reconciliation brief for Lovable — Atendimento + Cozinha

## Authority and baseline

The locally approved UI is the visual and operational source of truth for this reconciliation.

- Remote baseline verified after `git fetch --all --prune`: `origin/main` at `d884a93bd021dabb209c4ede18881e549aa6c5fc`.
- Approved local worktree uses that exact baseline; the remote was `0 ahead / 0 behind` at handoff time.
- Exact approved delta: `DOCS/APPROVED_UI_RECONCILIATION.patch`.
- Patch SHA-256: `3e45e02efe6722fd3bd562010e7c701bbee1b2970a662f170619217f4b8d1fad`.

> Do not redesign, reinterpret, “improve,” or replace the approved composition. Reproduce the approved behavior and visual hierarchy faithfully. Preserve any newer remote change that does not conflict. If the remote baseline has changed, reconcile per file and stop on a genuine semantic conflict instead of guessing.

## Objective

Reconcile the approved local `Atendimento + Cozinha` implementation into the current Lovable branch, preserving the existing domain and all unrelated behavior.

The approved result provides:

- Atendimento centered on actionable orders, not elapsed time alone;
- aging and urgency visible in `Em andamento` without creating false front-counter action;
- compact operational cards with localized urgency and clear primary actions;
- Kitchen FIFO with distinct Queue/Preparing sections, item/customization prominence and compact Ready handoff;
- Scooby Dog warm cream/yellow visual identity without generic SaaS/neon styling.

## Deterministic application order

1. Fetch/read the current remote branch and confirm its HEAD.
2. Compare it with baseline `d884a93`.
3. Apply or reproduce the complete approved changes in `DOCS/APPROVED_UI_RECONCILIATION.patch` as coherent file-level units.
4. Do not split the UI into a sequence of speculative micro-redesigns.
5. Apply only the demo-time adjustment specified below to `src/data/mock/seed-orders.ts`.
6. Run the complete gates.
7. QA `/owner` and `/admin/pedidos` against the approved behavior.

## Approved file units

### `src/lib/order/operational-view.ts`

Preserve the complete selector change from the patch:

- `FrontCounterReasonKind` contains only `confirm`, `pickupWaiting`, `deliveryWaiting`.
- `frontCounterReasonOf(order)` is based only on direct Atendimento actionability.
- `needsAction(order)` does not accept/use time.
- `selectNeedsAction()` includes actionable orders only.
- `selectInProgress()` keeps other active orders even when attention/overdue.
- Urgency remains independently derived from `createdAt` at 15/30 minutes.
- Do not add aging back as an action reason.

### `src/lib/order/operational-view.test.ts`

Preserve the complete test change from the patch:

- normal and overdue `confirmado` do not enter `Precisa de ação`;
- overdue `preparando` does not enter merely due to age;
- those orders remain in `Em andamento` with derived urgency;
- actionable reasons, pickup/delivery transitions, FIFO and non-mutation remain protected.

### `src/components/owner/FrontCounterOrderRow.tsx`

Use the complete approved component delta from the patch. Preserve:

- separate visual signals for new, status and urgency;
- compact card composition;
- localized accent bar rather than full overdue border;
- high-priority order/customer/reason/timer hierarchy;
- dominant primary CTA;
- Details and WhatsApp as secondary actions with accessible names and 44px touch targets;
- brief/static new-order treatment already supplied by existing `.order-new` CSS;
- calmer treatment when `secondary` is true.

### `src/components/owner/OwnerFrontCounterView.tsx`

Use the complete approved component delta from the patch. Preserve:

- compact clickable KPIs with integrated selected state;
- no separate large “Filtro ativo” row;
- dominant warm `Precisa de ação` operational region;
- responsive action-card grid;
- visually calmer `Em andamento` section;
- existing search and history behavior.

### `src/components/owner/KitchenTicket.tsx`

Use the complete approved component delta from the patch. Preserve:

- FIFO position, `orderRef` and timer hierarchy;
- status top accent independent from urgency;
- localized attention/overdue timer treatment, never a full red border;
- item quantities, additions, removals and notes fully visible;
- primary kitchen CTA only;
- no administrative or financial surface.

### `src/components/owner/OwnerKitchenView.tsx`

Use the complete approved component delta from the patch. Preserve:

- mobile segments;
- two simultaneous tablet/desktop sections;
- warm Queue section and subtle teal Preparing section from the same brand system;
- compact Ready handoff with no delivery/pickup completion CTA;
- no horizontal navigation scroll or masonry ordering.

## Only additional change: commercial demo timing

Update only the `minutesAgo(...)` values and their adjacent factual comments in the nine live orders in `src/data/mock/seed-orders.ts`. Do not alter order shape, ids, refs, content, statuses, history, storage key or storage version.

Use this stable distribution at reset time:

| Order | Status | Approved age |
|---|---|---:|
| X01 | novo | 3 min |
| X02 | novo | 7 min |
| X03 | confirmado | 12 min |
| X04 | preparando | 8 min |
| X05 | preparando | 18 min |
| X06 | preparando | 36 min |
| X07 | pronto pickup | 10 min |
| X08 | pronto delivery | 20 min |
| X09 | saiu_para_entrega | 14 min |

Keep activity timestamps internally coherent and no later than their order age. The demo should start with:

- normal, attention and overdue represented;
- exactly one overdue order immediately after reset;
- enough distance from the 30-minute threshold that several orders do not become overdue during a normal screenshot/QA session.

This is demo fixture timing only. Do not change the 15/30-minute UI heuristic.

## Invariants

Preserve without modification:

- `Order`, `OrderStatus` and fulfillment semantics;
- one state machine and `ownerNextStatus()`;
- pickup never receives `saiu_para_entrega`;
- same query, mutation, timer and repository seam;
- activity, `orderRef`, `publicTrackingId` and public tracking;
- localStorage `scooby-dog-orders/v5`;
- drawer and structurally reserved close-button area;
- search, KPIs, history, WhatsApp and printing;
- checkout and public pages;
- loading/error/pending behavior;
- AdminShell and current responsiveness.

Do not add Supabase, backend, realtime, auth/roles, new dependencies, stores, queries, timers, persisted preferences, SLA, stage age or a new state machine.

## Required behavior

### Atendimento

- `Precisa de ação`: only `novo`, pickup `pronto`, and delivery `pronto`.
- `confirmado` and `preparando` never enter solely because of attention/overdue.
- Non-actionable active orders remain in `Em andamento` and retain timer/urgency.
- New, attention and overdue remain visually distinct.
- Primary CTA dominates; Details/WhatsApp remain accessible and secondary.
- KPI filtering, search and history continue to work.

### Cozinha

- Queue contains `confirmado`, FIFO.
- Preparing contains `preparando`, FIFO.
- Ready contains `pronto` as handoff only.
- Kitchen actions remain only `Iniciar preparo` and `Marcar pronto`.
- No confirmation of new orders and no delivery/pickup completion actions.
- Items and all customizations remain visible without the drawer.

### Responsive QA

Validate at approximately 390px, 768px, 1024px, 1366×768 and wide desktop:

- no horizontal navigation scroll;
- no card/timer overlap;
- no broken CTA labels;
- secondary toolbar does not dominate mobile;
- minimum touch targets remain approximately 44px;
- Kitchen FIFO remains visually unambiguous in tablet landscape;
- drawer close does not overlap title/status.

## Gates

Run in CI order:

```bash
bun run format:check
bun run lint
bun run typecheck
bun run test
bun run build
```

Expected baseline before new seed-specific assertions: 81 passing tests. Report the actual runner total rather than hardcoding it in living documentation.

## Acceptance criteria

- Approved file patch is reproduced faithfully, with no unsolicited redesign.
- Actionability and aging remain separate.
- Only one or two demo orders are overdue immediately after reset; the specified fixture yields one.
- Atendimento reads as a restaurant command center, not an administrative table.
- Cozinha preserves FIFO, production readability and touch operation.
- Scooby Dog cream/yellow identity remains recognizable without the logo.
- Domain, state machine, repository, storage v5 and backend are unchanged.
- Unrelated remote changes are preserved.
- All gates pass and quick responsive QA matches the approved local reference.

## Explicit non-goals

- No further visual exploration or “wow” pass.
- No redesign of other pages.
- No backend/Supabase work.
- No transition enforcement refactor.
- No `pendingId` concurrency refactor.
- No storage audit/version bump.
- No codebase language normalization.
- No manual/WhatsApp order intake.
- No new operational features.
