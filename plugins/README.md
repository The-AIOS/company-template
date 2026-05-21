# PLUGINS — {Company}-distributed Claude Code plugins

> Optional company-distributed plugins. When an operator runs `/aios:company --sync {your-company}`, the contents of this folder land at `plugins/{your-company}/` in their AIOS vault.

## Why distribute plugins at the company level?

Companies have shared operational patterns that aren't general enough for the bundled `aios` plugin. Examples:

- `/acme-pipeline:sync` — refresh Acme's CRM pipeline view
- `/acme-pipeline:month-end` — Acme's month-end closing routine
- `/acme-board:prep-deck` — generate a board prep deck from internal sources
- Plugin-scoped agents (`acme-customer-rescue`, `acme-board-prep`)
- Plugin-scoped skills (Acme's voice, Acme's review-cycle rituals)
- Plugin-scoped MCP servers (internal CRM, billing, etc.) declared via `.mcp.json`

## Structure

Each company-distributed plugin follows the canonical Claude Code plugin layout:

```
plugins/<plugin-name>/
├── .claude-plugin/
│   └── plugin.json          ← REQUIRED: name, version, description, author
├── commands/                ← slash command .md files (becomes /<plugin>:<cmd>)
│   └── <cmd>.md
├── agents/                  ← plugin-scoped task agents (optional)
├── skills/                  ← plugin-scoped skills (optional)
├── hooks/                   ← plugin-scoped hooks (optional)
├── .mcp.json                ← plugin-scoped MCP servers (optional)
├── CLAUDE.md                ← plugin-specific instructions (optional)
└── README.md                ← human-readable docs (optional)
```

On the operator side, it lands at `plugins/{your-company}/<plugin-name>/` — namespaced by company so multiple companies' plugins never collide.

## Naming convention

- **Plugin folder name:** use a hyphenated descriptive name like `acme-pipeline`, `acme-board`, or `acme-ops`. Don't prefix with `aios-` (that's reserved for framework bundles).
- **Slash command invocation:** if your plugin is named `acme-pipeline` with a `sync.md` command, operators invoke it as `/acme-pipeline:sync` — NOT `/aios:sync` (that'd collide with the bundled `aios` plugin).
- **Plugin manifest:** declare `"name"` in `.claude-plugin/plugin.json` matching the folder name. Set `"version"` (semver) so `/aios:update` can track changes.

## Empty folder = no plugin shipment

If this folder contains only this README (no `<plugin-name>/` subfolders), operators who mount {your-company} won't get any plugins. That's fine — most companies don't ship custom plugins; agents/skills/templates alone are often enough.

## See also

- AIOS `/aios:company` command reference at [The-AIOS/aios](https://github.com/The-AIOS/aios)
- Bundled `aios` plugin at [The-AIOS/aios → plugins/aios/](https://github.com/The-AIOS/aios/tree/main/plugins/aios) — canonical example of the plugin structure
- Anthropic's `claude-for-legal` at [github.com/anthropics/claude-for-legal](https://github.com/anthropics/claude-for-legal) — reference for multi-plugin marketplaces
