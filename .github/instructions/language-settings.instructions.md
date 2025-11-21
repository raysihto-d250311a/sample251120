# Language Settings

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
- [ ] Configure Copilot to use user's prompt language for interactions
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
