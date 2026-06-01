# Wizard — Design rationale

Non-obvious decisions and why they were made. Read this before editing the skill to avoid undoing intentional choices.

---

**Cross-section reinforcement is intentional, not duplication.** Persona, rules, and Key concepts can address the same concept at different abstraction levels. Test: does each representation do something the others don't? If no, cut the weaker one.

**Rules are conditions, not interaction directives.** Rules are conditions on the work, sequencing, and output quality — not interaction style guidance. When writing or reviewing rules, ask "what condition does this enforce?" not "how does this change the tone?"

**Axis integrated into flow, not embedded per-section.** The axis is established once in Scoping and updated at phase boundaries. The older per-section pattern caused drift between instances and redundant re-establishment.

**Flowchart is optional in CREATE.** For simpler skills, the flowchart step is overhead. Wizard offers it rather than mandating it — the optionality is deliberate.

**Bold-title paragraph structure (`**Title** — prose`) was deliberately not codified in Key concepts.** Used consistently throughout Key concepts but not added as a formal entry — it's a formatting convention, out of scope for a section that covers vocabulary and frameworks.

**The "show, don't describe" rule covers tool invocations and code, not just output formats.** The rule was extended beyond output format conventions to include tool calls (`Glob(.claude/skills/<name>/**)`) and code snippets. When writing new instructions, give the exact call or concrete snippet — not a prose description of what the call should look like.

**Output path is currently hardcoded to `.claude/skills/`.** Known limitation — plugin repos use a different layout. Tracked in todo; do not work around by editing the path in multiple places.

**The blank skill template in SKILL.md is the canonical starting point for new skills.** The Key concepts placeholder text ("Optional. Add entries for vocabulary, frameworks, assumptions, or construction guidance reused across sections. See Key concepts design for when and how.") signals both the optional nature and the pointer to the design section.
