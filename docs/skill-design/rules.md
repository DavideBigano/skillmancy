# Wizard — Rules

Explicit behavioral conditions the skill must satisfy — governing sequencing and output quality rather than conversation style.

- [What rules do](#what-rules-do)
- [Format](#format)
- [The fixed first rule](#the-fixed-first-rule)
- [Adding, changing, and removing rules](#adding-changing-and-removing-rules)
- [Axis relationship](#axis-relationship)

## What rules do

Rules are explicit conditions the skill must satisfy — making failure modes explicit rather than leaving them to the persona. Not style guidance or tone instructions; most govern sequencing and output quality. Test: if removed, would behavior change observably? If not, it's a preference — cut it.

---

## Format

Each rule follows this structure:

```
**[Rule name]** — *if* [condition to check] *then* [concrete counter-action]
```

The rule name is a short imperative phrase. The body must imply a concrete action or refusal — not a vague aspiration. "Be thorough" is not a rule. "Do not begin drafting until scope is clear; ask follow-up questions rather than assuming" is.

---

## The fixed first rule

"Be direct, not diplomatic" is always the first rule, verbatim:

```
**Be direct, not diplomatic** — Your job is to produce the best possible outcome, not to protect the user's feelings. If a specification is vague, say so. If a proposed approach has a real problem, name it clearly and explain why. If the direction is wrong, push back — with a reason, not just a preference. That said, pushback is not a reflex: if a choice is well-reasoned and the tradeoffs are understood, say so and move forward. Contrarianism is as useless as sycophancy.
```

No rationale needed. Always present, always first, always verbatim.

---

## Adding, changing, and removing rules

**Adding** — state the rule and the behavior or risk it addresses, referenced from the prior discussion. No grounded rationale = preference in disguise.

**Changing** — state what the rule currently does, what gap or over-specification it creates, and what the replacement achieves differently.

**Removing** — state what the rule was preventing. If a real failure mode is now unguarded, either keep it or explain what covers it.

---

## Axis relationship

Rules carry more weight in operational skills; in conversational skills the persona handles more implicitly. When the axis shifts, audit: some rules may become redundant, new ones may be needed.
