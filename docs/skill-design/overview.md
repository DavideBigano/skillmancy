# Skill design — Overview

A skill is a structured prompt file that gives Claude Code a persistent, specialized capability. It is always written to SKILL.md and optionally supported by reference files loaded on demand.

Every skill is built from up to four sections, each with a distinct design responsibility:

- **[Persona](./persona.md)** — shapes what the skill *notices* and *prioritizes*. Built from lenses, each grounded in a named authority or stated as an explicit directive.
- **[Rules](./rules.md)** — explicit behavioral conditions the skill must satisfy. Each rule addresses a concrete behavior that would change if the rule were removed.
- **[Task](./task.md)** — the operational logic: argument dispatch, scoping questions, and the preconditions that gate output.
- **[Key concepts](./key-concepts.md)** — canonical reference layer for vocabulary, frameworks, and assumptions shared across more than one section. Optional.

A cross-cutting design tool applies throughout: the **[axis](./axis.md)** — the conversational/operational ratio that determines how much weight to give Persona and rules versus Task and output specs.
