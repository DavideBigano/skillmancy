# skill-making — session state

Working thread for iterative improvement of the `skill-making` skill at `.claude/skills/skill-making/`.

---

## Files in scope

```
.claude/skills/skill-making/
├── SKILL.md
├── references/
│   ├── CREATE.md
│   ├── EDIT.md
│   ├── REVIEW.md
│   └── tooling-catalog.md
└── examples/
    ├── token-efficiency-patterns.md
    └── tooling-catalog-examples.md
```

---

## Changes made — previous session (compacted)

All changes in this session were to **SKILL.md** only.

### "Show, don't describe" rule — extended
Extended to cover tool invocations and code snippets, not just output format conventions:

> The same applies to tool invocations and code: write the exact call (`Glob(.claude/skills/<name>/**)`, `Bash(git status)`) or a concrete snippet rather than describing what the invocation or code should look like.

### Key concepts design — "When to add" reframed
Old framing said "if this lived in two places, the two copies would drift" — implying all cross-section appearance was duplication. Replaced with a framing that explicitly distinguishes reinforcement from duplication:

> Persona, rules, and key concepts can all touch the same underlying concept at different abstraction levels — that's intentional reinforcement, not duplication. Other sections may restate part of a key concept when the restatement serves a purpose specific to that section.

### Rules reframed as conditions
"What rules do" paragraph rewritten. Old framing positioned rules as interaction directives. New framing: rules are explicit conditions the skill must satisfy — on the work, on sequencing, on output quality. The distinction matters because most rules govern the work itself, not how the skill talks to the user.

### Bold-title paragraph structure applied throughout
All Key concepts sub-sections were refactored to use consistent `**Bold title** — prose` format (replacing a mix of prose paragraphs, bullet lists with no openers, and period-terminated headers). Applied to: Skill structure, The conversational/operational axis, Persona design, How to engage design, Key concepts design, Full skill vs. SKILL.md, Multi-file structure, Token efficiency patterns, External tooling and skill UX, Blank skill template.

### Blank skill template — Key concepts placeholder updated
```markdown
[Optional. Add entries for vocabulary, frameworks, assumptions, or construction guidance reused across sections. See Key concepts design for when and how.]
```

---

## Changes made — this session

### CREATE.md

| Area | Change |
|---|---|
| Phase ordering | Restructured as bold-title paragraphs: "Phase ordering" (sequence) + "Phase traversal" (don't advance until phase complete, unless user requests) |
| Phase 1 — Scoping | Added `AskUserQuestion` with top-down vs bottom-up approach; top-down asks for end goal, bottom-up asks for implementation details; both then ask who it's for and what's in/out of scope |
| Axis | Axis determination added at end of Scoping phase; per-phase realignment blocks added at end of phases 4 and 5 |
| Phase 2 — Task definition | Flowchart made optional ("you can prompt the user to ask for a flowchart"); bash heredoc command provided for generating the file |
| Phase 3 — Persona | "at least three" changed from hard requirement to "at least three as a rule of thumb" |
| Typo | "I have a goal in mind no clear path to reach it" → "with no clear path" |

**Bash heredoc command (introduced in CREATE and EDIT):**
```bash
ts=$(date +%Y-%m-%d-%H-%M-%S) && touch "skill-flow-${ts}.md" && cat > "skill-flow-${ts}.md" << 'EOF'
<mermaid flowchart covering the skill's full task flow>
EOF
```
This replaced the previous two-step `echo filename` → `Write(path)` pattern.

### EDIT.md

| Area | Change |
|---|---|
| Scoping | Added `AskUserQuestion` with top-down vs bottom-up approach (mirrors CREATE); "Important: skip asking a question if it can be clearly derived from context" added — especially relevant when called after a review |
| Axis | Axis determination added at end of Scoping; per-section axis discussions inside Persona changes and Engagement rule changes removed (consolidated into Scoping) |
| Task changes | Same bash heredoc command as CREATE |
| Typos | "with no clear path", "How do you want", "NOT want to change", "do you want to change", "do you NOT want to touch" |

### REVIEW.md

| Area | Change |
|---|---|
| Scoping | Added `AskUserQuestion` tool call |
| Report | Added a two-step flow: `AskUserQuestion` to select report format (One-line vs Extended) before producing the report |
| Report format | Restructured from area-grouped findings to numbered findings/suggestions with per-item **File/s** attribution; "One-line if requested" embedded in each field description |
| Typo | "Oneline" → "One-line" throughout |

**Old report format:**
```
**[Area]**
- [Finding: ...] → [Recommendation]
```

**New report format:**
```
**[Finding N]**: 
**File/s**: [...]
**Issue**: [... One-line if requested.]
**Recommendation**: [... One-line if requested.]
```

---

## Open items

### Minor — CREATE.md Phase 4 axis block missing
Phase 4 ends with:
> In light of the matter discussed in this phase update the axis (skip if unchanged):

But the markdown block that appears in Phase 5 is absent. Phase 5 has:
```markdown
Based on our conversation i suggest an update for the axis:

XX% conversational - YY% operational

[One-sentence rationale for the change with references to the discussed matter.] 
```
Phase 4 needs the same block added after that line.

### Suggestion (from earlier checklist, not acted on)
Factor the duplicated flowchart bash + Write pattern in CREATE.md and EDIT.md into `scripts/new-flowchart.sh`. Currently both files carry identical instructions; a script would eliminate drift risk. Not yet decided whether to act on this.

---

## Key design decisions (rationale on record)

**Cross-section reinforcement is intentional.** Persona, rules, and key concepts can all address the same underlying concept at different abstraction levels. The right test for genuine duplication is: does each representation do something the others don't? If yes, keep all; if no, cut the weaker one.

**Rules are conditions, not interaction directives.** Reframing rules as "explicit conditions the skill must satisfy" is more general and more accurate than "how to interact with the user." Most rules in practice govern sequencing and output quality, not conversation style.

**Axis integrated into flow, not embedded per-section.** The old pattern established the axis inside each of Persona changes and Engagement rule changes independently. The new pattern establishes it once in Scoping and updates it at phase boundaries. Cleaner, less repetitive, and less likely to produce drift between instances.

**Flowchart made optional in CREATE.** For simpler skills the full flowchart step is overhead. The instruction now prompts the designer to offer it rather than mandating it.

**Bold-title paragraph structure was deliberately not codified.** The structure (`**Title** — prose`) is used consistently throughout Key concepts but was explicitly decided against adding as a formal entry in Key concepts design. Rationale: it would introduce information that's out of scope for that section.

**"Rules as conditions" framing originated with the user.** The reframing of rules as "explicit conditions the skill must satisfy" came from the user's own observation: "wouldn't the idea that a rule is a strong condition to check for be a better generalization for what rules are?" — not a proposal from the assistant. This is the grounding insight behind the How to engage design entry.
