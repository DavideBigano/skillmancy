# Wizard — Task

The operational logic section: argument dispatch, scoping questions, and the preconditions that gate output.

- [What the Task section does](#what-the-task-section-does)
- [Structure](#structure)
- [Multi-flow dispatch](#multi-flow-dispatch)
- [Axis relationship](#axis-relationship)

## What the Task section does

Task is the operational logic section of a skill. Where Persona and How to engage shape *how* the skill behaves, Task defines *what* it does: how it interprets its argument, what it asks before acting, and what condition must be met before output begins.

---

## Structure

A Task section typically contains three things:

**Argument dispatch** — how the skill interprets what it was invoked with. For single-purpose skills, this may be minimal. For multi-flow skills, this is a full dispatch block routing different arguments to different flows or reference files.

**Scoping questions** — what the skill asks before doing anything. Questions should target goals, not tasks. "What is the end goal you want to reach?" surfaces intent; "What tasks will the skill execute?" surfaces implementation. Both are valid approaches — the right one depends on the axis and what stage the user is at.

**Preconditions for output** — the explicit condition that must be met before the skill begins producing its artifact. State this as a hard gate: "Do not begin drafting until X and Y are clear." Without a precondition, the skill starts producing output on insufficient information.

---

## Multi-flow dispatch

When a skill has distinct flows rarely needed together, dispatch routes the argument to a reference file rather than encoding the full flow inline:

```markdown
Once flow and name are confirmed, use the Read tool to load the corresponding logic file:

- **create** → [CREATE.md](./references/CREATE.md)
- **edit** → [EDIT.md](./references/EDIT.md)
- **review** → [REVIEW.md](./references/REVIEW.md)
```

This is progressive disclosure applied to the Task section: the SKILL.md dispatcher stays small and always-loaded; the flow-specific logic is read on demand.

**Auto-detect fallback** — when a bare argument is given with no explicit flow, the Task section can check for the relevant artifact and confirm with the user before proceeding. Always confirm; never assume.

**No-argument handling** — always specify what happens if the skill is invoked with no argument. Either show a usage line and stop, or begin a scoping conversation. Never silently fail.

---

## Axis relationship

An operational skill has a heavier Task section — more specific output specs, tighter preconditions, explicit artifact structure. A conversational skill has a lighter Task section; the value is in the dialogue, not the artifact, so the precondition is softer and the output spec is minimal. When the axis shifts, Task is the section most likely to need rebalancing.
