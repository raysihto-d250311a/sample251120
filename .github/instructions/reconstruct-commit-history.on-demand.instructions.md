# Commit History Reconstruction Instructions

**Instruction Type:** On-Demand  
**Description:** This instruction should only be followed when the user explicitly requests commit history reconstruction. Do not apply these instructions automatically.

Before merging this PR, rebuild the commit history into a clear, logical form.
Commits should serve as documentation for future readers, not as a work log.

**IMPORTANT**: The first step is to create a revert commit that undoes all PR changes. This is a required step that must not be skipped. Only after the revert commit is created and verified should you proceed to reapply changes in logical commits.

Trigger with any of:

- `@copilot reconstruct-commit-history`  (primary)
- `@copilot reconstruct-commits`         (alias)
- `@copilot rebuild-commits`             (alias)
- `@copilot rewrite-commits`             (alias)
- `@copilot reorder-commits`             (alias)

## Steps

### Step 1: Create Revert Commit (REQUIRED - DO NOT SKIP)

**CRITICAL**: You MUST create and commit a revert commit as the first step. This is not optional.

1. **Create a single revert commit that completely reverts all PR changes**
   - This commit MUST restore the codebase to match the base branch exactly
   - Use `git revert` or manually undo all changes from the PR
   - Verify that after this commit, there are NO differences between your branch and the base branch
   - Example commit message: `revert: revert all PR changes for reconstruction`

**Verification after Step 1:**
- Run `git diff <base-branch>..HEAD` - this MUST show NO differences
- The working tree should be identical to the base branch
- All PR changes should be completely undone

### Step 2: Reapply Changes in Logical Commits

After completing Step 1 and verifying the revert, reapply all PR changes in well-organized commits:

1. **Reapply all PR changes in commits grouped by logical responsibility:**
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

- **Confirmation that Step 1 revert commit was created** - state the commit hash and verify no diff with base branch
- **List of all new commits** (hash + subject), starting with the revert commit
- **Exactly two GitHub compare URLs for verification**:
  1. After revert (should show **no diff**):
     - `https://github.com/OWNER/REPO/compare/BASE_BRANCH..AFTER_REVERT_HASH`
     - Replace BASE_BRANCH with the actual branch name (e.g., `main`, `develop`)
     - Replace AFTER_REVERT_HASH with the actual commit hash (e.g., `a1b2c3d`)
  2. After reapply (should show **no diff**):
     - `https://github.com/OWNER/REPO/compare/BEFORE_REVERT_HASH..FEATURE_BRANCH`
     - Replace BEFORE_REVERT_HASH with the actual commit hash (e.g., `d4e5f6g`)
     - Replace FEATURE_BRANCH with the actual branch name (e.g., `feature/my-feature`)
  
  **Important**: Provide exactly these two compare URLs, no more. Use actual branch names (not commit hashes) for BASE_BRANCH and FEATURE_BRANCH.
- **Additionally, provide** (so a human can open this as a new PR if needed):
  1. Suggested feature-branch name (follow project naming guidelines: `{type}/{scope}/{summary_in_snake_case}` format).
  2. Suggested PR title (follow project title guidelines).
  3. Suggested PR description in a markdown code block, summarizing the reconstructed commit set and its purpose.

**Note:** A human will handle force-push/rebase afterward (not your task). This note is for your understanding only—do not include it in your output.

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

For branch naming, commit messages, and PR titles, please refer to [CONTRIBUTING.md](../../CONTRIBUTING.md).
