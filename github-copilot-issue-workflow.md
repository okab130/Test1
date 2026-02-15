# GitHub Copilot Issueを使ったシステム開発手順

このドキュメントでは、GitHub Copilotを活用してIssueベースでシステム開発を進める手順を説明します。

## 概要

GitHub Copilotは、Issueを通じて自然言語でタスクを指示することで、コード生成、バグ修正、機能追加などを自動化できるAI開発支援ツールです。

## 前提条件

- GitHubアカウントを持っていること
- GitHub Copilotのサブスクリプションがアクティブであること
- リポジトリへの適切なアクセス権限があること

## 基本的な開発フロー

### 1. リポジトリの作成

```bash
# GitHubで新しいリポジトリを作成
# または既存のリポジトリを使用
```

1. GitHub.comにアクセス
2. 右上の「+」ボタンから「New repository」を選択
3. リポジトリ名、説明、公開/非公開を設定
4. 「Create repository」をクリック

### 2. 初期設定

```bash
# ローカルにクローン
git clone https://github.com/your-username/your-repo.git
cd your-repo

# 基本的なファイル構造を作成
# README.md, .gitignore などを追加
```

### 3. Issueの作成

開発したい機能や修正したいバグについて、Issueを作成します。

#### Issueの作成手順

1. リポジトリの「Issues」タブをクリック
2. 「New issue」ボタンをクリック
3. タイトルと説明を入力
4. `@copilot` をメンション（Issue本文またはコメントで）

#### Issue作成のベストプラクティス

```markdown
## タイトル例
- ユーザー認証機能の実装
- データベース接続エラーの修正
- RESTful APIエンドポイントの追加

## 説明文の書き方
@copilot

### 目的
[何を実現したいか明確に記述]

### 要件
- 機能要件1
- 機能要件2
- 非機能要件

### 技術スタック
- 使用する言語/フレームワーク
- データベース
- その他のツール

### 期待される成果物
- 実装されるファイル
- テストコード
- ドキュメント更新
```

### 4. GitHub Copilotによる自動実装

Issueに `@copilot` をメンションすると、Copilotが以下の処理を行います：

1. **要件の分析**: Issueの内容を理解
2. **コードの生成**: 必要なコードを自動生成
3. **プルリクエストの作成**: 変更を含むPRを自動作成
4. **テストの実行**: 自動テストを実行（設定されている場合）

#### Copilotへの指示の仕方

```markdown
@copilot

以下の機能を実装してください：
1. ユーザー登録API（POST /api/users）
2. バリデーション機能
3. ユニットテスト

言語: Python (Flask)
データベース: PostgreSQL
```

### 5. プルリクエストのレビュー

Copilotが作成したPRを確認します。

#### レビューのポイント

1. **コードの品質**
   - コーディング規約への準拠
   - エラーハンドリングの適切性
   - セキュリティの考慮

2. **テストの網羅性**
   - ユニットテストの存在
   - テストカバレッジ
   - エッジケースの考慮

3. **ドキュメント**
   - コメントの適切性
   - READMEの更新
   - API仕様書の更新

### 6. フィードバックと修正

問題がある場合は、PRのコメント欄でCopilotに追加の指示を出します。

```markdown
@copilot

以下の点を修正してください：
- エラーハンドリングを追加
- ログ出力を改善
- 変数名をより明確に
```

### 7. マージとデプロイ

レビューが完了したら、PRをマージします。

```bash
# PRがマージされた後
git checkout main
git pull origin main
```

## 高度な使い方

### 複数のIssueによる段階的開発

大きな機能は、複数の小さなIssueに分割します。

```
Epic Issue: ユーザー管理システムの構築
├── Issue #1: データベーススキーマの設計
├── Issue #2: ユーザー登録機能
├── Issue #3: ログイン機能
├── Issue #4: プロフィール編集機能
└── Issue #5: パスワードリセット機能
```

### Issueテンプレートの活用

`.github/ISSUE_TEMPLATE/` にテンプレートを作成：

