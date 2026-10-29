# Repository guidelines

REA provides local reverse-engineering workflows through shared CLI/MCP semantics. Preserve observations, derivations, inferences, unknowns, Evidence provenance and session semantics across both adapters. Provider setup lives in [README.md](README.md#choosing-a-deep-analysis-provider).

## Product and authority

Follow [CONTRIBUTING.md](CONTRIBUTING.md#contribution-scope). Unresolved scope, authority, side effects or required proof block integration. New capabilities involving target execution, injection, mutation or protection recovery need the maintainer's scope decision before substantial integration work. Proposals and small exploratory drafts may resolve questions; they do not authorise integration.

Ghidra uses ephemeral databases without modifying executable bytes or controlling a GUI. Windows Ghidra P0 has no mutation authority. IDA analysis is read-only; never save or close an attached GUI database.

Configuration changes must be additive, idempotent and backed up. Installers must not install/upgrade unrelated software (Homebrew, Node, npm, Java or Ghidra); Ghidra/IDA are bring-your-own. `rea setup` must show planned changes and require approval before writes or Hopper installation.

Preserve caller-selected local evidence, paths, URLs, digests and metadata. Redact transport credentials and explicitly sensitive values; names/patterns alone do not establish secrecy. Do not persist the ambient environment merely because a child inherits it.

## Architecture and cleanup

Dependencies flow inward through domain contracts, provider adapters, shared application workflows, then CLI/MCP adapters. Keep provider protocols out of domain/application layers. Read [docs/architecture.mermaid](docs/architecture.mermaid) for composition work and [docs/tool-design.md](docs/tool-design.md) for tool design.

Give parsed facts and resources one owner. Consumers use that owner's interpretation, preserving identity, omission, uncertainty and source evidence. Normalise once with format-aware parsers. Keep proof of ownership distinct from validity/editability/readiness; malformed owned data may still be removable. Unknown identity/applicability must remain unknown.

For bugs or review fixes, inspect the producing boundary and affected consumers; fix the ownership/representation rather than layering downstream repairs. Complete directly related refactoring and remove superseded representations only after consumer verification. Explain any remaining cleanup. Avoid abstractions for imagined complexity.

Retain ownership of resources whose cleanup failed. Reuse `src/process/` supervision and identity primitives; PID/executable path alone do not prove ownership after exit/reuse. Parse unknown inputs; model expected errors using the tagged algebra and `Result`. Preserve original values and explicit unknowns when normalisation loses information. File paths, file URLs and HTTP paths differ.

Validate advertised JSON Schemas against their declared dialect and actual clients after SDK conversion. Bind handlers to named exact contracts; catalog ordering cannot select operations/schemas. Tool limits must follow real format/protocol/authority/resource constraints, account for expansion before allocation and derive completeness from examined coverage.

## Performance

Optimise agent context first, analysis time second, CPU/memory third while preserving correctness, provenance, caller choices, compatibility and safe resource bounds. Return sufficient evidence/limitations, offer retained complete Evidence, and honour requested detail. Count whole-task schemas, calls and retries. Reuse validated work with correct cache keys, invalidation/lifetime and live-state freshness. Bound concurrency and retained state.

For cost-affecting changes compare equivalent representative completed workflows where available: tokens, elapsed/CPU time and peak process-family memory. Separate cold/warm results, estimates and unmeasured costs; fewer bytes alone do not prove faster analysis.

## Development

Use `.nvmrc` and `package.json#packageManager`. If the environment selects an older Node, fix PATH to the already-installed pinned toolchain.

- `npm ci`: locked dependencies.
- `npm run build:cached`: runtime and packaged skill.
- `npm run test:local -- PATH...`: source tests without building.
- `npm run test:focused -- PATH...`: exact tests and required artefacts.
- `npm run check:fast`: cached typecheck/lint and pre-push check.
- `npm run docs:check`: generated documentation validation.

Use focused checks during implementation; `npm run check:pr` is the optional complete local gate for broad changes/CI diagnosis. Follow [CONTRIBUTING.md](CONTRIBUTING.md) for generated ownership and releases. Preserve the managed Turborepo block below: turbo can re-add it; this change does not opt out or change runtime configuration.

Edit source contracts and `.agents/skills/reverse-engineer-anything/`; generated `docs/public/product-catalog.json`, `docs/verification/managed-conformance-*.json` and `skills/` are ignored. `.cache/mcp-tool-catalog.json` is test metadata. Never commit binaries, provider documents, credentials, build/dependency outputs or local plans.

## Tests and delivery

For tests/provider claims read [docs/testing.md](docs/testing.md). Prefer real public CLI/MCP workflows, then production-boundary integration, then producer goldens; module tests cover distinct semantics. Preserve malformed-input, cancellation, cleanup, permission, capacity and target-identity coverage. Simulated providers do not establish live behaviour.

Finish the requested scope with relevant checks, repair routine failures and stop without idle/backlog work. Delegate bounded work only when useful and preserve existing authority. Avoid repeated review of unchanged work. Use Conventional Commit/PR subjects and breaking-change markers. State changed files, checks/omissions, provider scope and residual risk; distinguish implementation, release readiness and release. Publishing/integration requires the applicable maintainer authority.

<!-- BEGIN:turborepo-agent-rules -->

# This is NOT the Turborepo you know

Turborepo configuration, task behavior, and CLI commands can vary between installed versions and may differ from your training data. Resolve the `turbo` package from this file's directory or relevant workspace; in monorepos, it may not be visible from the repository root. For example, run `node -p "require.resolve('turbo/package.json')"` from a workspace that depends on `turbo`.

Read `docs/README.md` inside that installed package first, then read the relevant pages from its `docs/` directory before changing Turborepo configuration or commands. Heed deprecation notices. These bundled docs match the installed package version and are available without network access.

This block is written and re-added by `turbo` before repository-scoped commands when an AI agent is detected. In the Turborepo source repository, its template is defined in `crates/turborepo-cli/src/cli/agent_guidance.rs`. Removing the managed block while updates are enabled means a later qualifying invocation will add it again. Set `"agentGuidance": false` in the root `turbo.json` or `turbo.jsonc` to opt out; this does not remove an existing block. Keep the block committed with your work to avoid an uncommitted change on the next agent invocation.
<!-- END:turborepo-agent-rules -->
