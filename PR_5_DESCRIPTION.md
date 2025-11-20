# PR #5: ワークフローのボット対応と貢献ガイドラインの追加

## 概要

このPRは、PR #3およびPR #4で提起された問題に対応するものです。主に以下の2つの改善を含みます：

1. **自動クローズワークフローのボット対応** - ボットアカウント（GitHub Appsなど）によるPRを適切に処理
2. **貢献ガイドラインの追加** - ブランチ命名規則、コミットメッセージ、PRタイトルの標準化

## 変更内容

### 1. ワークフローのボット対応 (`.github/workflows/auto-close-non-writable-prs.yml`)

**問題点:**
PR #3で発見された問題として、ボットアカウント（Copilotなど）がPRを作成した際に、GitHub APIの`getCollaboratorPermissionLevel`がエラーを返していました。このAPIはボットアカウントには対応していません。

**解決策:**
- PR作成者のタイプ（`user.type`）をチェックし、`Bot`の場合は権限チェックをスキップ
- ボットアカウントは全て信頼されたアカウントとして扱い、自動的に許可
- これにより、Copilot等のボットによるPRが正常に処理されるようになります

**変更箇所:**
```javascript
const userType = context.payload.pull_request.user.type;

// Accept all bot accounts without checking permissions
if (userType === 'Bot') {
  core.info(`${user} is a bot - allowing PR`);
  core.setOutput("permission", "admin");
  return;
}
```

### 2. 貢献ガイドラインの追加 (README.md)

PR #4で要求された標準化ガイドラインを追加しました。

**追加内容:**

#### ブランチ命名規則
フォーマット: `{type}/{scope}/{summary_in_snake_case}`

- **Type:** `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`
- **Scope:** 影響を受けるコンポーネントや領域（例: `workflow`, `readme`, `ci`）
- **Summary:** スネークケースでの簡潔な説明

例: `fix/workflow/handle_bot_pr_authors`

#### コミットメッセージフォーマット
[Conventional Commits](https://www.conventionalcommits.org/)形式に準拠:

```
<type>(<scope>): <description>

[optional body]

[optional footer]
```

例: `fix(workflow): handle bot PR authors to prevent API error`

#### PRタイトル
コミットメッセージと同じ形式を使用:

```
<type>(<scope>): <description>
```

## 影響範囲

### 追加機能
- ボットアカウントからのPRが正常に処理される
- 開発者向けの明確な貢献ガイドライン

### 変更されたファイル
- `.github/workflows/auto-close-non-writable-prs.yml` (+8行)
- `README.md` (+65行, -3行)

### 下位互換性
- すべての変更は既存の機能に対して下位互換性があります
- 既存のユーザーアカウントによるPRの処理に変更はありません

## テスト

- ワークフローのYAML構文を検証済み
- ボット処理ロジックのコードレビュー完了
- ガイドラインの内容を確認済み

## 関連するPR/Issue

- PR #3: ボットアカウント処理のエラー修正
- PR #4: 貢献ガイドラインの追加要求

## 補足

このPRは、リポジトリの保守性と開発者体験を向上させることを目的としています。ボット対応により、GitHub Copilotなどの自動化ツールとの連携が円滑になり、ガイドラインによりコードベースの一貫性が保たれます。
