# Skillmancy — Agent Guidelines

## docs/ — Shared Knowledge Base

`docs/` is the shared memory store for this project, maintained collaboratively by agents and users.

### Structure

```
docs/
├── index.md          ← authoritative index of all docs (always update this when adding files)
├── domain-a/
│   ├── topic-1.md
│   └── topic-2.md
└── domain-b/
    └── topic-1.md
```

### index.md format

```markdown
# Index

- Domain A
    - [Topic 1](./domain-a/topic-1.md)
    - [Topic 2](./domain-a/topic-2.md)
- Domain B
    - [Topic 1](./domain-b/topic-1.md)
```

### Rules for agents

- **Consult first**: whenever a topic comes up — in conversation, when planning, or before writing — check `docs/index.md` to see if relevant knowledge exists and read the relevant files before responding or acting.
- **After writing**: always update `docs/index.md` to include the new file.
- **Naming**: domain folders and file names must be descriptive enough that the index alone tells you where to look without opening files. Use lowercase kebab-case.
- **Scope**: one coherent topic per file. Split when a file covers more than one distinct concept.
- **No orphans**: every `.md` file under `docs/` (except `index.md` itself) must have an entry in the index.
- **Every doc belongs to a domain**: all content files must live inside a domain subdirectory. Only `index.md` lives directly under `docs/`.
