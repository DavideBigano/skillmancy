# Wizard — Migration helper

A planned feature to handle breaking changes to the canonical skill structure over time. Tracked in [#9](https://github.com/DavideBigano/skillmancy/issues/9).

---

## Problem

The skill structure evolves — section names change (e.g. "Key concepts" → "Resources", engagement rules → "Rules"), new conventions are introduced. When this happens, existing skills silently fall out of spec with no mechanism to detect or remediate the drift.

---

## Proposed feature

### Version field in frontmatter

Add a `skill-version` field to the skill frontmatter to record which version of the canonical structure the skill was authored against:

```yaml
---
name: skill-name
skill-version: 1
description: ...
---
```

This makes structural drift detectable at a glance and gives a migration helper a reliable starting point. Skills authored before versioning was introduced would be treated as an implicit baseline version.

### Migration helper skill

A dedicated skill (e.g. `/skillmancy:migrate`) that accepts a skill name and:

1. Reads the skill's current `skill-version`
2. Applies the relevant structural transforms in sequence up to the current version
3. Writes the updated skill back to disk

Each breaking change maps to a discrete, versioned migration step — renaming a section heading, updating cross-references, adjusting template language.

---

## Open questions

- Where migration logic lives — inline in the skill vs. versioned migration files loaded on demand
- Whether the wizard review flow should flag version mismatches as findings
- How to handle skills authored before versioning was introduced (implicit v0?)
- Granularity of version increments — one version bump per breaking change vs. batched releases
