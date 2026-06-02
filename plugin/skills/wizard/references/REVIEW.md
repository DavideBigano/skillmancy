# Skill review

## Pre-flight

Use Glob to check whether `.claude/skills/<name>/` exists.

If it does not, respond:

> No skill named `<name>` found at `.claude/skills/<name>/`. Use `/skillmancy:wizard create <name>` to create it.

Do not continue.

If it exists, read the full skill: SKILL.md and all files in `references/`, `examples/`, and `scripts/`. Every file must be read before the review begins — the review covers the full skill, not just SKILL.md.

---

## Scoping

Before beginning the review, use the `AskUserQuestion` tool to ask:

> What's your goal for this review?
> 1. **Pre-ship** — identify any blockers before the skill is considered done
> 2. **Diagnosing** — something feels off; focus the review on a specific area
> 3. **Health check** — routine balanced review; findings and suggestions weighted equally
> 4. **Improvement** — the skill works; lead the report with suggestions, treat findings as secondary unless they are hard violations

Use the answer to tune emphasis throughout the review and report.

If the user asks for more than one, execute and report each separately.

---

## Review

**Check 1 — Rule checks.** Apply each rule as a pass/fail check. Flag violations as findings.

**Check 2 — Lens review.** Apply each Persona authority's lens to the full skill. Resources is not a separate checklist — it's the shared vocabulary and frameworks the lenses draw from.

Follow the section for the chosen goal.

---

### Pre-ship

1. Run Check 1 in full — every violation is a blocker; the skill should not ship with rule violations
2. Run Check 2 focusing on gaps (findings) rather than opportunities (suggestions). Note suggestions briefly but do not treat them as blockers
3. When finished, jump to [Report](#report).

---

### Diagnosing

1. Ask one follow-up: "Which area or behavior seems off?"
2. Run Check 1 and Check 2 on the identified area — surface findings there in detail
3. Run a lighter pass of Check 1 and Check 2 on remaining areas — flag clear violations but do not deep-dive sections unrelated to the reported symptom
4. When finished, jump to [Report](#report).

---

### Health check

1. Run Check 1 in full
2. Run Check 2 in full
3. Weight findings and suggestions equally — no emphasis adjustment
4. When finished, jump to [Report](#report).

---

### Improvement

1. Run Check 1 — note hard violations but do not let them lead
2. Run Check 2 leaning toward opportunities: what does each lens see that the current design doesn't fully exploit?
3. Report leads with Suggestions; Findings appear after
4. When finished, jump to [Report](#report).

---

## Report

After completing the review, use the `AskUserQuestion` to ask the user:

> For the report/s you requested, what type do you want to generate?
> 1. One-line
> 2. Extended

If the user requested multiple reports, the answer applies to all unless they specify otherwise.

Then produce this report according to the answer:

```
## Review: <skill-name>

**Axis:** [assessed position, e.g., "65% conversational / 35% operational"]

### Findings

**[Finding N]**: 
**File/s**: [Found at which file/s]
**Issue**: [What the issue is and why it matters. One-line if requested.]
**Recommendation**: [Recommendation. One-line if requested.]

[Repeat per finding]

### Suggestions

**[Suggestion N]**: 
**File/s**: [Pertinent to which file/s]
**Opportunity**: [Where the skill's own groundwork points to unexploited potential. One-line if requested.]
**Grounded in**: [Specific authority, rule, or resource entry that motivates this. One-line if requested.]

[Only include suggestions that can be pinned to something in the skill's own persona, rules, or resources. If a suggestion cannot be grounded this way, omit it.]

### Summary
[N] finding(s), [M] suggestion(s). [What is sound, what needs fixing, and where the biggest growth opportunity lies. Always one-line]
```

If there are no findings, say so. If there are no suggestions, omit that section.

---

## Handoff

After presenting the report, if there are findings, say:

> To address these, run `/skillmancy:wizard edit <name>` — the findings above are the edit scope.
