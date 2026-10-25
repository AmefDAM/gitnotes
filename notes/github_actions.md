# GitHub Actions

GitHub Actions is an automation platform integrated into GitHub. It allows you to run tasks automatically in response to events such as pushing commits, opening pull requests, or manually starting a workflow.

Common uses include running tests, checking code quality, building applications, and deploying websites.

## 1. Core Concepts

| Term | Description |
|---|---|
| **Workflow** | An automated process defined in a YAML file. |
| **Event** | An action that triggers a workflow, such as a push or pull request. |
| **Job** | A group of steps executed on a runner. |
| **Step** | An individual task within a job. |
| **Action** | A reusable unit of automation used in a workflow step. |
| **Runner** | The machine that executes a job. |
| **Artifact** | A file or collection of files produced by a workflow and stored for later use. |

A workflow can contain one or more jobs, and each job contains one or more steps.

## 2. Where Workflows Are Stored

GitHub Actions workflow files must be stored in this directory in your repository:

```text
.github/
└── workflows/
    └── main.yml
```

Workflow files use YAML syntax and commonly have the `.yml` or `.yaml` extension.

## 3. Your First Workflow

The following workflow checks whether changes are pushed to the `main` branch and prints a message.

Create `.github/workflows/main.yml`:

```yaml
name: First Workflow

"on":
  push:
    branches:
      - main

jobs:
  greeting:
    runs-on: ubuntu-latest

    steps:
      - name: Display a message
        run: echo "Hello from GitHub Actions!"
```

### How it works

- `name`: The workflow's display name.
- `on`: Defines the events that trigger the workflow.
- `push`: Runs the workflow when commits are pushed.
- `branches`: Restricts the trigger to the `main` branch.
- `jobs`: Defines the jobs in the workflow.
- `runs-on`: Selects the runner environment.
- `steps`: Lists the tasks to execute.
- `run`: Executes a shell command on the runner.

When you push a commit to `main`, GitHub Actions starts the workflow automatically.

**Note:** Quoting `"on"` avoids parsing issues with some YAML tools that interpret `on` as a boolean instead of a string. GitHub Actions accepts both `on:` and `"on":`.

## 4. Running Python Tests

GitHub Actions can run tests automatically whenever code is pushed. This example checks out the repository, installs Python, and runs `pytest`.

Create `.github/workflows/python-tests.yml`:

```yaml
name: Python Tests

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Check out repository
        uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.12"

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install pytest

      - name: Run tests
        run: pytest
```

### Important details

- `actions/checkout` checks out the repository so the runner can access its files.
- `actions/setup-python` installs and configures the requested Python version.
- `with` passes configuration options to an action.
- The `run` block can execute multiple shell commands.
- `pytest` runs the tests found by pytest's discovery rules.

**Note:** This example assumes your repository contains tests compatible with `pytest`. If your project uses another test framework or has a different directory structure, adapt the workflow accordingly. For reproducible builds, manage and install the project's actual dependencies rather than assuming `pytest` is the only dependency.

## 5. Environment Variables and Secrets

Workflows often need configuration values, API keys, or deployment credentials.

### Environment variables

```yaml
steps:
  - name: Display environment
    run: echo "Environment: $APP_ENV"
    env:
      APP_ENV: development
```

The `env` section defines an environment variable available to that step.

### Secrets

Sensitive values should be stored in GitHub Actions secrets rather than written directly into workflow files.

For example:

```yaml
steps:
  - name: Run deployment
    run: ./deploy.sh
    env:
      DEPLOY_TOKEN: ${{ secrets.DEPLOY_TOKEN }}
```

Create the secret in the repository's **Settings → Secrets and variables → Actions**.

**Security note:** Never print secrets to logs, commit them to the repository, or expose them to untrusted pull-request workflows. Grant workflows only the permissions they need.

## 6. Viewing Workflow Results

After pushing a commit:

1. Open the repository on GitHub.
2. Select the **Actions** tab.
3. Select the workflow run.
4. Open a job to inspect its steps and logs.

A workflow run may succeed, fail, or be cancelled. The logs help identify which step needs attention.

## 7. Deployment Automation

GitHub Actions can also deploy websites and applications. The exact workflow depends on the hosting provider and deployment method.

A typical deployment process looks like this:

```text
Push to main
     |
     v
Run checks and tests
     |
     v
Build the project
     |
     v
Deploy the generated files
     |
     v
Website or application updated
```

For a static website, deployment may involve publishing HTML, CSS, and JavaScript files. For a PHP and MySQL application, the process is different: the PHP application and database generally need a compatible server environment, and database migrations or other deployment steps may be necessary.

**Important:** GitHub Actions does not automatically deploy a project merely because the workflow exists. You must configure the deployment destination, credentials, permissions, and deployment commands.

## 8. Quick Reference

| Task | YAML or location |
|---|---|
| Name a workflow | `name: Workflow Name` |
| Trigger on a push | `on: push` |
| Trigger on pull requests | `on: pull_request` |
| Restrict a trigger to `main` | `branches: [main]` |
| Define a job | `jobs:` |
| Select an Ubuntu runner | `runs-on: ubuntu-latest` |
| Execute a shell command | `run: echo "Hello"` |
| Use a reusable action | `uses: owner/action@version` |
| Pass action inputs | `with:` |
| Define environment variables | `env:` |
| Access a repository secret | `${{ secrets.SECRET_NAME }}` |
| Store workflow files | `.github/workflows/` |

## Further Reading

- [GitHub Actions documentation](https://docs.github.com/en/actions)
- [Understanding GitHub Actions](https://docs.github.com/en/actions/about-github-actions/understanding-github-actions)
- [Workflow syntax](https://docs.github.com/en/actions/writing-workflows/workflow-syntax-for-github-actions)
- [GitHub Actions security](https://docs.github.com/en/actions/security-for-github-actions/security-guides/security-hardening-for-github-actions)

