# Contributing Guidelines

Thank you for contributing to this repository! Please follow these guidelines to maintain consistency.

## Branch Naming Convention

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

## Commit Message Format

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

## Pull Request Title

PR titles should follow the same format as commit messages:

```
<type>(<scope>): <description>
```

**Examples:**
- `fix(workflow): handle bot PR authors to prevent API error`
- `feat(ci): add automated linting workflow`
- `docs(readme): add contributing guidelines`
