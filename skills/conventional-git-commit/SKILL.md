---
name: conventional-git-commit
description: Create git commits and draft, review, rewrite, or choose commit messages that follow Conventional Commits 1.0.0-beta.4. Use this skill whenever the user asks to commit changes, says "commit this", wants a commit message, asks whether a change is feat/fix/chore/refactor/etc., mentions breaking changes, changelogs, semantic versioning, release notes, squash commits, or wants staged changes summarized for git history. For exact specification wording and edge cases, consult references/conventional-commits-1.0.0-beta.4.md.
---

# Conventional Git Commit

Use this skill to make commit history explicit and machine-readable. The message should communicate the intent of the change, support changelog generation, and map naturally to semantic versioning when `feat`, `fix`, or `BREAKING CHANGE` is used.

For exact wording, examples, and edge cases from the source specification, read [references/conventional-commits-1.0.0-beta.4.md](references/conventional-commits-1.0.0-beta.4.md). Use the reference when the user asks about compliance details, SemVer implications, breaking changes, or ambiguous commit types.

## Commit message format

```text
<type>[optional scope][optional !]: <description>

[optional body]

[optional footer]
```

## Type selection

Choose the most specific type that describes the primary intent of the commit:

| Change | Type |
| --- | --- |
| Adds a new capability | `feat` |
| Patches a bug | `fix` |
| Improves an existing implementation without adding a feature or fixing a bug | `improvement` |
| Improves performance | `perf` |
| Refactors code without changing behavior | `refactor` |
| Adds or changes tests only | `test` |
| Changes documentation only | `docs` |
| Changes formatting only | `style` |
| Changes dependencies, packaging, or build configuration | `build` |
| Changes CI workflows | `ci` |
| Performs maintenance that does not fit another type | `chore` |

## Process

1. Inspect the changes being committed, preferably from the staged diff when available.
2. Identify the primary intent. If the commit mixes unrelated intents, suggest splitting it before writing the final message.
3. Choose the commit type from the table.
4. Add a scope only when it gives useful context, such as `parser`, `auth`, `docs`, or `deps`.
5. Write a concise imperative description after `: `. The description should complete the phrase "This commit will..."
6. Add a body only when the reason, tradeoff, migration note, or behavioral detail would help future readers.
7. Add footers for issue links, breaking changes, pull requests, reviewers, or required trailers.
8. Verify the final message matches the format before running `git commit`.

## Breaking changes

Use `BREAKING CHANGE: <description>` when the commit introduces a breaking API or user-facing compatibility change.

- Put `BREAKING CHANGE:` at the beginning of the body or at the beginning of a footer line.
- Keep `BREAKING CHANGE` uppercase exactly.
- You may add `!` before the colon in the subject, such as `chore!: drop Node 6`, but the message still needs a `BREAKING CHANGE:` body or footer.

## Footer and trailer handling

- Keep each footer as one piece of metadata per line.
- Preserve required trailers such as `Co-authored-by`.
- If there is both a body and footers, separate them with one blank line.
- If there is no body, place footers one blank line after the subject.

## Examples

**Feature with breaking change:**

```text
feat: allow provided config object to extend other configs

BREAKING CHANGE: `extends` key in config file is now used for extending other config files
```

**Breaking maintenance change with `!`:**

```text
chore!: drop Node 6 from testing matrix

BREAKING CHANGE: dropping Node 6 which hits end of life in April
```

**Documentation-only change:**

```text
docs: correct spelling of CHANGELOG
```

**Scoped feature:**

```text
feat(lang): add polish language
```

**Fix with issue footer:**

```text
fix: correct minor typos in code

See the issue for details on the typos fixed.

Closes #12
```
