# Wizard — Guidelines

User-defined directions for the model to follow, described positively, applying across the whole skill.

- [What guidelines do](#what-guidelines-do)
- [Format](#format)
- [The fixed first guideline](#the-fixed-first-guideline)
- [Adding, changing, and removing guidelines](#adding-changing-and-removing-guidelines)
- [Axis relationship](#axis-relationship)

## What guidelines do

Guidelines cover behavior the model would get wrong without explicit direction — framing, priorities, tradeoffs — that isn't implicit in the authorities and doesn't belong in the task flow. Test: if removed, would behavior change observably? If not, it's a preference — cut it.

---

## Format

Each guideline follows this structure:

```
**[Guideline label]** — [No-nonsense description]. (Yes: [positive example, ...] / No: [negative example, ...])
```

The label is a short imperative phrase. The description must point toward a concrete approach or choice — not a vague aspiration. "Be thorough" is not a guideline. "Do not begin drafting until scope is clear; ask follow-up questions rather than assuming" is.

The Yes/No examples are optional when concrete examples are hard to give — a clear description alone is enough. Where examples are included, frame them positively first.

---

## The fixed first guideline

"Be direct, not diplomatic" is always the first guideline, verbatim:

```
**Be direct, not diplomatic** — Say what needs to be said, clearly and with reason. Pushback is not a reflex: if a choice is well-reasoned and the tradeoffs are understood, say so and move forward. (Yes: ["This design has no behavioral payoff — cut it"] / No: ["That's interesting, maybe consider..."])
```

Always present, always first, always verbatim.

---

## Adding, changing, and removing guidelines

**Adding** — state the guideline and the behavior or risk it addresses. No grounded rationale = preference in disguise.

**Changing** — state what the guideline currently does, what gap or over-specification it creates, and what the replacement achieves differently.

**Removing** — state what the guideline was preventing. If a real failure mode is now unguarded, either keep it or explain what covers it.

---

## Axis relationship

Guidelines carry more weight in operational skills; in conversational skills the authorities handle more implicitly. When the axis shifts, audit: some guidelines may become redundant, new ones may be needed.
