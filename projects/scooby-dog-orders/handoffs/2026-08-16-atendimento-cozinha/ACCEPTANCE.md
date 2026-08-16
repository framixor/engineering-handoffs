# Acceptance — Atendimento + Cozinha

- `Precisa de ação` contains only directly actionable front-counter orders.
- Aging alone never promotes confirmed/preparing orders into that queue.
- New, attention and overdue remain visually distinct.
- `Em andamento` retains aging and urgency without competing with the primary queue.
- Pickup never receives a delivery action.
- Kitchen preserves FIFO, visible customizations and only preparation actions.
- Ready orders are compact kitchen handoff without delivery/pickup completion CTA.
- Mobile around 390px and tablet landscape have no required horizontal navigation scroll.
- Drawer close does not overlap title or status.
- Demo reset begins with one overdue order and does not place several orders immediately next to
  the 30-minute threshold.
- Domain, state machine, repository, storage `v5` and backend remain unchanged.

Run the target project's complete CI sequence and report the actual results.
