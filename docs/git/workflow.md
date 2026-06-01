# Git Workflow

Branching conventions, commit discipline, and PR process for this project.

- [Branching](#branching)
- [Committing](#committing)
- [Pushing](#pushing)
- [Pull Requests](#pull-requests)
- [After merge](#after-merge)
- [Pulling main into a feature branch](#pulling-main-into-a-feature-branch)

## Branching

Always branch off `main`.

Branch naming convention:
```
<type>/declarative-branch-name
```

Valid types:
- `enhancement` — new functionality
- `refactor` — restructuring existing code without behaviour change
- `maintenance` — dependency updates, config, tooling
- `bugfix` — fixing a defect
- `cleanup` — removing dead code, improving readability

## Committing

Follow **Commit Early, Commit Often (CECO)**: commit every time a self-contained sub-component is complete — small enough to be reviewable on its own.

**One-line commits** — short, declarative, single-line. Makes PR history readable.

## Pushing

- **First push**: set the upstream with the same name as the local branch:
  ```
  git push --set-upstream origin <branch-name>
  ```
- **Subsequent pushes**: assume the remote branch already exists:
  ```
  git push
  ```

Push at the end of each working session and whenever the branch is ready for review.

## Pull Requests

Create a PR when the branch is review-ready or when prompted by the user:
```
gh pr create --title "<PR title>" --body "<PR body>"
```

**Title format** — mirrors the branch naming convention:
```
[Type] Declarative branch name
```
Example: `[Enhancement] Add user authentication flow`

The title may differ from the branch name if the scope changed after the branch was created.

**Body** — must follow `.github/PULL_REQUEST_TEMPLATE.md`.

## After merge

When the user reports a PR as merged, verify before acting:
```
gh pr view <pr-number> --json state -q .state
```

If confirmed merged, clean up:
```
git checkout main
git branch -d <branch-name>
git pull --prune
```

## Pulling main into a feature branch

To bring the latest main changes into the current feature branch:
```
git pull origin main
```
