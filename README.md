# sample251120

A test repository for testing GitHub Actions workflows.

## Features

### Auto-close Pull Requests

This repository automatically closes pull requests from users who do not have write access (collaborators with write, maintain, or admin permissions).

### Version Tagging Test

This repository includes a simplified workflow to test automatic version tagging functionality.

## Workflows

#### Auto-close Pull Requests

The auto-close functionality is implemented via GitHub Actions workflow located at:
`.github/workflows/auto-close-non-writable-prs.yml`

**How it works:**
- When a pull request is opened or reopened, a GitHub Actions workflow is triggered
- The workflow checks the permission level of the PR author
- Bot accounts (like GitHub Apps and bots) are automatically allowed
- If the author is a regular user without write, maintain, or admin access, the PR is automatically closed with a comment

**Workflow steps:**
1. Triggers on `pull_request_target` events (opened, reopened)
2. Checks if the PR author is a bot - if so, allows the PR
3. For regular users, checks the PR author's permission level using GitHub API
4. Closes the PR and adds a comment if the author lacks write access

#### Version Tagging Test

A simplified version tagging workflow is located at:
`.github/workflows/bump-version-test.yml`

This workflow demonstrates automatic version tagging without dependencies on external services or secrets:
1. Triggers on push to `develop` branch or manually via `workflow_dispatch`
2. First runs a dry-run to preview what tag would be created
3. Then creates the actual version tag with `rc` suffix for pre-releases
4. Finally creates a GitHub release with the tag and changelog

**Key features:**
- Uses `mathieudutour/github-tag-action@v6.2` for automatic version bumping
- Appends `rc` to pre-release tags
- Creates changelog automatically from commit messages
- No external dependencies or secrets required (uses only `GITHUB_TOKEN`)

This is a simplified version extracted from a more complex production workflow that includes Docker image building and AWS deployment steps.

## Dependency Management

### Dependabot for GitHub Actions

This repository uses Dependabot to automatically keep GitHub Actions dependencies up to date. The configuration is located at:
`.github/dependabot.yml`

Dependabot will:
- Check for updates to GitHub Actions weekly
- Automatically create pull requests for version updates
- Label PRs with `dependencies` and `github-actions` tags
- Limit open PRs to 10 to avoid overwhelming the repository

This ensures that workflow actions (like `actions/checkout`, `mathieudutour/github-tag-action`, etc.) stay current with the latest security patches and features.

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