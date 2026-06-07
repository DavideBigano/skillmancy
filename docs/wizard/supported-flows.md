# Wizard — Supported flows

The wizard skill supports three flows:

- **CREATE** — Used to create a new skill from scratch
- **EDIT** — Used to edit an existing skill
- **REVIEW** — Used to review a newly created or edited skill

Each flow:

- begins with a pre-flight check to confirm the skill exists (or doesn't)
- opens with a scoping step to establish intent and constrain the scope of work
- ends with a file operation (write or edit)

- [CREATE](#create)
- [EDIT](#edit)
- [REVIEW](#review)

---

## CREATE

**0 — Pre-flight** — Checks whether the skill already exists at the expected path. Stops if it does.

**1 — Scoping and setup** — Establishes what the skill is for, who it serves, and what is in/out of scope. Opens with an `AskUserQuestion` offering top-down (goal-first) or bottom-up (implementation-first) approach. Ends with axis determination and a user-chosen todo list of phases to tackle (Task, Persona, Guidelines, Resources, Writing) — phases can be addressed in any order.

**2 — Task** — Defines what the skill does and how. An optional mermaid flowchart (`skill-flow-<timestamp>.md`) can anchor iteration.

**3 — Persona** — Proposes named authorities from the corpus most relevant to the domain. For each, wizard states how it contributes and why it belongs. If the corpus for an authority is thin, flags it and prompts the user to drop it or convert it to a guideline.

**4 — Guidelines** — Proposes guidelines derived from everything established so far. Each is presented with how it contributes and why it belongs. "Be direct, not diplomatic" is always first, verbatim, no rationale required.

**5 — Resources** — Surfaces concepts needing consistent treatment across sections (vocabulary, frameworks, assumptions, guidance). Thin or redundant ones are flagged. Skipped if nothing surfaced.

**6 — Writing** — Checks skill existence again, then writes SKILL.md from the blank template and creates any reference sub-files if the task flow requires flow-based dispatch.

---

## EDIT

**0 — Pre-flight** — Confirms the skill exists. If not, stops. If yes, reads the full skill.

**1 — Scoping and setup** — Same top-down / bottom-up `AskUserQuestion` as CREATE; skips questions answerable from context. If called after a review, asks the user which findings to work on. Establishes scope and sets the axis.

**Change proposals** — Works through each affected section. For each: presents the current behavior, proposes the change with grounding in the scoping discussion, iterates until approved. Does not touch sections outside the agreed scope. Section-specific guidance:

- *Task changes* — optional mermaid flowchart available to anchor discussion
- *Persona changes* — for each authority added/changed, states how it contributes and why; flags thin corpus
- *Guideline changes* — for each guideline added/changed, states how it contributes and why; "Be direct, not diplomatic" always first
- *Resources changes* — checks substance (vs. inlining) and redundancy for each entry

**File update** — Applies approved changes with the Edit tool. Targeted edits only. Runs a dead-reference glob check before finalizing.

---

## REVIEW

**0 — Pre-flight** — Confirms the skill exists. If not, stops. If yes, reads the full skill.

**1 — Scoping** — Asks the user to choose a review goal via `AskUserQuestion`:
- **Base review** — routine review for detecting issues and inconsistencies
- **Diagnosing** — focused on a reported problem; iterates with the user until root cause is found
- **Improvement** — skill works; surface gaps and improvements, ignore violations

**2 — Review** — Six checks applied according to the chosen goal:
- *1a — Authorities review*: wizard's authorities correctly applied to the skill under review
- *1b — Internal authority consistency*: skill's own authorities applied consistently throughout
- *2a — Guidelines review*: wizard's guidelines correctly applied to the skill under review
- *2b — Internal guideline consistency*: skill's own guidelines applied consistently throughout
- *3a — Resources review*: wizard's resources correctly applied to the skill under review
- *3b — Internal resource consistency*: skill's own resources applied consistently throughout

Base review also runs a dead-reference glob check and marks findings.

**3 — Report** — Asks for format (One-line or Extended) then produces a structured report:

```
## Review: <skill-name>

**Axis:** [XX% conversational / YY% operational]

### Findings
**Finding [N]**:
**File/s**: [...]
**Issue**: [...]
**Recommendation**: [...]

### Suggestions
**Suggestion [N]**:
**File/s**: [...]
**Opportunity**: [...]
**Grounded in**: [specific authority, guideline, or resource entry]

### Summary
[N] finding(s), [M] suggestion(s). [One line: what's sound, what needs fixing, biggest opportunity.]
```

Suggestions must be grounded in the skill's own authorities, guidelines, or resources. After the report, directs the user to `/wizard edit <name>` with the report as edit scope.
