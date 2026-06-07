# Skill creation

- [0 — Pre-flight](#0--pre-flight)
- [1 — Scoping and setup](#1--scoping-and-setup)
- [2 — Task](#2--task)
- [3 — Persona](#3--persona)
- [4 — Guidelines](#4--guidelines)
- [5 — Resources](#5--resources)
- [6 — Writing](#6--writing)

## 0 — Pre-flight

Check skill existence with `glob <expected-skill-dir>`.

If it does, respond:

> A skill named `<name>` already exists at `<expected-skill-dir>`. Use `/wizard edit <name>` if you want to modify that or choose a different name for the skill.

Do not continue.

---

## 1 — Scoping and setup

**Scoping questions** — Use the `AskUserQuestion` tool to ask:

> How do you want to approach creating the skill?
> 1. **Top-down** — I have a goal in mind with no clear path to reach it.
> 2. **Bottom-up** — I already know the implementation details.

If option 1, ask:

> What is the end goal you want to reach?

If option 2, ask:

> What tasks will the skill execute?

In both cases then ask: 

> Who is the skill for — the person invoking it and their context?
> What is in scope and what is out of scope?

If any answer is too vague to identify which sections need editing and why, do not proceed. Enter a refinement conversation on the unclear point until all answers are concrete and actionable.

**Determining the axis** — Based on what has been agreed, state where the skill sits:

```markdown
XX% conversational - YY% operational

[One-sentence rationale with references to the discussed matter.] 
```

If the user agrees, proceed. If they push back, discuss until agreed.

**Realigning the axis** — At the end of each other phase, update the axis in light of the matter discussed in the phase (skip if unchanged):

```markdown
Based on our conversation i suggest an update for the axis:

XX% conversational - YY% operational

[One-sentence rationale for the change with references to the discussed matter.] 
```

**Next steps** — Ask the user what they want to tackle:
- [ ] Task
- [ ] Persona
- [ ] Rules
- [ ] Resources
- [ ] Writing

Create a todo of the chosen phases; each can be tackled in or out of order.

---

## 2 — Task

Ask the user to describe what the skill should do and how it should do it. Refine through conversation until the user approves.

To aid in this step you can prompt the user to ask for a flowchart of the task. The two of you can iterate on the design using it as an anchor.

The flowchart is written with `mermaid`. You can generate a file holding the chart which the user will be able to render and visualize.

To generate the flowchart run this verbatim:

```bash
    ts=$(date +%Y-%m-%d-%H-%M-%S) && touch "skill-flow-${ts}.md" && cat > "skill-flow-${ts}.md" << 'EOF'
    <mermaid flowchart covering the skill's full task flow>
    EOF
```

Present the file path to the user and wait for explicit approval.

If nothing surfaced skip this section.

---

## 3 — Persona

Draw from what was established previously. Propose the authorities from your corpus most relevant to the subject. For each, state, with reference to points discussed::

- How it contributes
- Why it belongs here

If the corpus for a persona is thin, flag it explicitly and prompt the user to drop it or define it as a guideline.

Ask the user which to keep. If proposed authorities don't fit discuss alternatives. 

If nothing surfaced skip this section.

---

## 4 — Guidelines

Draw from what was established previously. Propose a set of guidelines to drive the skill's behavior. For each state, with reference to points discussed::

- How it contributes
- Why it belongs here

"Be direct, not diplomatic" is always the first guideline, verbatim. It requires no rationale.

If any guideline needs adjustment or if the they want to add their own, switch to a conversation. Phase ends with user approval for all guidelines.

If nothing surfaced skip this section.

---

## 5 — Resources

Draw from what was established previously. Identify the concepts that surfaced across multiple sections: shared vocabulary, conceptual frameworks, operating assumptions, and construction guidance the skill takes for granted.

Present the list and ask whether anything is missing. Refine until complete.

For each concept, assess whether it has enough substance for a Resources entry — meaning it isn't already fully captured by an authority, a guideline, or task step. Flag thin or redundant concepts explicitly; expand through conversation or drop them.

If nothing surfaced skip this section.

---

## 6 — Writing

Check skill existence again with `glob <expected-skill-directory>`. If it exists, ask the user for a different skill name or placement.

Populate `<skill-directory>/SKILL.md` using the Write tool. Use the blank skill template as the starting point. Populate every section with what was agreed.

If the task flow includes mode-based dispatch or conditional loading, create the corresponding sub-files, following the multi-file structure pattern in SKILL.md's Resources.
