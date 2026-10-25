# Git - Regular Workflow

This guide covers the typical workflow when working on an existing Git repository.

## 1. Before Starting Work

### Step 1: Check the repository status
```bash
git status
```
Shows the current state of the working tree and staging area.

### Step 2: Get the latest remote changes
```bash
git pull
```
Fetches remote changes and integrates them into the current branch.
**Note:** This assumes the current branch has an upstream branch configured. If you have uncommitted changes, check their status before pulling, as they may conflict with incoming changes.

## 2. After Modifying Files

### Step 1: Check the changes
```bash
git status
```
*Shows modified, deleted, and untracked files.*
To inspect the changes made to tracked files:
```bash
git diff
```
*Displays changes that have not yet been staged.*

### Step 2: Stage the changes
Stage all changes in the current directory and its subdirectories:
```bash
git add .
```
Alternatively, stage a specific file:
```bash
git add path/to/file
```

### Step 3: Review the staged changes
```bash
git diff --staged
```
Displays the changes that will be included in the next commit.

### Step 4: Create a commit
```bash
git commit -m "type: describe the change"
```
Records the staged changes in the local repository history.
Use [Conventional Commits](./conventional_commits.md) to structure commit messages consistently.

### Step 5: Push the commits
```bash
git push
```
Uploads local commits to the remote repository.

## 3. The Complete Workflow

The usual sequence is:
```bash
git pull
git status
git add .
git diff --staged
git commit -m "type: describe the change"
git push
```
**Important:** Review the staged changes before committing. If `git status` shows no changes, you may not need to run `git add` or `git commit`.

## 4. Fixing Common Mistakes

### - Unstage a File (Keep Its Changes)

If you accidentally staged a file and want to remove it from the staging area without losing its changes:
```bash
git restore --staged path/to/file
```
To unstage all files:
```bash
git restore --staged .
```
The changes remain in your working directory; they are simply no longer staged for the next commit.

### - Fix the Last Commit Before Pushing

If you created the last commit but have not pushed it yet, you can change its message:
```bash
git commit --amend -m "type: corrected message"
```
If you forgot to include some changes or files:
```bash
git add path/to/file
git commit --amend --no-edit
```
`--amend` replaces the last commit with a new one. Use it to modify the latest commit, not an earlier commit in the history.

### - Undo the Last Commit Before Pushing

If you want to undo the last commit but keep its changes staged:
```bash
git reset --soft HEAD~1
```
If you want to keep the changes but unstage them:
```bash
git reset --mixed HEAD~1
```
`--mixed` is the default behavior of `git reset`. Neither command removes the changes from your working directory.

### - Undo a Commit That Has Already Been Pushed

If you want to undo a commit that has already been pushed without rewriting the shared history:
```bash
git revert COMMIT_HASH
git push
```
This creates a new commit that reverses the changes introduced by the specified commit.

If you need to modify a commit that has already been pushed, you can use `git commit --amend`, but updating the remote history will usually require a force push. Avoid doing this on shared branches unless you understand the consequences and have coordinated with other contributors.

## 5. Quick Reference

| Situation | Command |
|---|---|
| Fetch and integrate remote changes | `git pull` |
| Check the repository status | `git status` |
| View unstaged changes | `git diff` |
| Stage all changes in the current directory and its subdirectories | `git add .` |
| Stage a specific file | `git add path/to/file` |
| Review staged changes | `git diff --staged` |
| Create a commit | `git commit -m "type: description"` |
| Push local commits to the remote repository | `git push` |
| Unstage a file without losing its changes | `git restore --staged path/to/file` |
| Unstage all changes | `git restore --staged .` |
| Amend the last commit message | `git commit --amend -m "type: corrected message"` |
| Add forgotten changes to the last commit | `git add path/to/file` followed by `git commit --amend --no-edit` |
| Undo the last commit and keep changes staged | `git reset --soft HEAD~1` |
| Undo the last commit and keep changes unstaged | `git reset --mixed HEAD~1` |
| Safely undo a pushed commit | `git revert COMMIT_HASH` followed by `git push` |
