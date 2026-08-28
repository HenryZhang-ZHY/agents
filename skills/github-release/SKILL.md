---
name: github-release
description: "Publish a GitHub Release from a verified Git commit and tag using the gh CLI. Use only when a human explicitly invokes $github-release and asks to create or publish a release."
---

# GitHub Release

Publish a GitHub Release with reviewed notes, an immutable target commit, and post-publish verification.

## Authorization boundary

- Treat explicit skill invocation as workflow selection, not by itself as permission to mutate GitHub.
- Create a release only when the human explicitly asks to publish or create it and provides or approves the tag.
- If the tag, target, repository, draft/prerelease status, or release-note intent is materially ambiguous, resolve it before publishing.
- Never delete or replace a release, move or force-push a tag, or publish over an existing tag/release unless the human separately requests that exact action.

## Inputs

Establish these values before publishing:

- Repository: default to the current Git repository.
- Tag: require a human-provided or human-approved value, such as `v1.2.0`.
- Target: default to the current `HEAD` only after verifying that exact commit is present on the intended remote branch.
- Release kind: stable and published by default; use draft or prerelease only when requested or clearly encoded by a prerelease version.
- Notes: default to GitHub-generated notes reviewed and, when useful, supplemented with concise highlights.
- Assets: upload only the files explicitly requested, after verifying their paths and contents.

## Workflow

### 1. Inspect without changing remote state

1. Run `gh auth status` and identify the repository with `gh repo view`.
2. Inspect `git status --short --branch`, the current branch, `HEAD`, remotes, and upstream tracking state.
3. Fetch the intended remote and its tags. Require a clean worktree and confirm the target commit is pushed.
4. Check existing tags and releases with `git ls-remote --tags` and `gh release view <tag>`.
5. Stop if the release already exists. If only the tag exists, continue only after verifying that it points to the approved target; stop on any mismatch.
6. Identify the previous release and inspect every commit from its tag through the target. Confirm there are new commits and that the requested version is plausible under SemVer when SemVer is in use.

### 2. Prepare and review release notes

Use GitHub's release-notes API to preview generated notes before publication when possible:

```bash
repo_name=$(gh repo view --json nameWithOwner --jq .nameWithOwner)
gh api --method POST "repos/$repo_name/releases/generate-notes" \
  -f tag_name="$release_tag" \
  -f target_commitish="$target_sha" \
  -f previous_tag_name="$previous_tag"
```

- Check that the notes cover the commits in the release range and do not claim unrelated changes.
- If generated notes contain only a comparison link or omit important direct commits, prepend a short `## Highlights` section with `--notes` while retaining `--generate-notes`.
- Use `--notes-start-tag <previous-tag>` so GitHub compares against the intended release.
- For a first release, omit the previous-tag fields and summarize the initial contents.

### 3. Publish once

For a new stable tag, use this shape and include only applicable options:

```bash
gh release create "$release_tag" \
  --target "$target_sha" \
  --title "$release_tag" \
  --generate-notes \
  --notes-start-tag "$previous_tag" \
  --fail-on-no-commits \
  --latest
```

- Add `--notes <text>` or `--notes-file <path>` for reviewed custom highlights.
- Add `--draft` only when the human asks for a draft.
- Add `--prerelease --latest=false` for a prerelease.
- If the intended tag already exists but no release exists, first verify that it targets the approved commit, then add `--verify-tag` instead of creating or moving the tag.
- Run the publish command once. If it fails or returns an ambiguous result, inspect GitHub before retrying.

### 4. Verify and report

1. Read the release back with `gh release view <tag> --json name,tagName,isDraft,isPrerelease,publishedAt,url,targetCommitish,body`.
2. Resolve the remote tag with `git ls-remote` and verify it points to the approved commit. Dereference annotated tags when necessary.
3. Confirm the expected Latest, draft, or prerelease status with `gh release list`.
4. Return the release URL, tag, target commit, publication status, and a concise summary of the notes and assets.

## Stop conditions

Stop without publishing when authentication or write access is missing, the worktree is dirty, the target is not pushed, the tag/release conflicts with existing remote state, there are unexpectedly no new commits, or release contents cannot be verified. Report the blocker and preserve all existing remote state.
