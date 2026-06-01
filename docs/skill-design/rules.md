# Wizard — Rules

Explicit behavioral conditions the skill must satisfy — governing sequencing and output quality rather than conversation style.

- [What rules do](#what-rules-do)
- [Format](#format)
- [The fixed first rule](#the-fixed-first-rule)
- [Adding, changing, and removing rules](#adding-changing-and-removing-rules)
- [Axis relationship](#axis-relationship)

## What rules do

Rules are explicit conditions the skill must satisfy. Each rule exists because the model *would* behave differently without it — it makes a failure mode explicit rather than leaving it to the persona to catch implicitly.

Rules are not style guidance or tone instructions. Most govern sequencing and output quality, not conversation style. The right test for a rule: if you removed it, would the skill's behavior change in a concrete, observable way? If not, it's a preference, not a rule — cut it.

---

## Format

Each rule follows this structure:

```
**[Rule name].** [Body: rationale or condition embedded, concrete action or refusal — not a preference.]
```

The rule name is a short imperative phrase. The body must imply a concrete action or refusal, not a vague aspiration. "Be thorough" is not a rule. "Do not begin drafting until scope is clear; ask follow-up questions rather than assuming" is a rule.

---

## The fixed first rule

"Be direct, not diplomatic" is always the first rule, verbatim:

```
**Be direct, not diplomatic.** Your job is to produce the best possible outcome, not to protect the user's feelings. If a specification is vague, say so. If a proposed approach has a real problem, name it clearly and explain why. If the direction is wrong, push back — with a reason, not just a preference. That said, pushback is not a reflex: if a choice is well-reasoned and the tradeoffs are understood, say so and move forward. Contrarianism is as useless as sycophancy.
```

This rule requires no rationale when proposing the rule set. It is always present, always first, always verbatim.

---

## Adding, changing, and removing rules

**Adding** — state the rule and the specific behavior or risk it addresses, referenced from the scoping or task discussion. A rule without a grounded rationale is likely a preference in disguise.

**Changing** — state what the rule currently does, what gap or over-specification it creates, and what the replacement achieves differently.

**Removing** — state what the rule was preventing. If removing it leaves a real failure mode unguarded, either keep the rule or explain what else covers it.

---

## Axis relationship

Rules carry more weight in operational skills, where the persona is lighter and consistent output behavior depends more on explicit conditions. In conversational skills, the persona does more of this work implicitly. When the axis shifts, audit the rules: some may become redundant, and some gaps may need new rules to fill them.
