# Wizard — Key concepts

## What key concepts are

Key concepts is the canonical reference layer for a skill. It holds vocabulary, frameworks, assumptions, and construction guidance that need to be applied consistently across more than one section or file. It is optional — if nothing needs to be defined once and used in multiple places, skip it.

---

## The four types of entry

**Shared vocabulary** — terms or patterns the skill uses in a specific, non-obvious way. Define them once; reference them from wherever they're needed. If a term is only used in one section, define it there inline.

**Conceptual frameworks** — models the skill reasons from without re-explaining every time. A framework earns its place if multiple sections would otherwise have to reconstruct it independently.

**Operating assumptions** — things the skill takes as given about the context, the user, or the domain. Not rules (rules are conditions to satisfy), but starting conditions that constrain the design space.

**Shared construction guidance** — instructions for how to build or evaluate a skill section that multiple flows need to apply consistently. Wizard itself uses this type extensively: the Persona design, How to engage design, and Key concepts design entries are all shared construction guidance used by CREATE, EDIT, and REVIEW.

---

## When to add an entry

Add an entry when a concept needs to be applied consistently in more than one section, and each section would otherwise have to define it independently. The test: would two sections that both use this concept drift apart without a shared definition? If yes, add it. If they're each using it in a section-specific way with no overlap risk, leave it inline.

**Reinforcement vs. duplication** — Persona, rules, and key concepts can all address the same underlying concept at different abstraction levels. This is intentional reinforcement, not duplication. The test for genuine duplication: does each representation do something the others don't? If yes, keep all. If no, cut the weaker one.

---

## Format

Each entry follows this format:

```
**[Concept name]** — [Definition or description.]
```

For longer entries, use a `**Bold title** — prose` paragraph. The structure is consistent throughout Key concepts but is not itself a formal Key concepts entry (it would be out of scope there).

---

## Common mistakes

**Adding entries that belong inline** — if a concept only appears in one section, define it there. Key concepts is not a glossary for everything in the skill.

**Thin entries** — an entry that says "X is important" without defining what X means or how to apply it is not a key concept entry. Either expand it through conversation or cut it.

**Redundant entries** — an entry that restates something already fully covered by a Persona authority or a rule without adding anything distinct. Check each entry: if removing it from Key concepts left the skill unchanged (because the idea is already fully expressed elsewhere), it's redundant.
