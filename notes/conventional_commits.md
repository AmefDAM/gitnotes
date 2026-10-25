# Conventional Commits

Conventional Commits is a convention for writing consistent, descriptive commit messages. It makes changes easier to understand when reviewing a project's history.

## 1. Commit Message Structure

A Conventional Commit follows this format:

```text
type(scope): description
```

- **type**: The category of change.
- **scope** *(optional)*: The part of the project affected by the change.
- **description**: A short summary of the change, written in the imperative mood.

Example:

```bash
git commit -m "docs(regular_workflow): add regular Git workflow guide"
```

In this example:
- `docs` identifies the change as documentation.
- `regular_workflow` identifies the affected file or area.
- `add regular Git workflow guide` describes the change.

## 2. Common Commit Types

| Type | Purpose | Example |
|---|---|---|
| `feat` | Introduce a new feature | `feat(login): add password recovery` |
| `fix` | Fix a bug | `fix(validation): reject empty usernames` |
| `docs` | Add or update documentation | `docs(readme): update project instructions` |
| `style` | Changes that do not affect code meaning, such as formatting | `style: fix indentation` |
| `refactor` | Restructure code without changing its external behavior | `refactor(auth): simplify login logic` |
| `perf` | Improve performance | `perf(search): reduce lookup time` |
| `test` | Add or modify tests | `test(login): add invalid password cases` |
| `build` | Change build systems or external dependencies | `build: update project dependencies` |
| `ci` | Change continuous integration configuration | `ci: add automated tests` |
| `chore` | Other maintenance tasks that do not fit a more specific type | `chore: remove temporary files` |
| `revert` | Revert a previous commit | `revert: undo login validation change` |

**Note:** These types are commonly used, but the Conventional Commits specification does not require this exact list. Teams can define additional types.

## 3. Writing Good Commit Messages

Follow these guidelines to make commit messages clear and consistent:

- Use lowercase for the type and scope.
- Keep the description concise and specific.
- Use the imperative mood: `add`, `fix`, `update`, `remove`.
- Do not end the description with a period.
- Use a scope when it helps identify the affected part of the project.
- Omit the scope when it adds no useful information.

Examples:

```text
docs: add Git installation instructions
docs(create_a_repo): explain repository initialization
feat: add user registration
fix(parser): handle empty input
```

## 4. Breaking Changes

A breaking change introduces a modification that is incompatible with previous behavior.

There are two common ways to indicate one.

### Option A: Add `!` after the type or scope

```text
feat(api)!: remove the legacy endpoint
```

### Option B: Add a `BREAKING CHANGE:` footer

```text
feat(api): update the response format

BREAKING CHANGE: the response no longer includes the legacy field
```

The `!` marker and the footer can also be used together.

## 5. Commit Message Examples

These examples illustrate how to choose a type based on the change being made.

| Change | Commit message |
|---|---|
| Create a new Markdown guide | `docs: add Git command reference` |
| Update an existing guide | `docs(regular_workflow): clarify the pull workflow` |
| Correct a typo in documentation | `docs: fix spelling mistakes` |
| Add a new Python feature | `feat: add number multiplication function` |
| Fix a Python bug | `fix: handle negative numbers correctly` |
| Add automated tests | `test: add edge case coverage` |
| Update a GitHub Actions workflow | `ci: add Python test workflow` |
| Remove an unnecessary file | `chore: remove temporary text file` |

## 6. Quick Reference

| Rule | Format |
|---|---|
| Basic structure | `type: description` |
| With a scope | `type(scope): description` |
| Breaking change | `type!: description` |
| Breaking change with scope | `type(scope)!: description` |
| Breaking change footer | `BREAKING CHANGE: explanation` |

Create a commit using the chosen message:

```bash
git add path/to/file
git commit -m "type(scope): description"
git push
```

For a commit that changes several files, stage the relevant files before committing. The commit message should describe the overall change, not merely list the filenames.

**Reference:** [Conventional Commits specification](https://www.conventionalcommits.org/en/v1.0.0/)