# Git Branches and Merging

Branches allow you to work on different features, fixes, or experiments independently without directly changing another branch.

Merging integrates changes from one branch into another.

## 1. Understanding Branches

A branch is a movable reference to a commit. When you create a commit on a branch, that branch reference advances to the new commit.

For example, a repository might have this structure:

```text
main
  |
  A---B---C
       \
        D---E  feature
```

In this example:

- `main` points to commit `C`, its latest commit.
- `feature` points to commit `E`, its latest commit.
- Commits `D` and `E` belong to the feature's history and are not yet part of `main`.

Branches are useful for developing features, fixing bugs, and testing changes independently.

## 2. Listing and Creating Branches

| Command | Description |
|---|---|
| `git branch` | List local branches. |
| `git branch -a` | List local and remote-tracking branches. |
| `git branch feature` | Create a branch named `feature`. |
| `git switch feature` | Switch to the `feature` branch. |
| `git switch -c feature` | Create a branch and switch to it. |
| `git branch -m new-name` | Rename the current branch. |
| `git branch -d feature` | Delete a local branch that Git considers safely merged. |
| `git branch -D feature` | Force-delete a local branch, even if it has unmerged changes. |

### Create and switch to a branch

```bash
git switch -c feature
```

This creates a new branch named `feature` from the current commit and switches to it.

**Note:** Creating a branch does not automatically switch to it. Use `git switch` to change branches.

## 3. Working on a Branch

Once you switch branches, you can edit files and commit changes as usual.

```bash
git switch -c feature
# Edit files

git status
git add .
git commit -m "feat: add new feature"
```

The commit is added to the branch you currently have checked out.

**Important:** Before switching branches, check `git status`. Git may prevent switching if changes would be overwritten. Some uncommitted changes can follow you between branches when they do not conflict, so switching branches does not automatically save or discard them.

## 4. Merging Branches

A merge integrates changes from one branch into the branch currently checked out.

Suppose you have finished working on `feature` and want to integrate it into `main`.

### Step 1: Switch to the destination branch

```bash
git switch main
```

The destination branch is the branch that will receive the changes.

### Step 2: Merge the feature branch

```bash
git merge feature
```

This integrates the changes from `feature` into `main`.

### Step 3: Push the updated branch

```bash
git push
```

If `main` tracks the appropriate remote branch, this pushes the merge result to the remote repository.

### Example workflow

```bash
git switch -c feature
# Make changes
git add .
git commit -m "feat: add new feature"

git switch main
git merge feature
git push
```

**Note:** This example assumes the local `main` branch is up to date and configured to track the intended remote branch. If the remote has new commits, integrate them as appropriate before pushing.

## 5. Types of Merge

### Fast-forward merge

A fast-forward merge is possible when the destination branch has not advanced since the source branch diverged from it.

Before:

```text
A---B  main
     \
      C---D  feature
```

After merging `feature` into `main`:

```text
A---B---C---D  main, feature
```

Git moves the destination branch forward. No new merge commit is necessary.

### Three-way merge

A three-way merge is needed when both branches have new commits since they diverged.

Before:

```text
      C---D  feature
     /
A---B
     \
      E---F  main
```

After merging `feature` into `main`:

```text
      C---D
     /     \
A---B       M  main
     \     /
      E---F
```

Here, `M` represents a merge commit that combines the histories of both branches.

The actual commit graph depends on the repository history and merge options.

## 6. Merge Conflicts

A merge conflict occurs when Git cannot automatically reconcile changes. For example, both branches may modify the same part of a file in incompatible ways.

Git marks the conflicting section in the file:

```text
<<<<<<< HEAD
Current branch version
=======
Incoming branch version
>>>>>>> feature
```

- `<<<<<<< HEAD` marks the beginning of the current branch's version.
- `=======` separates the two versions.
- `>>>>>>> feature` marks the end of the incoming branch's version.

The exact branch names and labels may differ depending on the operation.

### How to resolve a conflict

1. Check which files have conflicts.

   ```bash
   git status
   ```

2. Open each conflicted file and decide what the final content should be.

3. Remove the conflict markers and keep the correct content.

4. Stage the resolved files.

   ```bash
   git add path/to/file
   ```

5. Complete the merge.

   ```bash
   git commit
   ```

   For a normal merge conflict, Git prepares a merge commit message. Review it and save the commit to finish the merge.

**Important:** Do not simply remove the markers without checking the code or text between them. You must decide which changes to keep, and you may need to combine both versions.

### Abort a merge

If you want to cancel an in-progress merge before completing it:

```bash
git merge --abort
```

This attempts to restore the state from before the merge started. It may not fully reconstruct pre-merge changes in every situation, so avoid starting a merge with important uncommitted changes.

## 7. Working with Remote Branches

Local branches and remote-tracking branches are different. A remote-tracking branch records your local view of a branch on a remote repository; it is updated by operations such as `git fetch`.

| Command | Description |
|---|---|
| `git fetch` | Update remote-tracking references without integrating changes into the current branch. |
| `git branch -r` | List remote-tracking branches. |
| `git branch -a` | List local and remote-tracking branches. |
| `git push -u origin feature` | Push `feature` and set its upstream tracking branch. |
| `git push origin --delete feature` | Delete the `feature` branch from the remote repository. |

### Publish a new branch

```bash
git switch -c feature
# Make changes and commit them
git push -u origin feature
```

The `-u` option sets the upstream branch, allowing future `git push` and `git pull` commands to use that tracking relationship by default.

**Note:** Deleting a local branch does not delete the remote branch, and deleting a remote branch does not automatically delete the local branch.

## 8. Quick Reference

| Task | Command |
|---|---|
| List local branches | `git branch` |
| List all branches | `git branch -a` |
| Create a branch | `git branch feature` |
| Switch branches | `git switch feature` |
| Create and switch to a branch | `git switch -c feature` |
| Rename the current branch | `git branch -m new-name` |
| Merge a branch into the current branch | `git merge feature` |
| Delete a merged local branch | `git branch -d feature` |
| Force-delete a local branch | `git branch -D feature` |
| Abort an in-progress merge | `git merge --abort` |
| List remote-tracking branches | `git branch -r` |
| Publish a branch and set its upstream | `git push -u origin feature` |
| Delete a remote branch | `git push origin --delete feature` |

## Further Reading

- [Create or Clone a Repository](./create_a_repo.md)
- [Regular Workflow](./regular_workflow.md)
- [Git Command Reference](./git_reference.md)
- [Conventional Commits](./conventional_commits.md)
- [Undoing Changes](./undo_changes.md)
