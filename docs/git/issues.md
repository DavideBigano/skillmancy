# GitHub Issues

Issues serve as the project backlog. Capture any out-of-scope work as an issue rather than letting it get lost.

- [Creating an issue](#creating-an-issue)
- [Listing open issues](#listing-open-issues)
- [Referencing issues](#referencing-issues)

## Creating an issue

```
gh issue create --title "[Type] Declarative issue name" --body "<body>"
```

Types follow the same convention as branches:
- `Enhancement`
- `Refactor`
- `Maintenance`
- `Bugfix`
- `Cleanup`

The body should briefly explain what needs doing and why. Enough context for someone picking it up cold.

## Listing open issues

```
gh issue list
```

## Referencing issues

Link an issue in a PR body or commit message with `#<issue-number>`. Use `Closes #<issue-number>` in a PR body to auto-close the issue when the PR merges.
