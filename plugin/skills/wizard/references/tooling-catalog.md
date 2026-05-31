# Tooling catalog

Concrete tools skills can leverage, organized by purpose. Add an entry when a tool has a clear trigger (when to use it) and is broadly applicable across multiple skills. If a tool is specific to one skill's domain, document it in that skill's `references/` file instead.

---

## Computational efficiency tools

Tools that replace in-context computation with cheaper, more persistent alternatives. Use these when context is doing work that a command, script, or external system could do for free.

### git
**Purpose:** Version control — precise snapshots, queryable history, exact diffs.
**Use when:** A skill needs to track state changes, contributions, or history over time.
**Replaces:** Growing markdown logs, accumulated in-context diffs, manually maintained changelogs.

```bash
git add <file> && git commit -m "<message>"
git log --oneline -- <file>
git diff HEAD~1 -- <file>
```

### Grep and Glob
**Purpose:** File content search (Grep) and path pattern matching (Glob) — built into Claude Code as dedicated tools.
**Use when:** A skill needs to locate files by pattern or find content within files.
**Replaces:** Reading files into context to scan them manually; `find` or `ls` piped through logic.

### rtk
**Purpose:** CLI proxy that reduces token consumption on common commands by 60–90% via smart filtering, grouping, truncation, and deduplication.
**Use when:** A skill runs commands whose raw output is verbose — `git status`, `cargo test`, `pytest`, `docker ps`, `jest`.
**Replaces:** Raw verbose command output that floods context.

```bash
rtk init -g          # Install shell hook once (auto-rewrites subsequent commands)
rtk git status       # Or invoke explicitly per command
rtk cargo test --ultra-compact
```

### jq / yq
**Purpose:** Command-line processors for JSON (jq) and YAML (yq).
**Use when:** A skill needs to extract, filter, or transform structured data from files or command output.
**Replaces:** Reading full JSON/YAML files into context to retrieve a few fields.

```bash
jq '.dependencies | keys' package.json
yq '.services.*.image' docker-compose.yml
jq -c '.' data.json        # Compact: removes all whitespace
```

### Data format selection
**Purpose:** Choosing the most token-efficient format for structured data that must pass through context.
**Use when:** A skill generates or receives tabular or structured data.

Prefer the most compact format that preserves necessary structure:
- **Compacted JSON** (`jq -c`) — nested structures, API responses; benchmarks show ~32% token reduction vs pretty-printed JSON, but 11–16% less efficient than TOON on uniform arrays
- **CSV** — flat tabular data; smallest footprint for purely uniform rows
- **TOON** — uniform arrays of objects with consistent fields; 33–42% smaller than compact JSON, human-readable, and structurally aware (field headers + length declarations); best for LLM-to-LLM data passing; efficiency advantage over compact JSON degrades quickly as data becomes more nested and less tabular — prefer compact JSON for deeply nested or semi-uniform structures
- **TOML** — human-readable config where the user will edit it directly
- Avoid pretty-printed JSON in context unless the user needs to read it directly

---

## UX and presentation tools

Tools that replace text output with richer interaction surfaces. Use these when the user's goal is inherently visual, interactive, or iterative — and text is a structural limitation, not just a style choice.

### Diagram and flowchart servers
**Purpose:** Render and interactively edit diagrams from structured definitions (Mermaid, PlantUML, DOT).
**Use when:** A skill's output is a process flow, architecture diagram, state machine, or any structure that is spatial by nature. Text descriptions of these are approximations.
**Integration:** MCP server. The skill generates the diagram definition; the server renders it and accepts edits.

### Prototype and UI preview servers
**Purpose:** Render UI mockups or interactive prototypes from component definitions or structured specs.
**Use when:** A skill designs interfaces or user flows. A rendered prototype communicates affordances and layout that a text spec cannot.
**Integration:** MCP server or dedicated tool. The skill outputs the spec; the server renders it.

### Digital sketchboards
**Purpose:** Visual surfaces for freeform spatial layouts, rough ideation, and graphical elements.
**Use when:** A task requires spatial reasoning or visual iteration — wireframing, concept sketching, diagram brainstorming before a formal definition exists.
**Integration:** MCP server or external tool with a shared canvas.

*See [tooling-catalog-examples.md](../examples/tooling-catalog-examples.md) for skill text examples of each entry.*
