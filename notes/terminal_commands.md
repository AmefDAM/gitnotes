# Terminal Commands

A practical reference for navigating directories, managing files, and working with projects from the terminal.

These commands are useful when working with Git, GitHub, and Visual Studio Code, but they are **not "Git commands"**. Their behavior may vary depending on the operating system and shell.

## 1. Navigation

| Command | Description |
|---|---|
| `pwd` | Display the current working directory. |
| `ls` | List files and directories in the current directory. |
| `ls -la` | List all files, including hidden files, with detailed information. |
| `cd directory` | Move into a directory. |
| `cd ..` | Move to the parent directory. |
| `cd ~` | Move to the user's home directory. |
| `cd -` | Return to the previous working directory in shells that support it. |

Examples:

```bash
pwd
ls -la
cd my-project
cd ..
```

## 2. Creating and Managing Files and Directories

| Command | Description |
|---|---|
| `mkdir directory` | Create a directory. |
| `mkdir -p path/to/directory` | Create a directory and any missing parent directories. |
| `touch file.txt` | Create an empty file if it does not exist, or update its modification timestamp if it does. |
| `cp source destination` | Copy a file. |
| `mv source destination` | Move or rename a file or directory. |
| `rm file.txt` | Delete a file. |
| `rmdir directory` | Remove an empty directory. |

Examples:

```bash
mkdir my-project
touch README.md
cp README.md README_backup.md
mv README_backup.md backup.md
rm backup.md
```

**Warning:** `rm` deletes files without moving them to the recycle bin. Be especially careful with recursive deletion commands such as `rm -r`.

## 3. Opening Projects in Visual Studio Code

| Command | Description |
|---|---|
| `code .` | Open the current directory in VS Code. |
| `code file.py` | Open a specific file in VS Code. |
| `code -n .` | Open the current directory in a new VS Code window. |

Example:

```bash
cd my-project
code .
```

If you are already working inside VS Code, you can open its integrated terminal using **Terminal → New Terminal**. You do not need to open a separate terminal application.

**Note:** The `code` command must be available in your terminal. If it is not recognized, your VS Code installation or system PATH may need configuring.

## 4. Inspecting Files and Searching

| Command | Description |
|---|---|
| `cat file.txt` | Display a file's contents. |
| `less file.txt` | Read a file page by page in supported terminals. |
| `head -n 10 file.txt` | Display the first 10 lines. |
| `tail -n 10 file.txt` | Display the last 10 lines. |
| `grep "text" file.txt` | Search for text in a file. |
| `find . -name "*.md"` | Find Markdown files under the current directory. |

Examples:

```bash
cat README.md
grep "TODO" README.md
find . -name "*.md"
```

## 5. Checking Installed Tools

| Command | Description |
|---|---|
| `git --version` | Display the installed Git version. |
| `python --version` | Display the Python version available through `python`. |
| `python3 --version` | Display the Python 3 version, where this command is available. |
| `code --version` | Display the installed VS Code version, if the command is available. |

The exact command names depend on the operating system and how the tools were installed.

## 6. Windows vs. Linux and macOS

Some commands differ between shells and operating systems.

| Task | Linux / macOS / Bash | Windows Command Prompt | Windows PowerShell |
|---|---|---|---|
| Show current directory | `pwd` | `cd` | `Get-Location` |
| List files | `ls` | `dir` | `Get-ChildItem` or `ls` |
| Change directory | `cd folder` | `cd folder` | `cd folder` |
| Create a directory | `mkdir folder` | `mkdir folder` | `mkdir folder` |
| Remove a file | `rm file.txt` | `del file.txt` | `Remove-Item file.txt` |

**Note:** PowerShell supports aliases such as `ls`, `pwd`, and `rm`, but these are not necessarily the same programs as their Unix counterparts. Commands and options are not always interchangeable.

## 7. Quick Reference

| Task | Command |
|---|---|
| Show current directory | `pwd` |
| List files, including hidden files | `ls -la` |
| Enter a directory | `cd directory` |
| Go up one directory | `cd ..` |
| Create a directory | `mkdir directory` |
| Create an empty file | `touch file.txt` |
| Copy a file | `cp source destination` |
| Move or rename a file | `mv source destination` |
| Delete a file | `rm file.txt` |
| Open the current directory in VS Code | `code .` |
| Display a file's contents | `cat file.txt` |
| Find Markdown files | `find . -name "*.md"` |
| Check the Git version | `git --version` |

**Important:** This guide primarily uses Bash-style commands. If you use Windows Command Prompt or PowerShell, check the operating-system-specific alternatives before running commands.