# Skill creation

## Pre-flight

Use Glob to check whether `.claude/skills/<name>/SKILL.md` already exists.

If it does, respond:

> A skill named `<name>` already exists at `.claude/skills/<name>/`. Use `/skillmancy:wizard edit <name>` to modify it.

Do not continue.

---

## Phase ordering

**Phase ordering** — phases have a default order, on user request the order can change:
1. Scoping
2. Task definition
3. Persona
4. Rules
5. Key concepts
6. Writing. 

**Phase traversal** — When in a phase, do not move to the next one until the current is complete unless the user explicitly requests it.

---

## Phase 1 — Scoping

Use the `AskUserQuestion` tool to ask:

> How do you want to approach creating the skill?
> 1. **Top-down** — I have a goal in mind with no clear path to reach it.
> 2. **Bottom-up** — I already know the implementation details.

If option 1 is chosen, follow up by asking:

> 1. What is the end goal you want to reach?

Otherwise, if option 2 is chosen, follow up by asking:

> 1. What tasks will the skill execute?

In both cases then ask: 

> 2. Who is the skill for — the person invoking it and their context?
> 3. What is in scope and what is out of scope?

If any answer is too vague to identify which sections need editing and why, do not proceed. Enter a refinement conversation on the unclear point until all answers are concrete and actionable.

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

## Phase 2 — Task definition

Ask the user to describe what the skill should do and how it should do it. Refine through conversation until the user approves.

To aid in this step you can prompt the user to ask for a flowchart of the task. The two of you can iterate on the design using it as an anchor.

The flowchart is written with `mermaid`. You can generate a file holding the chart which the user will be able to render and visualize.

To generate the flowchart run:

```
Bash(
    ts=$(date +%Y-%m-%d-%H-%M-%S) && touch "skill-flow-${ts}.md" && cat > "skill-flow-${ts}.md" << 'EOF'
    <mermaid flowchart covering the skill's full task flow>
    EOF
)
```

Present the file path to the user and wait for explicit approval.

When the user approves, remind them:

> Remember to delete `skill-flow-<timestamp>.md` once the skill is written.

---

## Phase 3 — Persona

Draw from what was established in Phases 1–2. Propose the authorities from your corpus most relevant to the subject. For each, state:

- The lens it contributes
- Why it belongs here — referencing a specific point from the scoping or task definition discussion

If the corpus is thin, show the most relevant available but flag it explicitly:

> The corpus here is limited — these are the closest matches, but you may want to define parts of the persona manually.

Ask the user which are worth keeping (at least three as a rule of thumb). If proposed authorities don't fit, switch to a conversation to find alternatives. Custom additions — first-person directives, explicit mental models — are always welcome alongside or instead of named authorities.

---

## Phase 4 — Rules

Propose a set of rules based on everything gathered in Phases 1–3. For each rule:

- State the rule
- Explain why it is there — referencing the specific behavior or risk it addresses from the prior discussion

"Be direct, not diplomatic" is always the first rule, verbatim. It requires no rationale.

If any rule needs adjustment, switch to a conversation. The phase ends when the user approves the full rule set.

In light of the matter discussed in this phase update the axis (skip if unchanged):

---

## Phase 5 — Key concepts (optional)

Based on everything discussed in Phases 1–4, identify concepts that surfaced across multiple sections: shared vocabulary, conceptual frameworks, operating assumptions, and construction guidance the skill takes for granted.

Present the list and ask whether anything is missing. Refine until complete.

For each concept, assess whether it has enough substance for a Key concepts entry — meaning it isn't already fully captured by a Persona lens, a rule in Rules, or a step in Task. Flag thin or redundant concepts explicitly; expand through conversation or drop them.

If nothing surfaced from the discussion and the user has nothing to add, skip this section.

In light of the matter discussed in this phase update the axis (skip if unchanged):

```markdown
Based on our conversation i suggest an update for the axis:

XX% conversational - YY% operational

[One-sentence rationale for the change with references to the discussed matter.] 
```

If the user agrees, proceed. If they push back, discuss until agreed.

---

## Phase 6 — Writing

**Folder creation** — Check whether `.claude/skills/<name>/` already exists. If it does, use `<name>_01` for the remainder of this phase. Then create the directory:

```bash
mkdir .claude/skills/<name>
```

Populate `.claude/skills/<name>/SKILL.md` using the Write tool. Use the blank skill template in SKILL.md as the starting point. Populate every section with what was agreed in Phases 1–5.

If the task flow includes mode-based dispatch or conditional loading, create the corresponding sub-files now, following the multi-file structure pattern in SKILL.md's Key concepts.

Before finalizing, `Glob(.claude/skills/<name>/**)` to list all files. Check each for dead references and flag any to the user — let them decide whether to remove, update, or create the missing file.

Remind the user:

> Remember to delete `skill-flow-<timestamp>.md`.
