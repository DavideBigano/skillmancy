# Skill design — Resources

The optional canonical reference layer: shared vocabulary, frameworks, and assumptions that need consistent treatment across multiple skill sections.

- [What resources are](#what-resources-are)
- [The four types of entry](#the-four-types-of-entry)
- [When to add an entry](#when-to-add-an-entry)
- [Format](#format)
- [Common mistakes](#common-mistakes)

## What resources are

Resources is the canonical reference layer for a skill: vocabulary, frameworks, assumptions, and construction guidance applied consistently across more than one section. Optional — if nothing needs a shared definition, skip it.

---

## The four types of entry

**Shared vocabulary** — terms the skill uses in a specific, non-obvious way. Define once; reference from wherever needed. If only one section uses it, define it inline.

**Conceptual frameworks** — models the skill reasons from without re-explaining. Earns its place when multiple sections would otherwise have to reconstruct it independently.

**Operating assumptions** — things the skill takes as given about the context, user, or domain. Not rules (which are conditions to satisfy) but starting conditions.

**Shared construction guidance** — instructions for building or evaluating a skill section that multiple flows apply consistently. In Wizard, the Persona design and Resources design entries are this type.

---

## When to add an entry

Add when a concept needs consistent treatment across more than one section. Test: would sections using this concept drift apart without a shared definition? If yes, add it; if each uses it in a section-specific way, leave it inline.

**Reinforcement vs. duplication** — Persona, rules, and resources can address the same concept at different abstraction levels — that's intentional. Test for genuine duplication: does each representation do something the others don't? If no, cut the weaker one.

---

## Format

Each entry follows this format:

```
**[Label]** — [Definition or description of a concept.]
```

For longer entries, use a `**Bold title** — prose` paragraph. The `**Title** — prose` pattern is a formatting convention, not itself a Resources entry — it would be out of scope there.

---

## Common mistakes

**Adding entries that belong inline** — if a concept only appears in one section, define it there. Resources is not a glossary for everything in the skill.

**Thin entries** — an entry that says "X is important" without defining what it means or how to apply it. Expand or cut.

**Redundant entries** — an entry that restates something fully covered by a Persona authority or rule. If removing it leaves the skill unchanged, cut it.
