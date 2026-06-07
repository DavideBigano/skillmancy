# Skill review

## 0 — Pre-flight

Check skill existence with `glob <expected-skill-directory>`.

If it does not exist, respond:

> Skill `<name>` not found at `<expected-skill-directory>`. Use `/wizard create <name>` to create it.

Do not continue.

If it exists, read the full skill.

---

## 1 — Scoping

Before beginning the review, use the `AskUserQuestion` tool to ask:

> What's your goal for this review?
> 1. **Base review** — routine review for detecting issues and inconsistencies
> 2. **Diagnosing** — something feels off; focus the review on a specific issue
> 3. **Improvement** — reviewing the skill looking for gaps in implementation and possible improvements

Use the answer to tune emphasis throughout the review and report.

If the user asks for more than one, execute and report each separately.

---

## 2 — Review

**Check 1a — Authorities review** Check if each /wizard's authority is correctly applied to the full skill under review.

**Check 1b — Internal authority consistency** Check if each of the reviewed skill's authorities are applied consistently throughout the full skill under review.

**Check 2a — Guidelines review** Check if each /wizard's guideline is correctly applied to the full skill under review.

**Check 2b — Internal guideline consistency** Check if each of the reviewed skill's guidelines are applied consistently throughout the full skill under review.

**Check 3a — Resources review** Check if each /wizard's resource is correctly applied to the full skill under review.

**Check 3b — Internal resource consistency** Check if each of the reviewed skill's resources are applied consistently throughout the full skill under review.

Follow the section for the chosen goal.

---

### Base review

1. Run all checks in full — mark every violation as a finding and any gap as a suggestion
2. Use `glob <skill-directory>/**/*` to list all files. Check each for dead references and mark them as findings.
3. Jump to [3 — Report](#3--report).

---

### Diagnosing

1. Ask the user what is the problem they want to fix.
2. Run pertinent checks on suspicious areas.
3. Surface the results to the user, ranked by likeliness to be the cause of the reported problem, and ask for feedback on them.
4. Iterate over points 2, 3 and 4 until satisfied — mark every result as a finding
4. Jump to [3 — Report](#3--report).

---

### Improvement

1. Run all checks as a way to surface possible improvements, not to find errors; mark every improvement and gap found as a suggestion and ignore violations
2. Jump to [3 — Report](#3--report).

---

## 3 — Report

After completing the review, use the `AskUserQuestion` to ask the user:

> For the report/s you requested, what type do you want to generate?
> 1. One-line
> 2. Extended

If the user requested multiple reports, the answer applies to all unless they specify otherwise.

Then produce this report according to the answer:

```
## Review: <skill-name>

**Axis:** [XX% conversational / YY% operational]

### Findings

**Finding [N]**: 
**File/s**: [Found at which file/s]
**Issue**: [What the issue is and why it matters. One-line if requested.]
**Recommendation**: [Recommendation. One-line if requested.]

[Repeat per finding]

### Suggestions

**Suggestion [N]**: 
**File/s**: [Pertinent to which file/s]
**Opportunity**: [Where the skill's own groundwork points to unexploited potential. One-line if requested.]
**Grounded in**: [Specific authority, rule, or resource entry that motivates this. One-line if requested.]

[Only include suggestions that can be pinned to something in the skill's own persona, rules, or resources. If a suggestion cannot be grounded this way, omit it.]

### Summary
[N] finding(s), [M] suggestion(s). [What is sound, what needs fixing, and where the biggest growth opportunity lies. Always one-line]
```

If there are no findings, say so. If there are no suggestions, omit that section.

After presenting the report say:

> To address these, run `/wizard edit <name>` — the report above feeds into the edit scope.
