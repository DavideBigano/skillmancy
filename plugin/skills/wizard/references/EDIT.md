# Skill editing

## 0 — Pre-flight

Check skill existence with `glob <expected-skill-directory>`.

If it does not exist, respond:

> Skill `<name>` not found at `<expected-skill-directory>`. Use `/wizard create <name>` to create it.

Do not continue.

If it exists, read the full skill.

---

## 1 — Scoping and setup

**Derive from context** — Skip questions that can be clearly answered by information in context. If this flow is being called after a review ask the user what points they want you to work on. 

**Scoping questions** — Use the `AskUserQuestion` tool to ask:

> How do you want to approach this edit?
> 1. **Top-down** — I have a goal in mind with no clear path to reach it.
> 2. **Bottom-up** — I already know the implementation details.

If option 1, ask:

> What is the end state you want to reach?
> How do you want the skill to behave specifically?
> What behavior/s do you specifically NOT want to change?

Otherwise, if option 2, ask:

> Which part/s do you want to change?
> How do they need to change?
> What part/s do you NOT want to touch?

If any answer is too vague to identify which sections need editing and why, do not proceed. Enter a refinement conversation on the unclear point until all answers are concrete and actionable.

**Determining the axis** — Based on what has been agreed, state where the skill sits:

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

Based on the scoping answers, determine which sections require changes: **task**, **persona**, **rules**, **resources**. Only work on sections genuinely affected — do not propose changes the user did not indicate.

For each affected section:

1. **Present the current behaviors** — quote or summarize the relevant parts of the existing skill.
2. **Propose the new behaviors** — if scoping provides enough direction, make concrete proposals. If not, ask targeted clarifying questions first.
3. **Refine until approved** — iterate through conversation until user approves.

Next, some section-specific clarification.

### Task changes

The model may use mermaid flowcharts as an helper to discuss the changes. Create flowcharts using the following command verbatim:

```bash
    ts=$(date +%Y-%m-%d-%H-%M-%S) && touch "skill-flow-${ts}.md" && cat > "skill-flow-${ts}.md" << 'EOF'
    <mermaid flowchart covering the skill's full task flow>
    EOF
```

### Persona changes

For each authority being added or changed state, with reference to points discussed:

- How it contributes
- Why it belongs here

For each authority being removed, explain what gap this leaves and whether anything needs to compensate.

If the corpus for a persona is thin, flag it explicitly and prompt the user to drop it or define it as a guideline.

### Guideline changes

For each guideline being added or changed state, with reference to points discussed:

- How it contributes
- Why it belongs here

For each guideline being removed, explain what gap this leaves and whether anything needs to compensate.

"Be direct, not diplomatic" is always the first guideline, verbatim. It requires no rationale.

If any guideline needs adjustment or if the they want to add their own, switch to a conversation. Phase ends with user approval for all guidelines.

---

### Resources changes

For each entry being added, changed, or removed state, with reference to points discussed:

- The concept, its type (shared vocabulary, framework, or assumption), and what it defines
- Why this change

For entries being removed, check whether any sections that pointed to them need to be updated inline.

For each assess if it has enough substance for a Resources entry VS inlining it. Then check for excessive redundancy. Flag findings for discussion


---

## File update

Once all proposed changes are approved, apply them using the Edit tool. Make targeted edits — change only what was agreed. Do not restructure sections not part of the approved changes.

If scope has grown to the point where a full rewrite is warranted, say so explicitly before proceeding.

Use `glob <skill-directory>/**/*` to list all files. Check each for dead references and flag any to the user — let them decide whether to remove, update, or create the missing file.
