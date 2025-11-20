# sample251120

A test repository for automatically closing pull requests from users without write access.

## Features

This repository automatically closes pull requests from users who do not have write access (collaborators with write, maintain, or admin permissions).

### How it works

- When a pull request is opened or reopened, a GitHub Actions workflow is triggered
- The workflow checks the permission level of the PR author
- Bot accounts (like GitHub Apps and bots) are automatically allowed
- If the author is a regular user without write, maintain, or admin access, the PR is automatically closed with a comment

### Workflow

The auto-close functionality is implemented via GitHub Actions workflow located at:
`.github/workflows/auto-close-non-writable-prs.yml`

The workflow:
1. Triggers on `pull_request_target` events (opened, reopened)
2. Checks if the PR author is a bot - if so, allows the PR
3. For regular users, checks the PR author's permission level using GitHub API
4. Closes the PR and adds a comment if the author lacks write access

## Contributing Guidelines

### Branch Naming Convention

When creating a new branch, use the following format:

```
{type}/{scope}/{summary_in_snake_case}
```

**Type:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting, etc.)
- `refactor`: Code refactoring
- `test`: Adding or updating tests
- `chore`: Maintenance tasks

**Scope:**
- A short identifier for the affected component or area (e.g., `workflow`, `readme`, `ci`)

**Summary:**
- A brief description in snake_case (e.g., `add_bot_handling`, `update_permissions`)

**Examples:**
- `fix/workflow/handle_bot_pr_authors`
- `feat/ci/add_linting_workflow`
- `docs/readme/add_contributing_guidelines`

### Commit Message Format

Follow [Conventional Commits](https://www.conventionalcommits.org/) format:

```
<type>(<scope>): <description>

[optional body]

[optional footer]
```

**Examples:**
- `fix(workflow): handle bot PR authors to prevent API error`
- `feat(ci): add automated linting workflow`
- `docs(readme): add contributing guidelines`

### Pull Request Title

PR titles should follow the same format as commit messages:

```
<type>(<scope>): <description>
```

**Examples:**
- `fix(workflow): handle bot PR authors to prevent API error`
- `feat(ci): add automated linting workflow`
- `docs(readme): add contributing guidelines`