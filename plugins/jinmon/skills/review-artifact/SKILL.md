---
name: review-artifact
description: コードレビューとセキュリティレビューをサブエージェントで実行し、合否を判定するスキル
context: fork
---

## いつ使うか

- `/jinmon`skillのステップ3として呼ばれるとき
- 「レビューして」と指示されたとき

## 実行手順

### 0. 仕様ファイルを確認する

`$ARGUMENTS` で渡された仕様ファイルのパスを読み込む。

### 1. レビューを実行する

**サブエージェントを明示的に起動して**以下を順に実行する。

```
/code-review
/security-review
```

### 2. 合否を判定する

**OKの条件(全て満たすこと):**

- [ ] 実装内容がステップ0で読み込んだ仕様ファイルの受け入れ要件を全て満たしている
- [ ] [coding-philosophy.md](../../rules/coding-philosophy.md) の規約違反がゼロ
- [ ] `security-review` で指摘事項がゼロ

### 3. 結果に応じて対応する

**OKの場合:** 完了を報告して終了する。

**NGの場合:**

修正方針が明確な場合(コーディング規約違反・セキュリティ指摘など):
1. 実装を修正する
2. `/code-review` と `/security-review` を再実行する
3. 全てOKになったら完了を報告して終了する

修正方針が不明な場合(仕様の解釈が割れる・設計の判断が必要など):
→ [escalation-policy.md](../../rules/escalation-policy.md) に従い人間に確認してから修正する