```markdown
---
name: 機能実装リクエスト
about: 新機能の実装をCopilotに依頼
title: '[FEATURE] '
labels: enhancement
assignees: ''
---

@copilot

## 機能概要
[機能の説明]

## 要件
- [ ] 要件1
- [ ] 要件2

## 技術仕様
- 言語:
- フレームワーク:
- データベース:

## 参考資料
- [関連ドキュメントへのリンク]
```

### ラベルとマイルストーンの活用

- **ラベル**: `bug`, `enhancement`, `documentation`, `copilot`
- **マイルストーン**: リリースバージョンごとに整理
- **プロジェクトボード**: 進捗管理

## トラブルシューティング

### Copilotが応答しない場合

1. `@copilot` のメンションが正しいか確認
2. Issue説明が十分に詳細か確認
3. リポジトリの権限設定を確認

### 生成されたコードが期待と異なる場合

1. より詳細な指示を追加
2. サンプルコードを提供
3. 既存のコードスタイルを参照するよう指示

### エラーが発生した場合

```markdown
@copilot

以下のエラーが発生しています：
```
[エラーメッセージ]
```

原因を調査して修正してください。
```

## ベストプラクティス

### 1. 明確な指示を出す
- 曖昧な表現を避ける
- 具体的な要件を箇条書きで記載
- 技術スタックを明示

### 2. 小さく始める
- 最初は小さなタスクから試す
- 段階的に複雑な機能を追加
- 各Issueは単一の責任に焦点を当てる

### 3. レビューを怠らない
- Copilotが生成したコードも人間がレビュー
- セキュリティとパフォーマンスを確認
- チーム内でコードレビュープロセスを確立

### 4. ドキュメントを維持
- Issueで議論した内容を記録
- 設計判断の理由を残す
- READMEを常に最新に保つ

### 5. テストを重視
- Copilotにテストコードも生成させる
- CI/CDパイプラインを設定
- 自動テストを実行

## ワークフロー例

### 実際の開発シナリオ

#### ステップ1: 新機能のIssue作成

```markdown
Title: RESTful APIエンドポイントの追加

@copilot

Node.js + Expressで商品管理のCRUD APIを実装してください。

## エンドポイント
- GET /api/products - 全商品取得
- GET /api/products/:id - 特定商品取得
- POST /api/products - 商品作成
- PUT /api/products/:id - 商品更新
- DELETE /api/products/:id - 商品削除

## 要件
- MongoDBをデータベースとして使用
- 入力バリデーションを実装
- エラーハンドリングを適切に実装
- Jestでテストコードを作成

## ファイル構成
src/
  routes/
    products.js
  controllers/
    productController.js
  models/
    Product.js
  __tests__/
    products.test.js
```

#### ステップ2: Copilotによる実装

Copilotが自動的に：
1. 必要なファイルを作成
2. コードを生成
3. テストを作成
4. PRを作成

#### ステップ3: レビューとフィードバック

PRコメントで：
```markdown
@copilot

良い実装です！以下の点を追加してください：
- プロダクトの在庫数チェック
- 削除時のソフトデリート実装
```

#### ステップ4: マージとクローズ

- PRを承認
- mainブランチにマージ
- Issueが自動的にクローズ

## まとめ

GitHub Copilot Issueを使った開発フローは：

1. **効率的**: 繰り返し作業を自動化
2. **一貫性**: コーディング標準を維持
3. **透明性**: 変更履歴がIssueとPRに記録
4. **学習機会**: Copilotが生成するコードから学習

この手順に従うことで、チーム開発の生産性を大幅に向上させることができます。

## 参考リンク

- [GitHub Copilot Documentation](https://docs.github.com/en/copilot)
- [GitHub Issues Guide](https://docs.github.com/en/issues)
- [GitHub Pull Requests](https://docs.github.com/en/pull-requests)
- [GitHub Actions for CI/CD](https://docs.github.com/en/actions)

---

最終更新日: 2026-02-15
