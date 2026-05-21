# Company Template (AIOS)

A scaffold for mounting a company's venture context — and optional company-specific infrastructure — into an [AIOS](https://github.com/The-AIOS/aios) vault.

## Use

This repo is **a template, not a runtime**. To use it:

1. **From an AIOS operator's perspective:** in your `~/aios` Claude session, run:

   ```
   /aios:company --create
   ```

   The `/aios:company` command clones this template, walks you through filling in the 10 context files (interview-driven), pushes to your new venture-context repo (typically `{your-org}/venture-context`), and registers it in your `USER.md`.

2. **Mounting an existing company's venture-context** (you got an invite from a teammate):

   ```
   /aios:company --mount {url}
   ```

## What's inside

### `context/` — the canonical 10 context files

The structure a company's knowledge ships in. Layered by purpose:

**Layer 1 — Identity:**
- `about_venture.md` — mission, history, what the company does
- `positioning.md` — category, narrative, worthy rivals
- `personas.md` — who it serves
- `primitives.md` — core technical/conceptual IP

**Layer 2 — Operations:**
- `gtm.md` — go-to-market motion
- `offerings.md` — products / services catalog
- `pricing.md` — pricing model + tiers
- `culture.md` — values, decision frameworks, rituals

**Layer 3 — Brand:**
- `design.md` — visual + voice design system (per Google's design.md spec)
- `brand.md` — URL pointers to logos / fonts / palette / asset library

When an operator runs `/aios:company --sync {your-company}`, these files land at `vault/00 - notes/context/ventures/{your-company}/` in their vault.

### `CLAUDE.md` — Claude operating manual (root-level)

How Claude should act when working in this company's context: voice, tradeoff rules, escalation triggers, communication boundaries. Composes with each operator's personal `INTENT.md` (operator-side autonomy levels + company-side operating principles).

### Optional infra folders (top-level)

Beyond context, a company can distribute **its own infra** to operators who mount it. When `/aios:company --sync` runs, these land at namespaced paths in the operator's vault:

| Folder | Lands at (operator's vault) | Use case |
|---|---|---|
| `agents/` | `agents/{your-company}/` | Company-specific agents (e.g. `acme-board-prep`, `acme-onboarding`) |
| `plugins/<plugin>/` | `plugins/{your-company}/<plugin>/` | Company-distributed Claude Code plugins — self-contained bundles of slash commands + plugin-scoped agents/skills/hooks/MCPs |
| `hooks/` | `hooks/{your-company}/` | Company-specific event hooks |
| `mcps/` | `mcps/{your-company}/` | Company-specific MCP servers (e.g. integration with your CRM / billing) |
| `skills/` | `skills/{your-company}/` | Company-specific Agent Skills |
| `templates/` | `templates/{your-company}/` | Company-specific templates (proposal, contract, deck shapes) |

Each folder starts as a scaffold with a placeholder README. Add company-specific content when you have it; leave empty if you don't (operators just won't get anything in those namespaces).

### Optional addons in `context/`

Scaffolded as commented-out, uncomment to activate:

- `coding-practices.md` — engineering standards, code review philosophy, commit conventions
- `tools-we-use.md` — internal stack reference
- `repos.md` — pointer list of company repos with 1-line descriptions

## Naming convention

Recommended repo name when you fork: `{your-org}/venture-context` (e.g. `acme/venture-context`, `sovrahq/venture-context`). The `/aios:company --create` flow uses this default.

## License

GPL v2+ (template structure). Your company-specific content inside the forked repo is whatever you license it as.

## See also

- [The-AIOS/aios](https://github.com/The-AIOS/aios) — the AIOS framework this template plugs into
- `plugins/aios/commands/company.md` (in The-AIOS/aios) — the canonical `/aios:company` command reference
