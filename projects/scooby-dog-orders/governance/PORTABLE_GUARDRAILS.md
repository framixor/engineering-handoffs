# Portable Framixor guardrails — Scooby Dog

> Operational mirror derived from canonical Framixor governance. Canonical workspace governance,
> the official product repository and current deployment evidence prevail on conflict.

## Evidence and preflight

1. Official Framixor GitHub state is primary evidence for promoted Git state.
2. Real deployment evidence identifies what is actually published.
3. Local branches/worktrees are candidates until promoted; directory names do not prove authority.
4. `STATE`, checkpoints and handoffs are dated evidence, never a substitute for current Git/runtime.
5. Before editing, report repository, branch, HEAD, clean/dirty state, upstream, ahead/behind,
   target issue/PR, environment and external effects.
6. A documentation, Git or deployment conflict must be reported, not resolved by guessing.

## Bounded execution

- Execute only the current slice and its declared files/behavior.
- Do not change shared foundation, tenancy, auth/authz, RLS, grants, privileged RPCs, schemas,
  migrations or environment contracts for local convenience.
- Product UI and behavior belong to `framixor/scooby-dog-orders`.
- Shared backend evolution belongs to `framixor/framixor-supabase`.
- Commerce and Apollo/Construction are sibling streams. Commerce never depends on Apollo-owned
  schemas or migration ranges.
- When backend work is authorized, read the current numbering and lease contracts first. A number
  seen in this mirror is never an allocation.

## Environments and Supabase

- TEST, STAGING and PROD have different semantics and credentials.
- Git containing a migration and a database having applied it are different facts.
- PROD is deny-by-default. Tool capability or environment visibility is not PROD authorization.
- Worktrees isolate code, not shared databases. Do not run uncoordinated mutations.
- Never expose `.env`, credentials, signed URLs, service-role keys, customer data or private refs.

## Git and promotion

- Read-only agents do not change Git state.
- Do not pull, merge, rebase, reset, stash, force-push or rewrite published/Lovable-connected
  history automatically.
- Do not push, merge, deploy or promote without explicit round-specific authorization.
- A handoff or this mirror cannot grant those permissions.
- Preserve unrelated work and stop on semantic conflicts.

## Product architecture

- Keep the existing data seam: UI uses product ports/adapters; it does not call Supabase directly.
- Domain/state-machine behavior stays in the product domain layer, not presentation components.
- Tenant-specific Scooby Dog identity stays in configuration/presentation and never contaminates
  reusable Commerce components or shared platform code.
- Use existing primitives, tokens and gates. Do not invent a parallel architecture.

## Frontend visual process

- Existing product first: inspect the current surface, reusable components, tokens, `BRAND.md`,
  `REUSE.md` and approved patterns before proposing UI.
- shadcn/ui over Radix is the foundation when already adopted and compatible. Preserve the existing
  design system. Lucide (`lucide-react`) is the current icon set; preserve it rather than mixing
  libraries casually.
- 21st.dev is the priority discovery/reference surface; Animista may support selective
  microanimations with `prefers-reduced-motion`.
- External research is not adoption and does not authorize dependency changes. Evaluate technical
  compatibility, accessibility, weight, maintenance, tokens and brand fit.
- Classify visual work as Repair, Refinement or Modeling. Modeling follows
  `discover → evaluate → candidates → human selection when material → prototype/isolate → adapt → integrate → verify`.
- A visual task never authorizes reinterpretation of backend, Supabase, tenancy, auth, RLS,
  migrations or data contracts.

**Agents execute Framixor governance; they do not redefine it.**
