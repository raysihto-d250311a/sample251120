# GitHub Copilot Instructions

This file contains instructions for GitHub Copilot to help maintain consistency and quality in this repository.

## Commit History Reconstruction Before Merge

Before merging this PR, rebuild the commit history into a clear, logical form.
Commits should serve as documentation for future readers, not as a work log.

### Steps:
1. **Add one commit that fully reverts current PR changes** (restore base branch state).
2. **Reapply all PR changes in commits grouped by logical responsibility:**
   - Each commit must have one coherent purpose ("what and why").
   - Avoid trivial commits; do not mix unrelated concerns or oversplit without reason.
   - Include tests and migrations in the same commit as their related feature.

### Rules:
- Final HEAD must match the current PR exactly.
- No behavioral changes.
- Use clear English commit messages.
- Follow [Conventional Commits](https://www.conventionalcommits.org/) format: `<type>(<scope>): <description>`

### Output:
- **List of new commits** (hash + subject).
- **Two GitHub compare URLs for verification:**
  1. After revert (should show **no diff**):
     - `https://github.com/OWNER/REPO/compare/BASE_BRANCH..AFTER_REVERT_HASH`
  2. After reapply (should show **no diff**):
     - `https://github.com/OWNER/REPO/compare/BEFORE_REVERT_HASH..FEATURE_BRANCH`
- **Additionally, provide** (so a human can open this as a new PR if needed):
  1. Suggested feature-branch name (follow project naming guidelines).
  2. Suggested PR title (follow project title guidelines).
  3. Suggested PR description in a fenced markdown code block (```markdown), summarizing the reconstructed commit set and its purpose.

**Note:** A human will handle force-push/rebase afterward (not your task).

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
