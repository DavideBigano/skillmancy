# Token efficiency patterns — examples

Skill text fragments illustrating each pattern from the Resources section.

---

## Prefer tools over in-context operations

**Anti-pattern (Task section):**
> Read `docs/policies/access-control.md`, copy its contents to `docs/archive/access-control.md`, then delete the original file.

**Pattern:**
> Move the file to the archive:
> ```bash
> mv docs/policies/access-control.md docs/archive/access-control.md
> ```

---

## Use git for stateful tracking

**Anti-pattern (Task section):**
> After each reviewer completes their pass, append their findings to `REVIEW_LOG.md` under a dated section header.

**Pattern:**
> After each reviewer completes their pass, commit the reviewed file:
> ```bash
> git add <reviewed-file>
> git commit -m "<domain> review: <filename>"
> ```
> Query the full review history with `git log --oneline -- <filename>`.

---

## Extract repetitive operations to scripts

**Anti-pattern (Task section):**
> To create a new policy document:
> 1. Read the template at `.templates/policy.md`
> 2. Replace `{{title}}` with the policy title, `{{date}}` with today's date, `{{owner}}` with the responsible team
> 3. Write the result to `docs/policies/<slug>.md`

**Pattern:**
> To create a new policy document, run:
> ```bash
> python scripts/scaffold.py --title "<title>" --owner "<team>"
> ```
> The script writes to `docs/policies/<slug>.md` and prints the path on success.

---

## Delegate to MCP servers or agents

**Anti-pattern (rule):**
> **Cover all dimensions.** For each design decision, assess security implications, map to compliance requirements, and identify legal constraints before proceeding.

**Pattern:**
> **Delegate specialized domains.** Security review and compliance mapping draw on different expertise — running both in a single pass dilutes both. Spawn a `cybersecurity-expert` agent for security assessment and a `compliance-expert` for regulatory mapping. Synthesize their outputs; do not blend their perspectives in-context.
