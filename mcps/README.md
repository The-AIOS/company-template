# MCPS — {Company}-specific mcps

> Optional company-distributed mcps. When an operator runs `/aios:company --sync {your-company}`, the contents of this folder land at `mcps/{your-company}/` in their AIOS vault.

## Why distribute mcps at the company level?

Companies have shared operational patterns that aren't general enough to live in canonical AIOS bundles. Examples:

- **agents:** `acme-board-prep` (knows how Acme runs board meetings), `acme-customer-rescue` (knows the Acme escalation playbook)
- **commands:** `/aios:acme-sync-pipeline` (refreshes Acme's CRM pipeline view), `/aios:acme-month-end` (Acme's month-end closing routine)
- **hooks:** UserPromptSubmit hooks that inject Acme-specific context
- **mcps:** Company-internal MCP servers (CRM, billing system, internal-tool wrappers)
- **skills:** SKILL.md folders for company-specific patterns
- **templates:** Proposal / contract / deck shapes specific to the company

## Naming convention

When you add content to this folder, the AIOS naming convention for company-distributed infra is:

- For single files (e.g. agents, commands): use `{your-company}-{name}.md` — e.g. `acme-board-prep.md`. When mounted, it becomes addressable as `{name}` at the namespaced path.
- For skill folders / hook scripts: use whatever name makes sense — they live in `mcps/{your-company}/` regardless.

## Empty folder = no shipment

If this folder is empty (just this README), operators who mount {your-company} won't get any mcps in their vault. That's fine — most companies don't ship custom mcps; context alone is enough.

## See also

- The AIOS `/aios:company` command reference (in [The-AIOS/aios](https://github.com/The-AIOS/aios))
- AIOS canonical mcps at the framework level: `mcps/aios-*/` (or relevant location)
