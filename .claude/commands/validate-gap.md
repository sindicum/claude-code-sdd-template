# validate-gap

既存の実装コードと `docs/` 内の仕様書を比較し、ギャップ（未実装・仕様逸脱）を検出する。

## 目的

- 仕様書で定義された要件が実装されているか確認
- 実装が仕様から逸脱していないか検出
- 未実装の機能を可視化

## 実行フロー

### Step 1: 仕様書の読み込み

```
Read("docs/product-requirements.md")
Read("docs/functional-design.md")
```

要件リストを抽出する。

### Step 2: 実装コードのスキャン

```
Glob("src/**/*.{ts,tsx,js,jsx}")
Glob("app/**/*.{ts,tsx,js,jsx}")
```

実装されている機能を特定する。

### Step 3: implementation-validator サブエージェントの起動

ギャップ分析に特化したプロンプトで起動:

```
Task(subagent_type="implementation-validator", prompt="
仕様書と実装コードを比較し、以下を分析してください:

1. PRD の各要件について:
   - 実装済み / 部分実装 / 未実装 を判定
   - 実装箇所のファイルパスを特定

2. 仕様逸脱の検出:
   - 仕様と異なる動作をしている箇所
   - 仕様にない機能が追加されている箇所

3. 優先度の判定:
   - P0（必須）要件の実装状況を優先的に確認
")
```

### Step 4: 結果の出力

以下の形式でコンソールに出力:

```
🔍 実装ギャップ分析

📄 対象仕様書:
  - product-requirements.md
  - functional-design.md

📁 対象実装:
  - src/
  - app/

📊 PRD要件との比較:

  ✅ 実装済み: 12/15
  ⏳ 部分実装: 2/15
  ❌ 未実装: 1/15

📋 詳細:

### 実装済み
  ✅ [要件1] → src/components/Feature1.tsx
  ✅ [要件2] → src/lib/utils.ts
  ...

### 部分実装
  ⏳ [要件3]: エラーハンドリングが未実装
     → src/api/handler.ts:45
  ⏳ [要件4]: バリデーションが一部不足
     → src/components/Form.tsx:120

### 未実装
  ❌ [要件5]: 該当する実装なし

⚠️ 仕様逸脱: 1件
  - src/lib/calc.ts:30 - 計算ロジックが仕様と異なる
    仕様: [仕様の内容]
    実装: [実際の動作]

📋 推奨アクション:
  1. [P0] [要件5] の実装を優先
  2. [P1] [要件3] のエラーハンドリング追加
  3. [P1] src/lib/calc.ts の仕様逸脱を修正
```

## 実装コードが存在しない場合

```
📁 実装コードが見つかりません。

💡 以下のディレクトリにコードを配置してください:
  - src/
  - app/

または /add-feature で機能実装を開始してください。
```

## 使用ツール

- Glob: ファイル検索
- Read: 仕様書・コードの読み込み
- Grep: 特定パターンの検索
- Task (implementation-validator): ギャップ分析
