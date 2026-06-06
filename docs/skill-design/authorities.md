# Wizard — Authorities

The section that shapes what the skill notices and prioritizes, built from named real-world persons or works whose corpus the model was trained on.

- [What authorities do](#what-authorities-do)
- [Authorities](#authorities)
- [Synthesis paragraph](#synthesis-paragraph)
- [Axis relationship](#axis-relationship)

## What authorities do

Authorities shape what the skill *notices* and *prioritizes* — implicit behavior specification through corpus, not explicit rules. "You are an expert in X" is an adjective, not an authority: adjectives don't change behavior, they just claim it.

---

## Authorities

Each authority is a named real-world person or work (book, guide, essay, ...) contributing a distinct, non-overlapping perspective. The format is:

```
**[Name/work]** gave you your [perspective label]: [what it sees that others miss, and how it shapes behavior].
```

**Corpus** — The body of knowledge tied to a person or work that the model was already trained on. Load-bearing test: would swapping for another person or work in the same field change behavior? If no, the authority is too generic.

**Evaluating an authority** — Ask: what does this perspective see that a generic model wouldn't? If you can't answer concretely, cut it. Distinctness matters; count alone is not a signal.

**Thin corpus** — If no well-known authority fits the domain, move the authority to Guidelines with explicit first-person directives instead. A longer, explicit guideline beats a short authority that relies on inference.

---

## Synthesis paragraph

The synthesis unifies the authorities into a single operating approach:

- Begins with "You work [approach]-first" or equivalent
- States the dominant operating approach and any hard constraints
- Names what this specialist never does

If it reads as a list of parallel behaviors rather than a coherent approach, the authorities may be too scattered. A slightly enumerative synthesis is acceptable if each authority is genuinely load-bearing.

---

## Axis relationship

Conversational skills need richer Authorities — the dialogue is where value is generated. Operational skills can carry a lighter section; the artifact spec does more work. Match authority depth to conversational weight.
