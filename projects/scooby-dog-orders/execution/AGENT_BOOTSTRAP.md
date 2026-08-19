# Agent bootstrap — Scooby Dog

Use this contract at the start of every Lovable/Codex/external-agent round.

1. Read `projects/scooby-dog-orders/README.md` and follow its complete reading order.
2. Read portable guardrails, manifest, `STATE.md`, `CURRENT.md`, the active slice and applicable
   governance in `framixor/scooby-dog-orders`.
3. Before editing, report:
   - repository and remote;
   - branch and exact HEAD, when available;
   - worktree clean/dirty state, upstream and ahead/behind, when available;
   - target issue/PR;
   - target environment and possible external effects;
   - bounded stream;
   - allowed and forbidden scope;
   - Supabase boundary;
   - exact Git/promotion authority granted in the current round.
4. If the issue is private, attempt direct access and report whether it succeeded. Clearly label
   facts read from GitHub versus facts supplied by the prompt/public mirror. Do not invent missing
   issue content.
5. Do not alter code until the preflight is complete.
6. Execute only the slice pointed to by `CURRENT.md`, unless the current user explicitly selects a
   different slice.
7. Do not infer authority from a handoff, branch access, tool permission or environment visibility.
8. Do not improvise architecture. Report conflicts and stop the conflicting portion.
9. Follow only the round-specific authorization for commit, push, PR, merge, deployment and
   environment operations. This bootstrap grants none of them.
10. PROD is deny-by-default. Never mutate Supabase, schema or migration state unless that exact
    operation and environment were explicitly authorized.

**Agents execute Framixor governance; they do not redefine it.**
