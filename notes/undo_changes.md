# Undoing Changes in Git

This guide explains how to undo mistakes in Git while understanding what happens to your changes and commit history.

**Important:** Before running a command that discards changes or rewrites history, check the repository status and make sure you do not need the affected work.

## 1. Understand the Three Main States

Git changes can exist in three main places:

- **Working directory:** Changes you have made to files but have not staged.
- **Staging area:** Changes prepared for the next commit using `git add`.
- **Repository history:** Changes already recorded in commits.

Different commands undo changes in different states.

## 2. Unstage Changes

If you staged changes with `git add` but do not want them included in the next commit, you can unstage them without losing the edits.

### Unstage a specific file

```bash
git restore --staged path/to/file
```

### Unstage all staged changes

```bash
git restore --staged .
```

The changes remain in your working directory. They are simply removed from the staging area.

## 3. Discard Uncommitted Changes

Use these commands carefully: they can permanently discard work.

### Discard changes to a tracked file

```bash
git restore path/to/file
```

Restores the file in the working directory to its staged version, or to the last committed version if no staged changes exist. Unstaged edits to that file are discarded.

### Discard all unstaged changes to tracked files

```bash
git restore .
```

Restores tracked files under the current directory to their staged versions, discarding their unstaged changes.

**Important:** These commands do not remove staged changes, and they do not delete untracked files.

### Remove an untracked file

```bash
git clean -n
```

Previews which untracked files Git would remove.

```bash
git clean -f
```

Deletes untracked files.

To preview and remove untracked directories as well:

```bash
git clean -nd
git clean -fd
```

**Warning:** `git clean` can permanently delete untracked work. Inspect the preview before running the deletion command.

## 4. Undo the Last Commit

The correct command depends on whether you want to keep the changes and whether the commit has already been pushed.

### Keep the changes staged

```bash
git reset --soft HEAD~1
```

Moves the current branch back one commit while keeping the changes from that commit staged.

### Keep the changes unstaged

```bash
git reset --mixed HEAD~1
```

Moves the current branch back one commit and leaves the changes in the working directory, unstaged.

`--mixed` is the default mode of `git reset`.

### Discard the commit and its changes

```bash
git reset --hard HEAD~1
```

Moves the current branch back one commit and resets the working directory and staging area to match it.

**Warning:** This can permanently discard uncommitted changes and the changes introduced by the removed commit. Do not use it unless you are certain you no longer need that work.

These examples undo the latest commit on the current branch. `HEAD~1` refers to its first parent, which is the previous commit in a normal, linear history.

## 5. Amend the Last Commit

If the latest commit has a mistake, you may be able to correct it instead of creating another commit.

### Change the commit message

```bash
git commit --amend -m "docs: correct commit message"
```

### Include forgotten changes

```bash
git add path/to/file
git commit --amend --no-edit
```

`--amend` creates a replacement for the latest commit rather than adding an ordinary new commit. The replacement has a different commit ID.

**Important:** Amend is generally straightforward before pushing. If the original commit has already been pushed, amending it rewrites history and requires extra care.

## 6. Undo a Commit That Has Already Been Pushed

If a commit is already on GitHub, the safest general approach is to use `git revert`.

### Revert a specific commit

```bash
git revert COMMIT_HASH
```

Creates a new commit that reverses the changes introduced by the specified commit.

Then push the new commit:

```bash
git push
```

Find the commit hash with:

```bash
git log --oneline
```

For example:

```bash
git revert a1b2c3d
```

Replace `a1b2c3d` with the actual commit hash.

**Why use `revert`?** It preserves the existing history and adds a new commit, making it suitable for changes already shared with others.

### What if you already pushed the wrong commit?

If you need to undo its effects, `git revert` is usually preferable to resetting a shared branch. Rewriting published history with `git reset` and a force push can disrupt other contributors.

## 7. Recover a Lost Commit with Reflog

If you accidentally moved a branch pointer with `git reset`, a previous commit may still be recoverable through the reflog.

### Inspect recent reference movements

```bash
git reflog
```

The reflog records recent changes to local references, including previous positions of `HEAD`.

### Return to a previous commit

First, identify the appropriate commit hash in the reflog. If you want to restore the branch to that commit while keeping subsequent changes staged:

```bash
git reset --soft COMMIT_HASH
```

Replace `COMMIT_HASH` with the actual hash.

**Important:** The reflog is local and is not a substitute for a backup. Entries expire according to Git's reflog retention settings, and unreachable commits may eventually be pruned.

## 8. Quick Reference

| Situation | Command | Result |
|---|---|---|
| Unstage a file | `git restore --staged file` | Keeps changes in the working directory |
| Discard unstaged changes to a file | `git restore file` | Discards unstaged edits to that file |
| Preview untracked files for deletion | `git clean -n` | Shows what would be deleted |
| Delete untracked files | `git clean -f` | Permanently removes untracked files |
| Undo the last commit, keep changes staged | `git reset --soft HEAD~1` | Keeps changes staged |
| Undo the last commit, keep changes unstaged | `git reset --mixed HEAD~1` | Keeps changes in the working directory |
| Undo the last commit and discard its changes | `git reset --hard HEAD~1` | Discards affected changes |
| Amend the last commit | `git commit --amend` | Replaces the latest commit |
| Undo a published commit safely | `git revert COMMIT_HASH` | Creates a new reversing commit |
| Inspect recent reference movements | `git reflog` | Shows recent local reference history |

## Further Reading

- [Regular Workflow](./regular_workflow.md)
- [Git Command Reference](./git_reference.md)
- [Branches and Merging](./branches_and_merging.md)
- [Conventional Commits](./conventional_commits.md)
