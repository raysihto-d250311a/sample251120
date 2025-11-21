# 日本語設定

このリポジトリにおける Copilot とのすべてのやりとりは日本語で行ってください。

## 基本ルール

- **Copilot との対話**: すべての指示への応答、説明、Copilot からのレビュー指摘は日本語で行ってください
- **リポジトリのアウトプット**: コミットメッセージ、PR タイトル、PR 説明、チェックリスト、コード内コメント、コード内エラーメッセージは英語で記述してください
- **言語の使い分け**:
  - 日本語: Copilot とのやりとり、Copilot への指示の応答、Copilot からのレビュー指摘
  - 英語: リポジトリの標準共通言語として、すべてのアウトプット（コミット、PR、コードなど）

## 進捗報告の形式

`report_progress` ツールを使用する際は、以下の形式に従ってください：

- **コミットメッセージ**: Conventional Commits 形式で英語で記述
  - 例: `feat(workflow): add bot PR author handling`
  - 例: `fix(ci): fix auto-linting workflow`
  - 例: `docs(readme): add contributing guidelines`

- **PR 説明**: マークダウンチェックリストを使用し、英語で記述
  - 例: `- [x] Task completed`
  - 例: `- [ ] Task pending`

## 例

### 進捗報告の例（英語）

コミットメッセージ:
```
feat(copilot): add Japanese language configuration
```

PR 説明:
```
- [x] Understand the problem and repository structure
- [x] Create Japanese language configuration file in `.github/instructions/`
- [ ] Configure Copilot to use Japanese for interactions
- [ ] Verify the changes work correctly
- [ ] Review and finalize
```

### Copilot との対話の例（日本語）

✅ 良い例（日本語で Copilot と対話）:
```
リポジトリを探索しました。`.github/instructions` ディレクトリに新しい設定ファイルを作成します。
```

❌ 悪い例（英語で Copilot と対話）:
```
I've explored the repository. I'll create a new configuration file in `.github/instructions`.
```

## 注意事項

- リポジトリの「アウトプット」（コミット、PR、コード、ドキュメント）は標準共通言語である英語で記述してください
- Copilot との「やりとり」（対話、説明、レビュー応答）は日本語で行ってください
- 既存のドキュメントやコードが英語の場合、必要最小限の変更のみを行い、不要な翻訳は避けてください
- 変数名、関数名、ファイル名などは、既存のコーディング規約に従ってください
