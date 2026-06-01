# Skill design — Task

The operational logic section: argument dispatch, scoping questions, and the preconditions that gate output.

- [What the Task section does](#what-the-task-section-does)
- [Multi-flow dispatch](#multi-flow-dispatch)
- [Axis relationship](#axis-relationship)

## What the Task section does

Task defines *what* the skill does: how it interprets its argument, what it asks before acting, and what condition gates output. Where Persona and rules shape behavior, Task specifies execution.

---

## Multi-flow dispatch

When a skill has distinct flows rarely needed together, dispatch routes the argument to a reference file rather than encoding the full flow inline:

```markdown
Once flow and name are confirmed, use the Read tool to load the corresponding logic file:

- **create** → [CREATE.md](./references/CREATE.md)
- **edit** → [EDIT.md](./references/EDIT.md)
- **review** → [REVIEW.md](./references/REVIEW.md)
```

The SKILL.md dispatcher stays small and always-loaded; flow-specific logic is read on demand.

**Auto-detect fallback** — if a bare argument is given with no explicit flow, check for the relevant artifact and confirm before proceeding. Always confirm; never assume.

**No-argument handling** — always specify what happens with no argument: show a usage line and stop, or begin a scoping conversation. Never silently fail.

---

## Axis relationship

Operational skills have heavier Task sections — tighter preconditions, explicit artifact structure. Conversational skills have lighter ones; value is in the dialogue. When the axis shifts, Task is the first section to rebalance.
