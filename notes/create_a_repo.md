# Hot to create a repo

There are two common ways to start working with Git:

- Create a repository from an existing local folder.
- Clone an existing remote repository.

## - From an existing folder

*Use this method when you already have a project on your computer and want to start tracking it with Git.*

**(In terminal)**

### Step 1: Go to the proyect folder
```bash
cd path/to/project
```
### Step 2: Initialize Git
```bash
git init
```
Initializes a new local Git repository in the current folder.
### Step 3: Check the repository status
```bash
git status
```
Shows untracked files and changes that Git detects.
### Step 4: Stage the files
```bash
git add .
```
Stages changes in the current directory and its subdirectories, except files excluded by Git's ignore rules.
### Step 5: Create the first commit
```bash
git commit -m "feat: add initial project"
```
Creates the first commit containing the staged changes.
### Step 6: Connect the local repository to GitHub
Create an empty repository on GitHub, then copy its repository URL.
```bash
git remote add origin REPOSITORY_URL
```
Adds the remote repository and names it `origin`.
### Step 7: Set the main branch
```bash
git branch -M main
```
Renames the current branch to `main`.
### Step 8: Push the repository to GitHub
```bash
git push -u origin main
```
Uploads the local commits to GitHub and sets `origin/main` as the upstream branch for future pushes and pulls.

**Note:** These steps assume the GitHub repository is empty. If it already contains commits, such as an initial README, you may need to integrate the remote history before pushing.

## - Clone an existing repository

*Use this method when a repository already exists on GitHub and you want a local copy on your computer.*

**(In terminal)**

### Step 1: Clone the repository
```bash
git clone REPOSITORY_URL
```
Downloads the repository and its history into a new local folder.
### Step 2: Navigate into the repository folder
```bash
cd repository-name
```
The folder name usually matches the repository name.
### Step 3: Open the project in VS Code (opyional)
*If you are using an external terminal, you can open the current folder in VS Code:*
```bash
code .
```
If you are already working in VS Code, open the integrated terminal `(Terminal > New Terminal)` and continue from there.

**Note:** Git commands work the same way in both terminals, provided you are in the correct repository folder and Git is installed and available in the terminal.
### Step 4: Check the repository status
```bash
git status
```
Checks the current state of the local repository.