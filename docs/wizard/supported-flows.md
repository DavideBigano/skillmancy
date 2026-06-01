# Wizard — Supported flows

The wizard skill support three flows:

- **CREATE** — Used to create a new skill from scratch
- **EDIT** — Used to edit an existing skill
- **REVIEW** — Used to review a newly created or edited skill

Each flow:

- begins by reading the relevant skill files from disk before doing anything else
- opens with a scoping step to establish intent and constrain the scope of work
- advances through discrete steps or phases, not moving forward until the current one is complete
- ends with a file operation (write or edit) and a dead-reference check

- [CREATE — six phases](#create--six-phases)
- [EDIT — three steps](#edit--three-steps)
- [REVIEW — three steps](#review--three-steps)

---

## CREATE — six phases

Phases run in order by default. The user can request a different order. **Do not advance to the next phase until the current one is complete** unless the user explicitly requests it.

### Phase 1 — Scoping
Establishes what the skill is for, who it serves, and what is in/out of scope. Opens with an `AskUserQuestion` offering top-down (goal-first) or bottom-up (implementation-first) approach. Ends with axis determination — the first time the axis is set.

### Phase 2 — Task definition
Defines what the skill does and how. An optional mermaid flowchart can be generated as a shared anchor for iteration. The flowchart is written to a timestamped file (`skill-flow-<timestamp>.md`) the user can render; it is deleted once the skill is written.

### Phase 3 — Persona
Proposes named authorities from the corpus most relevant to the domain. For each, wizard states the lens it contributes and why it belongs, grounded in the scoping discussion. If the corpus is thin, flags it and invites manual first-person directives.

### Phase 4 — Rules
Proposes rules derived from Phases 1–3. Each rule is presented with the specific behavior or risk it addresses. "Be direct, not diplomatic" is always the first rule, requires no rationale. Ends with an axis update.

### Phase 5 — Key concepts (optional)
Surfaces concepts that appeared across multiple phases and need consistent treatment: shared vocabulary, frameworks, operating assumptions, construction guidance. Thin or redundant concepts are flagged for expansion or removal. Skipped if nothing surfaced. Ends with an axis update.

### Phase 6 — Writing
Creates `.claude/skills/<name>/` (or the configured output directory), writes SKILL.md from the blank template, and creates any reference sub-files if the task flow requires flow-based dispatch. Runs `Glob(.claude/skills/<name>/**)` before finalizing to check for dead references.

---

## EDIT — three steps

No numbered phases; the flow is: **Scoping → Change proposals → File update**.

**Scoping** — reads the full skill first (SKILL.md + all references/, examples/, scripts/). Opens with the same top-down / bottom-up `AskUserQuestion` as CREATE, but skips questions whose answers are clearly derivable from context (especially relevant when called after a review). Establishes which sections are in scope and which are not. Sets the axis.

**Change proposals** — works through affected sections in order: task → persona → rules → key concepts. For each: presents the current behavior, proposes the change, iterates until approved. Does not touch sections outside the agreed scope.

**File update** — applies approved changes with the Edit tool. Targeted edits only — does not restructure sections that weren't part of the agreed changes. Runs the same dead-reference Glob check as CREATE before finalizing.

---

## REVIEW — three steps

**Scoping → Review → Report → Handoff**.

**Scoping** — reads the full skill first. Asks the user to choose a review goal via `AskUserQuestion`:
- **Pre-ship** — blockers only; every rule violation stops the ship
- **Diagnosing** — focused on a reported symptom; lighter pass elsewhere
- **Health check** — balanced; findings and suggestions weighted equally
- **Improvement** — skill works; leads with suggestions, treats findings as secondary

**Review** — two checks applied according to the chosen goal:
- *Check 1 — Rule checks*: each How to engage rule applied as pass/fail
- *Check 2 — Lens review*: each Persona authority's lens applied to the full skill; Key concepts provides the shared vocabulary the lenses think in

**Report** — asks for format (One-line or Extended) then produces a structured report:

```
## Review: <skill-name>

**Axis:** [assessed position]

### Findings
**[Finding N]**:
**File/s**: [...]
**Issue**: [...]
**Recommendation**: [...]

### Suggestions
**[Suggestion N]**:
**File/s**: [...]
**Opportunity**: [...]
**Grounded in**: [specific authority, rule, or key concept]

### Summary
[N] finding(s), [M] suggestion(s). [One line: what's sound, what needs fixing, biggest opportunity.]
```

Suggestions must be grounded in the skill's own persona, rules, or key concepts — no free-floating suggestions.

**Handoff** — if findings exist, directs the user to `/skillmancy:wizard edit <name>` with the findings as the edit scope.
