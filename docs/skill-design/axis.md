# Skill design — Axis

The conversational/operational ratio that positions a skill between pure dialogue and pure artifact generation, and determines how much weight to give each section.

- [What the axis is](#what-the-axis-is)
- [How to use it](#how-to-use-it)
- [Axis relationship to each section](#axis-relationship-to-each-section)

## What the axis is

Every skill sits somewhere between fully conversational (value lives in the dialogue) and fully operational (value lives in the artifact). The axis is the explicit statement of that position.

```
XX% conversational - YY% operational

[One-sentence rationale referencing the specific discussion.]
```

The axis is a design tool, not an output field — it never appears in the finished skill file.

---

## How to use it

Establish the axis once intent and scope are clear. Revisit it whenever the design discussion meaningfully shifts the balance; skip the update if nothing has changed.

The axis determines how much weight to give each section:

- **High conversational weight** → richer Persona, lighter Task; the back-and-forth is where value is generated
- **High operational weight** → lighter Persona, heavier Task; the artifact spec does more of the work

---

## Axis relationship to each section

**Persona** — conversational skills need a rich, detailed Persona; operational skills can carry a lighter one.

**Rules** — carry more weight in operational skills, where consistent output depends more on explicit conditions. In conversational skills, the Persona does more of this work implicitly.

**Task** — operational skills have heavier Task sections (tighter preconditions, explicit artifact structure); conversational skills have lighter ones.

**Key concepts** — not strongly axis-dependent, but axis shifts can make some entries redundant or reveal new gaps.
