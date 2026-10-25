# Git Command Reference

A categorized reference of commonly used Git commands. Use this guide to look up commands and understand their purpose without going through a complete workflow tutorial.

## 1. Repository Information

| Command | Description |
|---|---|
| `git status` | Show the current state of the working tree and staging area. |
| `git log` | Display the commit history. |
| `git log --oneline` | Display each commit on a single line. |
| `git log --oneline --graph --all` | Display a graph of commits across branches. |
| `git show` | Show information about a commit and its changes. |
| `git diff` | Show unstaged changes to tracked files. |
| `git diff --staged` | Show staged changes that will be included in the next commit. |

Examples:

```bash
git log --oneline
git log --oneline --graph --all
git show HEAD
```

## 2. Repository Configuration

| Command | Description |
|---|---|
| `git config --list` | Display the available Git configuration settings. |
| `git config user.name` | Display the configured commit author name for the current configuration context. |
| `git config user.email` | Display the configured commit author email for the current configuration context. |
| `git config --global user.name "Your Name"` | Set the author name for your global Git configuration. |
| `git config --global user.email "you@example.com"` | Set the author email for your global Git configuration. |
| `git config --get remote.origin.url` | Display the URL configured for the `origin` remote, if present. |

**Note:** `--global` applies a setting to your user account on the computer. Repository-specific settings can override global settings.

## 3. Working with Files

| Command | Description |
|---|---|
| `git add file.txt` | Stage changes to a specific file. |
| `git add .` | Stage changes under the current directory, subject to Git's ignore rules. |
| `git add -A` | Stage additions, modifications, and deletions throughout the working tree. |
| `git rm file.txt` | Remove a tracked file and stage its deletion. |
| `git mv old.txt new.txt` | Move or rename a file and stage the change. |
| `git ls-files` | List files tracked by Git. |
| `git check-ignore -v file.txt` | Show which ignore rule excludes a file, if any. |

**Note:** Git generally detects renames by comparing file content when examining changes; it does not store a rename as a separate file operation in the commit.

## 4. Commits

| Command | Description |
|---|---|
| `git commit -m "message"` | Create a commit using the staged changes. |
| `git commit -am "message"` | Stage modifications and deletions of tracked files and commit them. Does not include new untracked files. |
| `git commit --amend` | Replace the latest commit with a new version. |
| `git show HEAD` | Inspect the latest commit. |

**Important:** `git commit -am` does not stage new, untracked files. Use `git add` first when adding new files.

For message conventions, see [Conventional Commits](./conventional_commits.md).

For detailed commit correction and recovery procedures, see [Undoing Changes](./undo_changes.md) when that guide is available.

## 5. Remote Repositories

| Command | Description |
|---|---|
| `git remote -v` | List configured remotes and their URLs. |
| `git remote add origin REPOSITORY_URL` | Add a remote named `origin`. |
| `git remote remove origin` | Remove the remote named `origin` from the local configuration. |
| `git fetch` | Download remote references and objects without integrating them into the current branch. |
| `git fetch --all` | Fetch from all configured remotes. |
| `git pull` | Fetch and integrate changes from the configured upstream branch or specified remote branch. |
| `git push` | Upload local commits to the configured remote destination. |
| `git push -u origin main` | Push `main` to `origin` and set the upstream tracking relationship. |
| `git ls-remote origin` | List references advertised by the remote named `origin`. |

**Note:** `git fetch` updates your local knowledge of remote branches but does not merge those changes into your current branch. `git pull` fetches and then integrates changes according to your configuration.

## 6. Tags

Tags are named references commonly used to mark specific commits, such as software releases.

| Command | Description |
|---|---|
| `git tag` | List local tags. |
| `git tag v1.0.0` | Create a lightweight tag at the current commit. |
| `git tag -a v1.0.0 -m "Release 1.0.0"` | Create an annotated tag with a message. |
| `git show v1.0.0` | Display information about a tag and its target. |
| `git push origin v1.0.0` | Push a specific tag to the remote. |
| `git push origin --tags` | Push all local tags that do not already exist on the remote. |

## 7. Ignore Rules

A `.gitignore` file specifies intentionally untracked files that Git should ignore.

Example `.gitignore`:

```gitignore
# Python cache files
__pycache__/
*.py[cod]

# Virtual environments
.venv/
venv/

# Environment variables and secrets
.env

# Editor and operating system files
.vscode/
.DS_Store
Thumbs.db
```

| Command or file | Description |
|---|---|
| `.gitignore` | Defines patterns for files Git should ignore when they are untracked. |
| `git check-ignore -v file.txt` | Identify the ignore rule matching a file. |
| `git status --ignored` | Include ignored files in the status output. |

**Important:** Adding a file to `.gitignore` does not stop Git tracking it if it has already been committed. Removing a tracked file from the index without deleting the local copy requires a different command:

```bash
git rm --cached file.txt
```

## 8. Quick Reference

| Task | Command |
|---|---|
| Check repository status | `git status` |
| View recent commits | `git log --oneline` |
| View commit graph | `git log --oneline --graph --all` |
| Inspect the latest commit | `git show HEAD` |
| View unstaged changes | `git diff` |
| View staged changes | `git diff --staged` |
| View remotes | `git remote -v` |
| Download remote updates without integrating them | `git fetch` |
| Stage all changes under the current directory | `git add .` |
| Stage all additions, modifications, and deletions | `git add -A` |
| Remove a tracked file | `git rm file.txt` |
| Show tracked files | `git ls-files` |
| List tags | `git tag` |
| Check ignored files | `git status --ignored` |
| Check Git version | `git --version` |

## Further Reading

- [Create or Clone a Repository](./create_a_repo.md)
- [Regular Workflow](./regular_workflow.md)
- [Terminal Commands](./terminal_commands.md)
- [Conventional Commits](./conventional_commits.md)
- [Branches and Merging](./branches_and_merging.md)
- [Undoing Changes](./undo_changes.md)
