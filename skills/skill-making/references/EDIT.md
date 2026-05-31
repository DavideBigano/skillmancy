# Skill editing

## Pre-flight

Use Glob to check whether `.claude/skills/<name>/` exists.

If it does not, respond:

> No skill named `<name>` found at `.claude/skills/<name>/`. Use `/skill-making create <name>` to create it.

Do not continue.

If it exists, read the full skill: SKILL.md and all files in `references/`, `examples/`, and `scripts/`. Every file must be read before the edit begins. The edit looks at the full skill, not just SKILL.md.

---

## Scoping

**Important**: skip asking a question if it's answer can be clearly derived from the context. If this flow is being called after a review ask the user what points they want you to work on. 

Use the `AskUserQuestion` tool to ask:

> How do you want to approach this edit?
> 1. **Top-down** — I have a goal in mind with no clear path to reach it.
> 2. **Bottom-up** — I already know the implementation details.

If option 1 is chosen, follow up by asking:

> 1. What is the end state you want to reach?
> 2. How do you want the skill to behave specifically?
> 3. What behaviour/s do you specifically NOT want to change?

Otherwise, if option 2 is chosen, follow up by asking:

> 1. Which part/s do you want to change?
> 2. How do they need to change?
> 3. What part/s do you NOT want to touch?

If any answer is too vague to identify which sections need editing and why, do not proceed. Enter a refinement conversation focused on the unclear point. The phase ends only when all three have concrete, actionable answers.

**Determining the axis position** — Based on what has been agreed, state where the skill sits:

```markdown
XX% conversational - YY% operational

[One-sentence rationale with references to the discussed matter.] 
```

If the user agrees, proceed. If they push back, discuss until agreed.

**Realining the axis** — At the end of each other phase, update the axis in light of the matter discussed in the phase (skip if unchanged):

```markdown
Based on our conversation i suggest an update for the axis:

XX% conversational - YY% operational

[One-sentence rationale for the change with references to the discussed matter.] 
```

---

## Change proposals

Based on the scoping answers, determine which of the following sections require changes: **task**, **persona**, **engagement rules**, **key concepts**. Only work on sections that are genuinely affected — do not propose changes to sections the user did not indicate need editing.

For each affected section, follow this pattern:

1. **Present the current behavior** — quote or summarize the relevant part of the existing skill.
2. **Propose the new behavior** — if the scoping answers provide enough direction, make a concrete proposal. If not, ask a targeted clarifying question first, then propose.
3. **Refine until approved** — if the user pushes back or wants changes, iterate through conversation. Do not move to the next section until the current one is approved.

Work through sections in this order: task → persona → engagement rules → key concepts. If the user asks to address them in a different order, allow it.

### Task changes

1. Ask the user to describe what the skill should do and how it should do it. Refine through conversation until the task is specific enough to be represented as a flowchart
2. Once the task flow is agreed, generate the filename: 

```
Bash(
    ts=$(date +%Y-%m-%d-%H-%M-%S) && touch "skill-flow-${ts}.md" && cat > "skill-flow-${ts}.md" << 'EOF'
    <mermaid flowchart covering the skill's full task flow>
    EOF
)
```

3. Present the file path to the user and wait for explicit approval before proceeding
4. When the user approves, remind them:

> Remember to delete `skill-flow-<timestamp>.md` once the skill is written.

### Persona changes

For each authority being added, changed, or replaced, state:

- The lens it contributes
- Why it belongs here — referencing a specific point from the scoping discussion or an existing part of the skill it connects to

For each authority being removed, explain what gap this leaves and whether anything needs to compensate.

If the corpus for this domain is thin, flag it explicitly and prompt the user to define the persona manually.

### Engagement rule changes

For each rule being added, changed, or removed, state:

- The rule
- Why this change — referencing the specific behavior or gap identified in scoping

---

### Key concepts changes

For each entry being added, changed, or removed, state:

- The concept, its type (shared vocabulary, framework, or assumption), and what it defines
- Why this change — referencing the specific gap or redundancy identified in scoping

For entries being removed, check whether any sections that pointed to them need to be updated inline.

---

## File update

Once all proposed changes are approved, apply them using the Edit tool. Make targeted edits — change only what was agreed. Do not restructure or rewrite sections that were not part of the approved changes.

If the scope of changes has grown to the point where a full rewrite is warranted, say so explicitly before proceeding.

Before finalizing, use `Glob(.claude/skills/<name>/**)` to list all files in the skill. Check each file for dead references and flag any to the user — let them decide whether to remove the reference, update it if stale, or create the missing file.
