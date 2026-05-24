---
tags:
  - context
  - venture
  - meta
---
# {Company} — Venture Context

This folder is the **source of truth** for everything about {Company}: identity, positioning, products, personas, pricing, market, GTM, brand, voice, culture, and technical primitives.

> When mounted into an operator's vault via `/aios:company --mount`, this folder lands at `vault/00 - notes/context/ventures/{company}/`. The `onboarding-{company}` agent reads these files to walk operators through {Company} in compelling voice on Day 1.

---

## What lives here (13 canonical files + 3 optional addons)

**Layer 1 — Identity:**

| File | Purpose |
|---|---|
| [[about_venture]] | What {Company} IS in one paragraph — mission, history, what you do |
| [[origin-story]] | Why {Company} exists — founding insight, why now, what was learned the hard way |
| [[positioning]] | Category definition, narrative, worthy rivals — what {Company} explicitly is NOT |
| [[personas]] | Who {Company} serves — buyer ICPs, audience archetypes |
| [[primitives]] | Core technical or conceptual IP — the load-bearing primitives that make {Company} possible |

**Layer 2 — Operations:**

| File | Purpose |
|---|---|
| [[gtm]] | Go-to-market motion — channels, sequencing, sales process |
| [[offerings]] | Products and services catalog — SKUs in plain language |
| [[pricing]] | Pricing model, tiers, packaging |
| [[culture]] | Operating principles, decision frameworks, rituals — the lived rules |
| [[market]] | Competitive landscape, macro forces, where the puck is going |

**Layer 3 — Brand + Voice:**

| File | Purpose |
|---|---|
| [[voice]] | **Required, load-bearing.** Voice and tone — how {Company} speaks. Used by `onboarding-{company}` for register calibration + every Claude session writing in {Company}'s name. |
| [[brand]] | URL pointers to logos, fonts, palette, asset library (this folder stores context, not binaries) |
| [[design]] | Visual design system per Google's `design.md` spec — tokens, components, render targets |

**Optional addons** (commented out by default; uncomment + populate to activate):

| File | When to activate |
|---|---|
| [[coding-practices]] | Engineering standards, code review philosophy, commit conventions — populate if {Company} ships code |
| [[tools-we-use]] | Internal stack reference — what tools the team uses day-to-day |
| [[repos]] | Pointer list of company repos with 1-line descriptions — populate if you have multiple repos |

---

## How this context flows

```
Operator's USER.md ## Companies (mounted)
  → registers {Company} with substrate + source-url + venture folder
       ↓
/aios:company --sync {company}
  → reads .{company}-sync tracker (hash + date)
  → diffs against remote HEAD
  → cascades context/ → vault/00 - notes/context/ventures/{company}/
  → cascades agents/, plugins/, templates/, etc. → {layer}/{company}/
       ↓
onboarding-{company} agent (auto-fires after --mount, offers after --sync)
  → reads voice.md for register calibration
  → reads about_venture + origin-story + positioning + culture in compelling voice
  → role-calibrates rest of the walk based on operator's declared role
       ↓
/today (next morning)
  → scans .{company}-sync tracker for freshness
  → surfaces venture-context updates in operator's daily plan
```

The relationship is read-only: `/aios:company --sync` pulls from this canonical into operator vaults. Operators never write back to this folder from their vault — they PR to this repo directly when they want to contribute.

---

## How to populate this folder

The cleanest path is `/aios:company --create` from an AIOS-enabled vault — that flow runs an interview, drafts each file, and pushes to a new venture-context repo. See [The-AIOS/company-template](https://github.com/The-AIOS/company-template) (this repo's source) for the canonical scaffold.

For existing companies migrating onto AIOS: clone the template, fill in each file at your own pace, push to your venture-context repo, then teammates `--mount` it.

---

**See also:**

- `README.md` (repo root) — entry point for humans browsing this repo
- `CLAUDE.md` (repo root) — {Company}'s operating manual that composes at runtime with each operator's personal `INTENT.md`
- `agents/onboarding-{company}.md` — the HR-Day-1 companion that reads these context files
- [The-AIOS/aios](https://github.com/The-AIOS/aios) — the framework canonical (the `/aios:company` command lives there)
