# Tooling catalog — examples

Skill text fragments for the tools in [tooling-catalog.md](../references/tooling-catalog.md).

---

## git

**Anti-pattern (Task section):**
> After each expert reviews the document, append their findings and timestamp to `REVIEW_LOG.md`.

**Pattern:**
> After each expert completes their pass, commit the reviewed file:
> ```bash
> git add <reviewed-file>
> git commit -m "<domain> review: <filename>"
> ```
> The full review history is available with `git log --oneline -- <filename>`.

---

## Grep and Glob

**Anti-pattern (Task section):**
> Read each file in `docs/policies/` and check whether it contains a `last-reviewed` field.

**Pattern:**
> Find all policy files missing a `last-reviewed` field:
> Use Grep with pattern `last-reviewed` across `docs/policies/**/*.md` — files with no match need updating.

---

## rtk

**Anti-pattern (Task section):**
> Run `cargo test` and analyze the output to identify failing tests.

**Pattern:**
> Run `rtk cargo test` to get a filtered summary of failing tests without the verbose build output. If rtk is not installed, run `rtk init -g` first to enable the shell hook.

---

## jq / yq

**Anti-pattern (Task section):**
> Read `package.json` and identify which dependencies are present.

**Pattern:**
> Extract the dependency list without loading the full file into context:
> ```bash
> jq '.dependencies, .devDependencies | keys' package.json
> ```

---

## Data format selection

**Anti-pattern (Task section):**
> Output the analysis results as a formatted JSON report.

**Pattern:**
> Output results as CSV if the data is tabular (one row per finding, headers on first line). Use compacted JSON (`jq -c`) for nested structures. Only use pretty-printed JSON if the user will read it directly rather than passing it to another step.

---

## Diagram server (UX)

**Anti-pattern (Task section):**
> Describe the authentication flow as a numbered list of steps with arrows indicating direction.

**Pattern:**
> Generate a Mermaid diagram definition and pass it to the diagram MCP server for rendering. The user edits nodes and connections directly in the rendered view.
> ```
> sequenceDiagram
>     User->>Auth: login(credentials)
>     Auth->>DB: validate
>     DB-->>Auth: result
>     Auth-->>User: token
> ```

---

## Prototype server (UX)

**Anti-pattern (Task section):**
> Describe the dashboard layout: a sidebar on the left with navigation items, a header with the user menu, and a main content area with a data table.

**Pattern:**
> Generate a component tree definition and pass it to the prototype MCP server. The rendered prototype shows the actual layout and allows repositioning — the user iterates on the prototype, not the description.
