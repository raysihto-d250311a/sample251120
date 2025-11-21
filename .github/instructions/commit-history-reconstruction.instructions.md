# Commit History Reconstruction Instructions

Before merging this PR, rebuild the commit history into a clear, logical form.
Commits should serve as documentation for future readers, not as a work log.

## Steps

1. **Add one commit that fully reverts current PR changes** (restore base branch state).
2. **Reapply all PR changes in commits grouped by logical responsibility:**
   - Each commit must have one coherent purpose ("what and why").
   - Avoid trivial commits; do not mix unrelated concerns or oversplit without reason.
   - Include tests and migrations in the same commit as their related feature.

## Rules

- Final HEAD must match the current PR exactly.
- No behavioral changes.
- Use clear English commit messages.
- Follow [Conventional Commits](https://www.conventionalcommits.org/) format: `<type>(<scope>): <description>`

## Output

- **List of new commits** (hash + subject).
- **Two GitHub compare URLs for verification** (replace OWNER, REPO, and hash placeholders with actual values):
  1. After revert (should show **no diff**):
     - `https://github.com/OWNER/REPO/compare/BASE_BRANCH..AFTER_REVERT_HASH`
  2. After reapply (should show **no diff**):
     - `https://github.com/OWNER/REPO/compare/BEFORE_REVERT_HASH..FEATURE_BRANCH`
- **Additionally, provide** (so a human can open this as a new PR if needed):
  1. Suggested feature-branch name (follow project naming guidelines).
  2. Suggested PR title (follow project title guidelines).
  3. Suggested PR description in a markdown code block, summarizing the reconstructed commit set and its purpose.

**Note:** A human will handle force-push/rebase afterward (not your task).

## Commit Organization Guidelines

When organizing commits for this repository, follow these guidelines:

### Preparation vs. Main Changes

- **Preparation commits** should include:
  - Refactoring of existing code or documentation
  - Infrastructure changes that enable the main feature
  - Documentation updates about system structure or organization
  - Changes to existing files that add metadata or reorganize without adding new features

- **Main change commits** should include:
  - New features or functionality
  - New files implementing the primary purpose
  - Documentation updates about specific features or usage
  - Implementation of the primary purpose of the PR

### Key Principles

1. **Separate preparation from main change**: When changes require preparation, split them into a preparation commit followed by a main change commit
2. **Group related changes**: All preparation changes should be grouped together; all main feature changes should be grouped together
3. **Documentation follows code**: Documentation about infrastructure and system organization belongs in preparation commits; documentation about specific features belongs in main change commits
4. **Clear commit boundaries**: Each commit should have a distinct, coherent purpose

### Example

For a PR adding a language configuration system:
- **Preparation commit**: Add instruction type metadata to existing files, update documentation with system structure explanation
- **Main change commit**: Add new feature files, update documentation with feature-specific usage information

## Repository Conventions

For branch naming, commit messages, and PR titles, please refer to [CONTRIBUTING.md](../../CONTRIBUTING.md).
