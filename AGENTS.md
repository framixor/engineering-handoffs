# Agent instructions

- Treat this repository as a handoff catalog, never as canonical product source code.
- For the generated engineering entrypoint, consume `HANDOFF_ENGINEERING.json` or its generated
  Markdown rendering and load only task-relevant authoritative references. Before executing a
  dated/active slice, still read `CURRENT.md` and every file it references.
- Always fetch and inspect the target repository before planning or implementation.
- A baseline mismatch requires reconciliation; never overwrite newer remote work blindly.
- Do not redesign or reinterpret an approved UI unless the handoff explicitly authorizes it.
- Do not push, open a PR, deploy or mutate external systems unless the user explicitly authorizes it.
- Never add credentials, `.env` contents, production data, private customer data or access tokens.
- Keep dated handoff directories immutable. Publish a new dated handoff and update `CURRENT.md`.
- Report actual gate results; do not preserve stale hardcoded test counts in living documents.
