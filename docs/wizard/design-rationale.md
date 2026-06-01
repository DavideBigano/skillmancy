# Wizard — Design rationale

Non-obvious decisions and why they were made. Read this before editing the skill to avoid undoing intentional choices.

---

**Cross-section reinforcement is intentional, not duplication.** Persona, How to engage rules, and Key concepts can all address the same underlying concept at different abstraction levels. The test for genuine duplication is: does each representation do something the others don't? If yes, keep all. If no, cut the weaker one. Don't conflate "appears in two places" with "redundant."

**Rules are conditions, not interaction directives.** How to engage rules are explicit conditions the skill must satisfy — on the work, on sequencing, on output quality. The older framing positioned them as interaction style guidance. The current framing is more general and more accurate: most rules in practice govern sequencing and output quality, not how wizard talks to the user. When writing or reviewing rules, ask "what condition does this enforce?" not "how does this change the tone?"

**Axis integrated into flow, not embedded per-section.** The axis is established once in Scoping and updated at phase boundaries. An older pattern placed axis discussions inside the Persona and Engagement rule change sections independently. That caused drift between instances and redundant re-establishment. The current pattern is cleaner and less likely to diverge.

**Flowchart is optional in CREATE.** For simpler skills, the full flowchart step is overhead. The instruction prompts wizard to *offer* the flowchart rather than mandate it. Editors should resist re-mandating it — the optionality is deliberate.

**Bold-title paragraph structure (`**Title** — prose`) was deliberately not codified in Key concepts.** The structure is used consistently throughout Key concepts but was explicitly decided against adding as a formal entry in Key concepts design. Reason: it would be out of scope for that section, which covers vocabulary and frameworks the skill reasons from — not formatting conventions.

**The "show, don't describe" rule covers tool invocations and code, not just output formats.** The rule was extended beyond output format conventions to include tool calls (`Glob(.claude/skills/<name>/**)`) and code snippets. When writing new instructions, give the exact call or concrete snippet — not a prose description of what the call should look like.

**Output path is currently hardcoded to `.claude/skills/`.** This is a known limitation. Plugin repos (like this one) use a different layout. Configurable output is a tracked todo item — do not work around it by editing the path in multiple places; fix it at the source.

**The blank skill template in SKILL.md is the canonical starting point for new skills.** The Key concepts placeholder reads: "Optional. Add entries for vocabulary, frameworks, assumptions, or construction guidance reused across sections. See Key concepts design for when and how." This wording was deliberate — it signals both the optional nature and the pointer to the design section for guidance.
