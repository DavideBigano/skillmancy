# Wizard — Persona

The section that shapes what the skill notices and prioritizes, built from lenses each grounded in a named authority or stated as an explicit directive.

- [What a persona does](#what-a-persona-does)
- [Lenses](#lenses)
- [Synthesis paragraph](#synthesis-paragraph)
- [Axis relationship](#axis-relationship)

## What a persona does

A persona shapes what the skill *notices* and *prioritizes*. The model behaves differently because it sees the problem through different eyes, not because it was told to follow different rules. This is implicit behavior specification: through its lenses, the skill adopts instincts without each one being spelled out as a rule.

A persona that only says "you are an expert in X" is an adjective, not a persona. The distinction matters because adjectives don't change behavior — they just claim it.

---

## Lenses

Each lens is a distinct, non-overlapping analytical perspective. When grounded in a named authority, the format is:

```
**[Name]** gave you your [lens label]: [what this person sees that others miss, and how it shapes behavior].
```

**Authorities** — an authority is a named real-world person whose body of work grounds a lens. Using a named authority rather than a generic descriptor ("an expert in X") gives the model a concrete set of instincts to draw from: the person's actual thinking, priorities, and blind spots, not just the label. An authority is load-bearing when the model's behavior changes because of *who the person is* — their specific perspective, not just their domain. If swapping the name for another person in the same field would produce the same lens, the authority is too generic. If removing them entirely would leave a real gap in coverage, they belong.

**Evaluating a lens** — for each proposed lens, ask: what does this perspective see that a generic model wouldn't? If you can't answer concretely, the lens is not load-bearing and should be cut. Multiple lenses can address different facets of the same process and reinforce each other — that's intentional. Count alone is not a signal; coverage and distinctness are.

**Thin corpus** — if no well-known authority provides sufficient grounding for the domain, do not force weak attributions. Instead, state the lenses as explicit first-person directives — the mental models, the heuristics, the non-obvious constraints directly. A longer, more explicit persona is better than a short one that relies on the model inferring what you meant.

---

## Synthesis paragraph

The synthesis unifies the lenses into a single operating approach. It:

- Begins with "You work [approach]-first" or equivalent
- States the dominant operating approach and any hard constraints
- Names what this specialist never does

If the synthesis reads as a coherent operating approach, the lenses converge. If it reads as a list of parallel behaviors, the lenses may be too scattered. A slightly enumerative synthesis is acceptable if each lens is genuinely load-bearing.

---

## Axis relationship

A heavily conversational skill needs a rich, detailed Persona — the back-and-forth is where value is generated, and the persona governs the quality of that dialogue. A heavily operational skill can carry a lighter Persona; the artifact spec does more work. When editing a persona, check the axis first: the depth of persona investment should match the conversational weight of the skill.
