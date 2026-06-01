# Wizard — Overview

Wizard is the skill-authoring skill. It guides an editor through designing, modifying, and auditing Claude Code skills via a structured, phase-driven conversation. Its output is always a skill file on disk — not advice about skills.

- [File layout](#file-layout)
- [Supported flows](#supported-flows)

---

## File layout

```
plugin/skills/wizard/
├── SKILL.md                          # Always loaded: dispatcher, persona, rules, key concepts
├── references/
│   ├── CREATE.md                     # Full phase-by-phase creation flow
│   ├── EDIT.md                       # Scoping + change proposal + file update flow
│   ├── REVIEW.md                     # Review checks + report generation flow
│   └── tooling-catalog.md            # Reference: tools and integration patterns
└── examples/
    ├── token-efficiency-patterns.md  # Concrete examples of execution efficiency patterns
    └── tooling-catalog-examples.md   # Worked examples for tooling-catalog.md
```

SKILL.md is the only always-loaded file. Everything else is read on demand — zero context cost until needed.

--- 

## Supported flows

Wizard is a multi-flow architecture. Each flow has its own reference file:

| Flow | Invocation | Reference file | What it does |
|---|---|---|---|
| `create` | `/skillmancy:wizard create <name>` | `references/CREATE.md` | Designs and writes a new skill from scratch through six ordered phases |
| `edit` | `/skillmancy:wizard edit <name>` | `references/EDIT.md` | Scopes and applies targeted changes to an existing skill |
| `review` | `/skillmancy:wizard review <name>` | `references/REVIEW.md` | Audits a skill against its own design criteria and produces a findings report |

If a bare `<name>` is given with no flow prefix, the skill auto-detects based on whether the directory exists and confirms with the user before proceeding. See [skill-flows.md](./skill-flows.md) for a detailed breakdown of each flow.
