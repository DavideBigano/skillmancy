# Wizard — Migration helper

A skill to migrate existing skills from an older plugin version to the current one. Implemented as `/skillmancy:migrate`.

---

## Problem

The skill structure evolves — section names change, new conventions are introduced. When this happens, existing skills silently fall out of spec with no mechanism to detect or remediate the drift.

---

## Solution

### skillmancy-version field

Each skill's `SKILL.md` frontmatter carries a `skillmancy-version` field recording which version of the canonical structure it was authored against:

```yaml
---
name: skill-name
skillmancy-version: "0.2.0"
---
```

Skills authored before versioning was introduced have no field — treated as `0.1.0` (pre-versioning baseline).

### Migration skill

`/skillmancy:migrate <skill-name>` reads the skill's current `skillmancy-version`, applies the relevant structural transforms up to the current version, and writes the updated skill back to disk. Each breaking change maps to a discrete, versioned migration defined inline in the skill.

---

## Supported migrations

| From | To | Key changes |
|---|---|---|
| 0.1.0 (or missing) | 0.2.0 | `## Persona` → `## Authorities`; `## Rules` → `## Guidelines` + Task checks |
