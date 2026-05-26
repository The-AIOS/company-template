# AGENTS — {Company}-specific agents

> Optional company-distributed agents. When an operator runs `/aios:company --sync {your-company}`, the contents of this folder land at `agents/{your-company}/` in their AIOS vault.

## Why distribute agents at the company level?

Companies have shared operational patterns that aren't general enough to live in canonical AIOS bundles. Examples:

- **agents:** `acme-board-prep` (knows how Acme runs board meetings), `acme-customer-rescue` (knows the Acme escalation playbook)
- **commands:** `/aios:acme-sync-pipeline` (refreshes Acme's CRM pipeline view), `/aios:acme-month-end` (Acme's month-end closing routine)
- **hooks:** UserPromptSubmit hooks that inject Acme-specific context
- **mcps:** Company-internal MCP servers (CRM, billing system, internal-tool wrappers)
- **skills:** SKILL.md folders for company-specific patterns
- **templates:** Proposal / contract / deck shapes specific to the company

## Naming convention (load-bearing, CI-enforced)

The AIOS naming convention for venture-namespaced agents:

- **General agents:** `{your-company}-{noun}.md` — e.g. `acme-decks.md`, `acme-brochures.md`, `acme-board-prep.md`, `acme-lawyer-uk.md`. The venture prefix disambiguates when an operator mounts multiple ventures (e.g. an operator with both `sovra` + `chuycepeda` mounted can spawn `sovra-decks` vs `chuycepeda-decks` unambiguously). When mounted, the agent is addressable as `{your-company}-{noun}` at the namespaced path `agents/{your-company}/.../{your-company}-{noun}.md`.
- **Onboarding companion** is the one exception — use the `onboarding-{your-company}.md` pattern (verb-target, not venture-prefix). The bundle's HR-Day-1 agent goes at `agents/onboarding-{your-company}.md`.
- **Skill folders / hook scripts / templates:** use whatever name makes sense — they live in `{layer}/{your-company}/` regardless (no naming constraint beyond folder placement).

**Why the convention matters:**
1. **Disambiguation** — operators with multiple ventures mounted (rare but real) get unambiguous agent names from `spawn` and `/agent` commands.
2. **Discoverability** — `ls agents/{your-company}/` shows files visibly venture-tagged, easy to scan.
3. **Anti-collision** — venture agents never accidentally shadow framework-default agents. Framework-bundled agents under `agents/aios/{bundle}/` stay function-named (`deck-builder`, `lawyer`, `accountant`); venture-namespaced agents always carry the prefix. No collision possible.

**Where AIOS canonical agents live** (NOT in this folder — for reference): `agents/aios/{sales,strategy,finance-legal,engineering,communication,personal}/` in the framework repo. Their names stay function-only (no `aios-` prefix) — they're the defaults, not a namespace.

**CI enforces this.** The `.github/workflows/validate-agent-names.yml` workflow checks every commit: every agent file in `agents/` must either (a) have `name: {venture}-{noun}` matching its filename basename, or (b) be `onboarding-{venture}.md`. Files with `{{placeholder}}` syntax (template scaffolds) are exempt. Violations fail CI, blocking merge.

## Empty folder = no shipment

If this folder is empty (just this README), operators who mount {your-company} won't get any agents in their vault. That's fine — most companies don't ship custom agents; context alone is enough.

## See also

- The AIOS `/aios:company` command reference (in [The-AIOS/aios](https://github.com/The-AIOS/aios))
- AIOS canonical agents at the framework level: `agents/aios/{bundle}/` (6 bundles: sales, strategy, finance-legal, engineering, communication, personal)
