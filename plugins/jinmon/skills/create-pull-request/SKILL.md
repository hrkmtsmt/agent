---
name: create-pull-request
description: PRを作成し、仕様ファイルのステータスを更新するスキル
context: fork
---

# Create Pull Request

PRを作成し、仕様ファイルのステータスを更新するスキル

## いつ使うか

- jinmonのステップ5として呼ばれるとき
- 「PRを作って」と指示されたとき

## 実行手順

### 1. PRを作成する

`gh` コマンドでPRを作成すること。

1. PRテンプレートを決定する
   - プロジェクトに `.github/PULL_REQUEST_TEMPLATE.md` があればそれを使う
   - なければ [@PULL_REQUEST_TEMPLATE.md](./PULL_REQUEST_TEMPLATE.md) を使う
2. テンプレートに仕様ファイル(`$ARGUMENTS`で渡されたパス)の内容を埋め込む
3. 埋め込んだ内容でPRを作成する

```bash
gh pr create --title "<機能名>" --body "$(cat <<'EOF'
<埋め込み済みのPR本文>
EOF
)"
```

### 2. 仕様ファイルのステータスを更新する

PR作成後、仕様ファイルの先頭フロントマターを更新する。

```markdown
---
status: implemented
pr: <PRのURL>
---
```

### 3. 完了報告

PRのURLを人間に伝えて終了する。

## 参照するルール

- [../../rules/pull-request.md](../../rules/pull-request.md)
