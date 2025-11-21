# sample251120

A test repository for testing GitHub Actions workflows.

## Features

### Pull Request Care on Creation

This repository provides automated care and follow-up for pull requests when they are created:
- Automatically closes pull requests from users who do not have write access (collaborators with write, maintain, or admin permissions)
- Automatically assigns the PR author as the assignee when a pull request is created without any assignees (for PRs from users with write access)

### Version Tagging Test

This repository includes a simplified workflow to test automatic version tagging functionality.

## Workflows

### Pull Request Care on Creation

The PR care functionality is implemented via GitHub Actions workflow located at:
`.github/workflows/pr-care-on-creation.yml`

**How it works:**
- When a pull request is opened or reopened, a GitHub Actions workflow is triggered
- The workflow checks the permission level of the PR author
- Bot accounts (like GitHub Apps and bots) are automatically allowed
- If the author is a regular user without write, maintain, or admin access, the PR is automatically closed with a comment
- For PRs from users with write access (including bot accounts), if the PR has no assignees, the workflow automatically assigns the PR author as the assignee. This means bot accounts may also be auto-assigned as PR assignees if they open a PR without any assignees.

**Workflow steps:**
1. Triggers on `pull_request_target` events (opened, reopened)
2. Checks if the PR author is a bot - if so, allows the PR
3. For regular users, checks the PR author's permission level using GitHub API
4. Closes the PR and adds a comment if the author lacks write access
5. For PRs with write access, checks if the PR has any assignees and assigns the PR author if none exist

### Version Tagging and Release

A unified version tagging and release workflow is located at:
`.github/workflows/version-release.yml`

This workflow automatically creates version tags and releases based on the branch:
1. Triggers on push to `develop` or `main` branch, or manually via `workflow_dispatch`
2. First runs a dry-run to preview what tag would be created
3. Then creates the actual version tag
4. Finally creates a GitHub release with the tag and changelog

**Branch-specific behavior:**
- **develop branch**: Creates pre-release tags with `rc` suffix (e.g., `v1.0.0-rc.0`) and marks releases as pre-releases
- **main branch**: Creates production tags without `rc` suffix (e.g., `v1.0.0`) and marks releases as production releases

**Key features:**
- Uses `mathieudutour/github-tag-action@v6.2` for automatic version bumping
- Conditional logic with `github.ref` to differentiate between branches
- For main branch releases, compares with the previous production release (non-rc tag) for changelog generation
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

## Copilot Instructions

This repository uses GitHub Copilot custom instructions to customize Copilot behavior.

### How GitHub Copilot Loads Instructions

GitHub Copilot automatically loads custom instructions from two locations:
1. **`.github/copilot-instructions.md`**: Repository-wide instructions that apply to all files
2. **`.github/instructions/*.instructions.md`**: Path-specific instructions that can target specific files using YAML frontmatter with `applyTo` glob patterns

Both types of files are automatically loaded by Copilot - no manual inclusion or referencing is needed.

### Main Instructions File

The `.github/copilot-instructions.md` file contains repository-wide instructions:
- **Language Settings** (Always-Active): Configures language usage for Copilot interactions
- **Commit History Reconstruction** (On-Demand): Reference link for documentation purposes (actual instructions in separate file)

### Instruction Types

Two types of instructions are defined:

1. **Always-Active Instructions**
   - These instructions are always active and Copilot follows them automatically in every session
   - Each section includes `**Instruction Type:** Always-Active` in the header
   - Example: Language Settings - configures language usage for Copilot interactions

2. **On-Demand Instructions**
   - These instructions are only followed when explicitly requested by the user
   - Each section includes `**Instruction Type:** On-Demand` in the header
   - Example: Commit History Reconstruction - provides guidance for commit history cleanup

### Language Settings

The Language Settings (in `.github/copilot-instructions.md`) configures:
- Copilot interactions use the same language as the user's prompt (e.g., Japanese prompts receive Japanese responses)
- Repository outputs (commits, PRs, code) always use English as the standard language

### Path-Specific Instructions

The `.github/instructions/` directory can contain path-specific instruction files that use YAML frontmatter to target specific files or directories. Currently contains:
- `reconstruct-commit-history.on-demand.instructions.md` - commit history cleanup guidance (On-Demand)

These files are automatically loaded by GitHub Copilot when working on matching files.

## Contributing

Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on branch naming, commit messages, and pull request titles.
