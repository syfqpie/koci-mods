# AGENTS.md

This file provides guidance to coding agents working in this repository.

## Overview

A collection of mods for Ragnarok Offline, kept "for fun". There is no build system, package manager, linter, or test suite. Each mod is a directory of configuration files.

## Structure

- `mods/<mod_name>/mod.json` is the mod manifest. It contains:
  - `name`, `version`, `author`, and `description`
  - `default`: `"off"` means the mod is disabled until the user enables it
  - `requires`: compatibility requirements, including the `app` semver range and `era`
  - `settings`: mod-specific settings
- Other files under `mods/<mod_name>/` mirror the game's data layout. For example, `conf/groups.yml` is a rAthena-style `PLAYER_GROUP_DB` that enables `@atcommands` by listing them under `Commands:` for group `Id: 0`.
- Settings schema and modding reference: https://github.com/Flux159/ragnarokoffline.app/blob/main/docs/MODDING.md. Settings are a flat list of `{key, type, default, label, description}` with `type` of `boolean`, `number` or `string`. There is no category/grouping support and a mod may declare at most 40 settings.
- `koci-atcommands` is the mod that holds the at-commands. Each at-command is a boolean setting whose `key` is the rAthena command name; `conf/when/<key>/groups.yml` is merged in only while that setting is on. To add an at-command, add a setting plus that file (titles/descriptions come from rAthena's `conf/atcommands.yml`). Categories are shown as a `Category:` prefix in `label`.

## Development Guidelines

- Keep changes small and focused on the requested task.
- Preserve the existing directory structure, file formats, and conventions.
- Do not introduce a build system, package manager, linter, test framework, or dependencies unless explicitly requested.
- Do not refactor unrelated files or introduce abstractions unnecessarily.
- Keep mods disabled by default unless explicitly requested otherwise.
- When adding or modifying at-commands, verify the command names and configuration format against the relevant rAthena configuration.
- Do not assume a mod is compatible with every Ragnarok Offline or rAthena version. Update compatibility requirements when needed.
- Do not commit changes unless explicitly requested.

## Release Flow

`.github/workflows/release.yml` runs when a GitHub Release is published. It zips each `mods/*/` directory to `dist/<mod_name>.zip`, with the mod folder itself at the ZIP root, and uploads the ZIP files to that release.

Any new directory under `mods/` is picked up automatically.

When changing a mod:

- Bump `version` in its `mod.json`.

## Validation

There is no automated test suite or build process.

Before finishing a change:

- Review the modified files for correctness.
- Verify that `mod.json` remains valid JSON.
- Check YAML syntax and indentation for modified YAML files.
- Confirm that the ZIP structure expected by the release workflow is preserved when changing packaging-related files.
- Summarize the changes and any validation that could not be performed.

## Git Operations

Agents MUST perform **read-only Git operations only**.

### Allowed operations
- Inspect repository status: `git status`
- View diffs: `git diff`, `git diff --cached`
- Inspect commit history: `git log`
- Inspect commits and changes: `git show`
- Inspect branches and tags: `git branch`, `git tag`
- Inspect remotes and configuration: `git remote -v`, `git config --get`
- Inspect tracked and untracked files: `git ls-files`, `git status`
- Compare revisions: `git diff <revision> <revision>`
- Inspect blame and file history: `git blame`, `git log --follow`

### Prohibited operations
Agents MUST NOT execute Git commands that modify repository state, history, configuration, or remote repositories, including:

- **Committing:** `git commit`, `git commit --amend`
- **Staging or unstaging:** `git add`, `git reset`, `git restore --staged`
- **Discarding changes:** `git checkout -- <file>`, `git restore`, `git clean`
- **Branch or tag mutations:** `git branch -d`, `git branch -D`, `git branch -m`, `git tag -d`
- **History rewriting:** `git rebase`, `git cherry-pick`, `git revert`, `git filter-branch`
- **Remote operations:** `git push`, `git fetch`, `git pull`, `git remote add`, `git remote remove`
- **Stashing:** `git stash`, including `push`, `pop`, and `drop`
- **Configuration changes:** `git config` commands that write configuration
- **Repository initialization or maintenance:** `git init`, `git clone`, `git gc`, `git prune`, `git worktree add`, and other state-changing operations
- **Destructive or mutating Git options:** any command using flags such as `--force`, `--hard`, or `-D` when they modify Git state

### Rules
1. Never create commits, amend commits, stage changes, switch branches, create or delete branches, or modify Git history.
2. Never push to, pull from, fetch from, or otherwise modify remote repositories.
3. Never discard, overwrite, or clean up user changes, even if they appear unrelated to the current task.
4. Never modify Git configuration, hooks, refs, the index, or repository metadata.
5. Do not use alternative commands or scripts to bypass these restrictions.
6. If a task requires a prohibited Git operation, explain what is needed and ask the user to perform it manually.
7. When in doubt, treat the operation as prohibited.

These restrictions apply to Git commands executed directly, through shell scripts, IDE integrations, MCP tools, or other agents. Agents may still edit project files as required by the task, but MUST NOT use Git to stage, commit, discard, or otherwise manipulate those changes.

**Default:** Inspect freely; mutate nothing. The user retains full control over all Git operations.