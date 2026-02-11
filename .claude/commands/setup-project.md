---
description: 初回セットアップ: 6つの永続ドキュメントを対話的に作成する
---

# 初回プロジェクトセットアップ

このコマンドは、プロジェクトの6つの永続ドキュメントを対話的に作成します。

## 実行方法

```bash
claude
> /setup-project
```

## 前提条件

`docs/ideas/` に要件整理ファイルが必要です。

```bash
# 確認
ls docs/ideas/

# ファイルが存在する場合 → セットアップ続行
✅ docs/ideas/initial-requirement.md が見つかりました
   この内容を元にPRDを作成します

# ファイルが存在しない場合 → セットアップ中断
⚠️  docs/ideas/ にファイルがありません
   先に要件整理を行ってください:
   「アイデアを整理したい」「壁打ちしたい」と伝えてください
   → create-initial-requirement スキルで docs/ideas/initial-requirement.md を作成後、
     再度 /setup-project を実行してください
```

**`docs/ideas/` にファイルがない場合は、このコマンドを中断してください。**

## 手順

### ステップ0: インプットの読み込み

1. `docs/ideas/` 内のマークダウンファイルを全て読む
2. 内容を理解し、PRD作成の参考にする

### ステップ1: プロダクト要求定義書の作成

1. **prd-writingスキル**をロード
2. `docs/ideas/`の内容（create-initial-requirement スキルの出力）を元に`docs/product-requirements.md`を作成
3. 要件サマリーを正式なPRDに変換：
   - プロダクトの概要と目的
   - 前提条件・制約条件
   - 機能要件（MVP/将来、優先度P0-P2）
   - 非機能要件
   - スコープ外
4. ユーザーに確認を求め、**承認されるまで待機**

**以降のステップはプロダクト要求定義書の内容を元にするため、自動的に作成する**

### ステップ2: アーキテクチャ設計書の作成

1. **architecture-designスキル**をロード
2. `docs/product-requirements.md`を読む
3. スキルのテンプレートとガイドに従って`docs/architecture.md`を作成

### ステップ3: 機能設計書の作成

1. **functional-designスキル**をロード
2. `docs/product-requirements.md`と`docs/architecture.md`を読む
3. スキルのテンプレートとガイドに従って`docs/functional-design.md`を作成

### ステップ4: リポジトリ構造定義書の作成

1. **repository-structureスキル**をロード
2. 既存のドキュメントを読む
3. スキルのテンプレートに従って`docs/repository-structure.md`を作成

### ステップ5: 開発ガイドラインの作成

1. **development-guidelinesスキル**をロード
2. 既存のドキュメントを読む
3. スキルのテンプレートに従って`docs/development-guidelines.md`を作成

### ステップ6: 用語集の作成

1. **glossary-creationスキル**をロード
2. 既存のドキュメントを読む
3. スキルのテンプレートに従って`docs/glossary.md`を作成

## 完了条件

- 6つの永続ドキュメントが全て作成されていること

完了時のメッセージ:
```
「初回セットアップが完了しました!

作成したドキュメント:
✅ docs/product-requirements.md
✅ docs/architecture.md
✅ docs/functional-design.md
✅ docs/repository-structure.md
✅ docs/development-guidelines.md
✅ docs/glossary.md

これで開発を開始する準備が整いました。

今後の使い方:
- ドキュメントの編集: 普通に会話で依頼してください
  例: 「PRDに新機能を追加して」「architecture.mdを見直して」

- 機能の追加: /add-feature [機能名] を実行してください
  例: /add-feature ユーザー認証

- ドキュメントレビュー: /review-docs [パス] を実行してください
  例: /review-docs docs/product-requirements.md
」
```