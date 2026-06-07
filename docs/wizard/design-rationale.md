# Wizard — Design rationale

Non-obvious decisions and why they were made. Read this before editing the skill to avoid undoing intentional choices.

---

**Cross-section reinforcement is intentional, not duplication.** Persona, rules, and Resources can address the same concept at different abstraction levels. Test: does each representation do something the others don't? If no, cut the weaker one.

**Guidelines are behavioral directions, not interaction directives.** Guidelines cover framing, priorities, and tradeoffs the model would get wrong without explicit direction — not interaction style. When writing or reviewing guidelines, ask "what behavior does this steer?" not "how does this change the tone?"

**Axis update behavior defined once in Scoping, not repeated per phase.** The axis can be updated at any phase boundary, but the instruction for how to do it lives in Scoping only. The older pattern of embedding the update block in each phase caused redundancy and drift between instances.

**Flowchart is optional in CREATE.** For simpler skills, the flowchart step is overhead. Wizard offers it rather than mandating it — the optionality is deliberate.

**Bold-title paragraph structure (`**Title** — prose`) was deliberately not codified in Resources.** Used consistently throughout Resources but not added as a formal entry — it's a formatting convention, out of scope for a section that covers vocabulary and frameworks.

**The "show, don't describe" rule covers tool invocations and code, not just output formats.** The rule was extended beyond output format conventions to include tool calls (`Glob(.claude/skills/<name>/**)`) and code snippets. When writing new instructions, give the exact call or concrete snippet — not a prose description of what the call should look like.

**Output path is currently hardcoded to `.claude/skills/`.** Known limitation — plugin repos use a different layout. Tracked in todo; do not work around by editing the path in multiple places.

**The blank skill template in SKILL.md is the canonical starting point for new skills.** The Resources section uses a structural template (`### Resource` headings with `**[Label]** — ...` placeholders) rather than prose instructions — consistent with the "show, don't describe" rule.
