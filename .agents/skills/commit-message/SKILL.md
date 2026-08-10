---
name: commit-message
description: Use when drafting a git commit message — a plain "commit this", a request for a "conventional commit", or when the user names a style ("normal", "verbose") or a type (feat/fix/docs/etc). Reads the actual staged (or unstaged, if nothing's staged) diff to write the description and body — never invents generic text. Asks about style, type, or breaking-change status only when the diff and the user's wording genuinely don't settle it; proceeds straight to drafting otherwise.
---

# Commit messages

Two formats:

## Normal

One line: `<type>[(scope)]: <description>`, lowercase description, no body, no footer.

## Verbose (Conventional Commits)

```
<type>[(scope)][!]: <description>

<body>

<footer(s)>
```

- One blank line between header/body and body/footer.
- Body: free-form, one or more paragraphs, explains what changed and why.
- Footers: one per line, `Token: value` or `Token #value`. Tokens use `-` for spaces (`Reviewed-by`, `Co-authored-by`), except `BREAKING CHANGE`, which stays verbatim and uppercase.
- Breaking change: signal it with `!` before the `:` in the header, a `BREAKING CHANGE:` footer, or both — at least one is required when the change breaks something.

## Types

| Type | Use for |
| --- | --- |
| feat | new feature |
| fix | bug fix |
| docs | docs only |
| style | formatting, no logic change |
| refactor | restructuring, no feature/fix |
| perf | performance improvement |
| test | add/update tests |
| build | build system/dependencies |
| ci | CI/config changes |
| chore | maintenance/misc |
| revert | reverts a prior commit |

## Workflow

1. **Analyze the diff.**
   ```
   git diff --staged      # if files are staged
   git diff                # if nothing's staged
   git status --porcelain
   ```
   The description and body describe what really changed, not a paraphrase of the request.

2. **Stage files, if needed.**
   ```
   git add path/to/file1 path/to/file2
   git add src/components/*
   git add -p              # interactive, for partial/grouped staging
   ```
   Never stage or commit secrets: `.env`, `credentials.json`, private keys, and similar.

3. **Derive type, scope, and description** from the diff (see below for when to ask instead of guessing). Description: present tense, imperative mood ("add", not "added" or "adds"), under 72 characters.

4. **Execute the commit.**
   ```
   git commit -m "<type>[scope]: <description>"
   ```
   or, with a body/footer:
   ```
   git commit -m "$(cat <<'EOF'
   <type>[scope]: <description>

   <optional body>

   <optional footer>
   EOF
   )"
   ```

## When to ask vs. proceed

- **Style** — ask if neither the user's wording nor the repo's recent `git log` style settles normal vs. verbose.
- **Type/scope** — usually obvious from the diff (new capability → `feat`, only test files → `test`, only formatting → `style`). Ask only when the diff is genuinely mixed (e.g. a fix bundled with an unrelated feature).
- **Breaking change** — ask if the diff removes or renames a public export, changes a signature, or otherwise looks breaking and the user hasn't said either way.

Skip the questions once the user has already specified enough (e.g. "verbose, type feat", "just a normal one-liner") — go straight to drafting.

## Best practices

- One logical change per commit.
- Present tense, imperative mood: "fix bug", not "fixed bug" or "fixes bug".
- Reference issues in the footer: `Closes #123`, `Refs #456`.
- Keep the header under 72 characters.

## Message content rules

- Never mention the agent, assistant, or AI tooling by name, and never add a co-author/generated-by trailer for it.
- Never write in a way that reads as AI-generated: no filler, no inflated language, no "this commit ensures/enables" phrasing.
- Never use em dashes. Use a comma, a period, or a parenthetical instead.

## Git safety

- Never modify git config.
- Never run destructive commands (`--force`, hard reset) unless the user explicitly asks.
- Never skip hooks (`--no-verify`) unless the user explicitly asks.
- Never force-push to `main`/`master`.
- If a commit fails because of a hook, fix the issue and create a new commit. Don't amend.
