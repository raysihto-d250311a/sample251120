# GitHub Copilot Instructions

This file contains custom instructions for GitHub Copilot to follow when working in this repository.

---

# Language Settings

**Instruction Type:** Always-Active  
**Description:** This instruction is always active and must be followed in every Copilot session automatically.

Use the same language for Copilot interactions as the user uses in their prompts.

## Basic Rules

- **Copilot Interactions**: Use the same language as the user's prompt for all responses, explanations, and review feedback
- **Repository Outputs**: Always use English for commit messages, PR titles, PR descriptions, checklists, code comments, and error messages
- **Language Distinction**:
  - User's prompt language: Copilot interactions, instruction responses, review feedback
  - English: Standard language for all repository outputs (commits, PRs, code, etc.)

## Progress Reporting Format

When using the `report_progress` tool, follow this format:

- **Commit Messages**: Use Conventional Commits format in English
  - Example: `feat(workflow): add bot PR author handling`
  - Example: `fix(ci): fix auto-linting workflow`
  - Example: `docs(readme): add contributing guidelines`

- **PR Descriptions**: Use markdown checklists in English
  - Example: `- [x] Task completed`
  - Example: `- [ ] Task pending`

## Examples

### Progress Report Example (English)

Commit message:
```
feat(copilot): add language configuration
```

PR description:
```
- [x] Understand the problem and repository structure
- [x] Create language configuration file in `.github/instructions/`
- [x] Update README documentation
- [ ] Verify the changes work correctly
- [ ] Review and finalize
```

### Copilot Interaction Examples

If user prompts in Japanese:

✅ Good (respond in Japanese):
```
リポジトリを探索しました。`.github/instructions` ディレクトリに新しい設定ファイルを作成します。
```

❌ Bad (respond in English when user prompted in Japanese):
```
I've explored the repository. I'll create a new configuration file in `.github/instructions`.
```

If user prompts in English:

✅ Good (respond in English):
```
I've explored the repository. I'll create a new configuration file in `.github/instructions`.
```

❌ Bad (respond in Japanese when user prompted in English):
```
リポジトリを探索しました。`.github/instructions` ディレクトリに新しい設定ファイルを作成します。
```

## Notes

- Repository "outputs" (commits, PRs, code, documentation) must use English as the standard language
- Copilot "interactions" (responses, explanations, review feedback) should match the user's prompt language
- Minimize changes to existing documentation and code; avoid unnecessary translations
- Follow existing coding conventions for variable names, function names, file names, etc.

---

# Commit History Reconstruction Instructions

**Instruction Type:** On-Demand  
**Description:** This instruction should only be followed when the user explicitly requests commit history reconstruction. Do not apply these instructions automatically.

Before merging this PR, rebuild the commit history into a clear, logical form.
Commits should serve as documentation for future readers, not as a work log.

Trigger with any of:

- `@copilot reconstruct-commit-history`  (primary)
- `@copilot reconstruct-commits`         (alias)
- `@copilot rebuild-commits`             (alias)
- `@copilot rewrite-commits`             (alias)
- `@copilot reorder-commits`             (alias)

## Steps

1. **Add one commit that fully reverts current PR changes** (restore base branch state).
2. **Reapply all PR changes in commits grouped by logical responsibility:**
   - Each commit must have one coherent purpose ("what and why").
   - Create multiple preparation commits if there are multiple different preparation purposes.
   - Create multiple main change commits if there are multiple different main purposes.
   - Do NOT merge unrelated changes into a single commit just because they are both "preparation" or both "main change".
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
  1. Suggested feature-branch name (follow project naming guidelines: `{type}/{scope}/{summary_in_snake_case}` format).
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

1. **Each commit must have one coherent purpose**: This rule applies to ALL commits, including both preparation commits and main change commits. Do NOT mix multiple unrelated changes in a single commit.
2. **Separate preparation from main change**: When changes require preparation, split them into preparation commit(s) followed by main change commit(s)
3. **Multiple commits per category when needed**: 
   - Create multiple preparation commits if there are multiple different preparation purposes
   - Create multiple main change commits if there are multiple different main purposes
   - Each commit should address ONE coherent purpose only
4. **Group related changes**: Only group changes that serve the SAME coherent purpose. Do not group all preparation changes or all main feature changes if they serve different purposes.
5. **Documentation follows code**: Documentation about infrastructure and system organization belongs in preparation commits; documentation about specific features belongs in main change commits
6. **Clear commit boundaries**: Each commit should have a distinct, coherent purpose

### Examples

#### Example 1: Single preparation, single main change
For a PR adding a simple language configuration system:
- **Preparation commit**: Add instruction type metadata to existing files
- **Main change commit**: Add language configuration feature files and documentation

#### Example 2: Multiple preparation commits
For a PR that requires different types of preparation:
- **Preparation commit 1**: Refactor configuration loading infrastructure
- **Preparation commit 2**: Add instruction type metadata to existing files
- **Main change commit**: Add language configuration feature files and documentation

#### Example 3: Multiple main change commits
For a PR adding multiple independent features:
- **Preparation commit**: Add shared infrastructure for new features
- **Main change commit 1**: Add language configuration feature
- **Main change commit 2**: Add validation feature
- **Main change commit 3**: Add export feature

#### Example 4: Multiple preparation and multiple main change commits
For a complex PR:
- **Preparation commit 1**: Refactor existing configuration system
- **Preparation commit 2**: Add instruction type metadata to existing files
- **Preparation commit 3**: Update documentation with system structure explanation
- **Main change commit 1**: Add language configuration feature
- **Main change commit 2**: Add validation and export features with their specific documentation

**Important**: Each commit above has ONE coherent purpose. Do NOT merge commits just because they are both "preparation" or both "main change" - only merge if they serve the exact same purpose.

## Repository Conventions

For branch naming, commit messages, and PR titles, please refer to [CONTRIBUTING.md](CONTRIBUTING.md).
