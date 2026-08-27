# Scooby Dog Orders — Engineering Handoff

> **Generated / derived / public-safe. Do not edit manually.** This file is rendered from
> `HANDOFF_ENGINEERING.json`. It is not canonical governance and grants no execution authority.

## Identity and authority

| Field | Value |
| --- | --- |
| Operating model | `1` |
| Product | `scooby-dog-orders` |
| Repository | [https://github.com/framixor/scooby-dog-orders](https://github.com/framixor/scooby-dog-orders) |
| Canonical ref | `refs/heads/main` |
| Product commit | `d29cc1a758e08ab1e1ffb8e41a65c11d7cb9b74f` |
| Classification | `DERIVED_PUBLIC_SAFE` |

This handoff is a derived public-safe execution aid, not canonical governance or product source.

- **Conflict rule:** Canonical Framixor governance, official product Git state and explicit current-run authorization prevail; stop on conflict.
- **Authorization rule:** This handoff grants no permission to write, push, merge, deploy or mutate an environment.

## Task-class routing

| Task class | Guidance | Required capabilities | Minimum gates | Write budget |
| --- | --- | --- | --- | --- |
| `general_implementation` | Use for bounded non-visual product changes. The task/run must still declare exact paths, effects and verification. | `framixor-task-preflight`, `framixor-verification` | `task-envelope`, `repository-identity`, `scope`, `evidence-bundle` | `bounded` |
| `visual_exploration` | Explore visual candidates only inside an explicitly isolated scope; exploration is not promotion or permission to rewrite the product. | `framixor-task-preflight`, `framixor-frontend`, `framixor-verification` | `task-envelope`, `repository-identity`, `scope`, `frontend-domain-evidence`, `evidence-bundle` | `bounded` |
| `faithful_visual_refactor` | Implement an approved visual direction faithfully. Preserve behavior and identity; do not invent a replacement direction. | `framixor-task-preflight`, `framixor-frontend`, `framixor-verification` | `task-envelope`, `repository-identity`, `scope`, `frontend-domain-evidence`, `evidence-bundle` | `bounded` |
| `new_ui_feature` | Add a bounded UI capability using the existing design system, data seams and product contracts. | `framixor-task-preflight`, `framixor-frontend`, `framixor-verification` | `task-envelope`, `repository-identity`, `scope`, `frontend-domain-evidence`, `evidence-bundle` | `bounded` |
| `component_implementation` | Implement or refine a component within existing tokens, primitives and accessibility expectations. | `framixor-task-preflight`, `framixor-frontend`, `framixor-verification` | `task-envelope`, `repository-identity`, `scope`, `frontend-domain-evidence`, `evidence-bundle` | `bounded` |
| `product_redesign` | Requires explicit redesign authority and human approval of material visual direction; it is never inferred from a normal frontend request. | `framixor-task-preflight`, `framixor-frontend`, `framixor-verification` | `task-envelope`, `repository-identity`, `scope`, `frontend-domain-evidence`, `evidence-bundle` | `bounded` |
| `visual_bugfix` | Repair a specific visual defect while minimizing change and preserving surrounding behavior and styling. | `framixor-task-preflight`, `framixor-frontend`, `framixor-verification` | `task-envelope`, `repository-identity`, `scope`, `frontend-domain-evidence`, `evidence-bundle` | `bounded` |

## Applicable capabilities

- `framixor-frontend` — Load Scooby identity and existing UI foundations, define the allowed-change envelope, then require rendered evidence for material visual work.
- `framixor-task-preflight` — Prove repository/ref, classify the task, declare environment and effects, and establish bounded scope before writing.
- `framixor-verification` — Recheck identity and scope, run repository and domain gates, and report PASS, FAIL or INCONCLUSIVE with evidence.

## Product governance references

- [Scooby repository rules](https://github.com/framixor/scooby-dog-orders/blob/d29cc1a758e08ab1e1ffb8e41a65c11d7cb9b74f/AGENTS.md)
- [Scooby repo-scoped bootstrap](https://github.com/framixor/scooby-dog-orders/blob/d29cc1a758e08ab1e1ffb8e41a65c11d7cb9b74f/docs/AGENT_BOOTSTRAP.md)
- [Scooby brand contract](https://github.com/framixor/scooby-dog-orders/blob/d29cc1a758e08ab1e1ffb8e41a65c11d7cb9b74f/BRAND.md)
- [Scooby reuse boundaries](https://github.com/framixor/scooby-dog-orders/blob/d29cc1a758e08ab1e1ffb8e41a65c11d7cb9b74f/REUSE.md)
- [Scooby dated engineering state](https://github.com/framixor/scooby-dog-orders/blob/d29cc1a758e08ab1e1ffb8e41a65c11d7cb9b74f/STATE.md)

## Frontend authority boundary

- Frontend work may change only the authorized product paths and behavior described by the current task/run.
- Use existing ports/adapters, configuration, tokens, shadcn/Radix foundations and Lucide icons where applicable.
- Material visual work is incomplete without running the application and inspecting rendered results.

## Backend and database boundary

- A frontend task does not authorize schema, migration, RLS, grants, RPC, auth, tenant, service-role or shared-platform changes.
- If a frontend task discovers a backend or database gap, implement only independent frontend-safe work, report the gap and stop that portion.
- No database mode, environment mutation or PROD operation is authorized by this handoff.

## Must preserve

- Official Git history and Lovable-connected published history; never rewrite it.
- The config-driven restaurant boundary and the existing UI-to-ports/adapters data seam.
- Scooby's mobile-first identity: saturated yellow, teal accents, light surfaces, Poppins and direct non-SaaS voice.
- Tenant-specific brand assets must not leak into reusable Commerce domain or shared components.
- Existing order, pricing, tracking, authentication and tenant behavior unless the task explicitly authorizes a compatible change.

## Forbidden actions

- Do not expose credentials, environment values, customer data, signed URLs or private infrastructure identifiers.
- Do not change backend/database contracts, migrations, RLS, auth, tenant boundaries or shared platform from a frontend task.
- Do not push, merge, deploy, promote or mutate TEST, STAGING or PROD without explicit run-specific authorization.
- Do not replay closed historical slices or treat this derived handoff as product authority.
- Do not load or infer unrelated product or platform context without a dependency established by the current task.

## Allowed external scope

- Read this handoff and the referenced Scooby files available to the executor.
- Inspect the current official Scooby repository/ref and targeted implementation before proposing changes.
- Perform only the task/run's explicit allowed paths and external effects; this handoff grants none by itself.
- Return candidate changes and evidence for Framixor review and promotion.

## Verification expectations

- Revalidate official repository, canonical ref/base, worktree, environment, changed files and authorized scope.
- Run format:check, lint, typecheck, test and build in that order for code changes.
- For material frontend work, run the application, inspect the rendered result and provide viewport/state evidence.
- Report every required gate as PASS, FAIL or INCONCLUSIVE; missing evidence never becomes PASS.

## Current product-level status

- The generated baseline is the exact official Scooby ref and commit recorded in Identity and Provenance.
- No implementation task is activated by this handoff; a separate task/run must provide scope and authorization.
- The official product repository remains authoritative for code and behavior; this artifact is a compact derived engineering contract.

## Provenance

| Source | Repository | Ref | Commit |
| --- | --- | --- | --- |
| Operating model | https://github.com/framixor/framixor-agent-operating-model | `refs/heads/main` | `7ee79286626360800abfbd96daddf38f0dcbc7c3` |
| Product | https://github.com/framixor/scooby-dog-orders | `refs/heads/main` | `d29cc1a758e08ab1e1ffb8e41a65c11d7cb9b74f` |

- Publication profile: `agent/handoffs/products/scooby-dog-orders.public-input.v1.json` — `b861daca652a18eadbdabb14553c58ad7506bdd39a6d3833cc75c393cdb41cc9`
- Source allowlist: `agent/handoffs/source-allowlist.v1.json` — `9cab45c80b27c745580e81dd33405d47fefeaafd5b5a08bf1cd68defe4b55426`

| Source class | Artifact | SHA-256 |
| --- | --- | --- |
| `operating_model` | `AGENTS.md` | `5babc1753f3361e135a5b9ccca100a6138da5309d9359b088b45c0c324ce6248` |
| `operating_model` | `MODEL_VERSION` | `4355a46b19d348dc2f57c046f8ef63d4538ebb936000f3c9ee954a27460dd865` |
| `operating_model` | `agent/capabilities/framixor-frontend/PROCEDURE.md` | `079a7e1243db360b366bb4901484f356826ff85f6f239d3c7f8d3d6c63a86f0d` |
| `operating_model` | `agent/capabilities/framixor-task-preflight/PROCEDURE.md` | `be4e8a70e402e92f65a6118e0f2c0a78003ac9b68249293d376714386cd2efdd` |
| `operating_model` | `agent/capabilities/framixor-verification/PROCEDURE.md` | `dc627753a32d2ad1e4dd2e1dec3df829edf1f89eed9df3f8d4dbbe824da5a923` |
| `operating_model` | `agent/manifest.json` | `9a24d4633afe3867026de71063a24688b30f6a4ddfdf30b68ddcd5616c83a296` |
| `operating_model` | `governance/AGENT_EXECUTION_CONTRACT.md` | `f28dae5cfca8029447a234c89f27a1a647552469d1bfd3a2d8cba7d86a9fe7f2` |
| `operating_model` | `governance/FRONTEND_VISUAL_CONTRACT.md` | `71bb965d0b492ee082487695158425e23d7aa9f05f1e6af59dabf3dcf5d909eb` |
| `product` | `AGENTS.md` | `c499f2be4e4cd1b60aeba49ceac29eb58da37408268f228e55f2df951007c17a` |
| `product` | `BRAND.md` | `ce9cbc777034b93be010fd71346ac291fc826f587c7f1612dfd45180eb0d54e0` |
| `product` | `REUSE.md` | `484e13758ad9a975b37f74b11c547caf614947fd22289d5a9da1e3a2a6c91ea8` |
| `product` | `STATE.md` | `38db1327e96946afffc68e042c871a6f4c5280b3e5fec3b9ecac9b6ea0972dc5` |
| `product` | `docs/AGENT_BOOTSTRAP.md` | `38e15e0a744b842277f03ac7179186557ae22a91e30214a292e700d86b7c6874` |
| `product` | `package.json` | `e0c2700a810f1f44748e87d1667a21fc09241773c50eab802c9d0a892d0d718c` |
