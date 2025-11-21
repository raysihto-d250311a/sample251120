# Commit History Reconstruction Instructions

**Instruction Type:** On-Demand  
**Description:** This instruction should only be followed when the user explicitly requests commit history reconstruction. Do not apply these instructions automatically.

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

## Repository Conventions

For branch naming, commit messages, and PR titles, please refer to [CONTRIBUTING.md](../../CONTRIBUTING.md).
