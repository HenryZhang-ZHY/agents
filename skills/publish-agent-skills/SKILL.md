---
name: publish-agent-skills
description: "Validate and publish Agent Skills from a GitHub repository using gh skill publish. Use only when a human explicitly invokes $publish-agent-skills and asks to publish one or more skills."
---

# Publish Agent Skills

Publish repository-hosted Agent Skills through the GitHub CLI's preview `gh skill publish` workflow.

## Authorization boundary

- Treat explicit skill invocation as workflow selection, not by itself as permission to mutate GitHub.
- Publish only when the human explicitly asks to publish Agent Skills and provides or approves the version tag.
- Resolve ambiguity about the repository, skill directory, included skills, or version before publishing.
- Never delete or replace an existing release, move a tag, or republish an existing version unless the human separately requests that exact action.
- Remember that `gh skill` is in preview. Read `gh skill publish --help` at execution time and stop if its current behavior conflicts with this workflow.

## Inputs

Establish these values before any publishing command:

- Repository or directory: default to the current repository root; pass a directory argument only when the human intends a narrower supported location.
- Skills: enumerate every `SKILL.md` that `gh skill publish` will discover and state which skills will be included.
- Tag: require a human-provided or human-approved SemVer-style tag such as `v1.2.0`.

## Workflow

### 1. Inspect the repository

1. Run `gh auth status`, `gh --version`, and `gh skill publish --help`.
2. Identify the repository with `gh repo view` and inspect `git status --short --branch`, `HEAD`, remotes, and upstream state.
3. Require a clean worktree and confirm `HEAD` is pushed to the intended remote branch.
4. Discover skills using the locations supported by the current command, including `skills/*/SKILL.md`, `skills/{scope}/*/SKILL.md`, root-level `*/SKILL.md`, and `plugins/{scope}/skills/*/SKILL.md`.
5. Check remote tags and releases. Stop if the approved tag or its release already exists.

### 2. Validate without publishing

Run the official dry run against the intended directory:

```bash
gh skill publish "$skill_directory" --dry-run
```

- Omit the directory argument when publishing from the current repository root.
- Require the dry run to pass before publishing. It validates skill naming, directory/name agreement, required frontmatter, and supported `allowed-tools` shape.
- If validation reports install metadata that can be stripped, use `--fix` only after checking the affected paths. Review every resulting diff, commit the correction, push it, and rerun `--dry-run`.
- Fix other validation errors directly, validate the affected skills, commit and push the corrections, then rerun the dry run.
- Never continue to publishing with validation errors or uncommitted fixes.

### 3. Publish the approved version once

Use the approved tag for deterministic, non-interactive publishing:

```bash
gh skill publish "$skill_directory" --tag "$release_tag"
```

- Omit the directory argument when publishing from the current repository root.
- Expect the command to validate again, add the `agent-skills` repository topic, and create a GitHub Release with generated notes.
- Run the command once. If it fails or the result is ambiguous, inspect remote tags, releases, and repository topics before considering a retry.

### 4. Verify and report

1. Read the created release with `gh release view <tag>` and verify the remote tag points to the pushed commit.
2. Confirm the repository has the `agent-skills` topic.
3. Use `gh skill preview <owner/repo> <skill-name>` to confirm each published skill is discoverable when the command supports it.
4. Return the release URL, version, target commit, and published skill names.

## Stop conditions

Stop without publishing when authentication or write access is missing, the worktree is dirty, the target is not pushed, the requested tag/release already exists, the dry run fails, fixes remain uncommitted, or the current preview command's behavior cannot be verified. Report the blocker and preserve existing remote state.
