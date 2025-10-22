---
title: チケット影響分析・工数見積もりプロンプトテンプレート
description: Notionチケットを分析し、フロントエンド/バックエンドコードベースの影響分析に基づいて実装時間（2,4,8,12,16時間）を見積もる
version: 1.0.0
created: 2025-01-17
allowed-tools: ["Read", "Glob", "Grep", "mcp__notionApi__*", "mcp__serena__read_file", "mcp__serena__list_dir", "mcp__serena__find_file", "mcp__serena__search_for_pattern", "mcp__serena__get_symbols_overview", "mcp__serena__find_symbol", "mcp__serena__find_referencing_symbols", "mcp__serena__think_about_*", "TodoWrite", "WebFetch"]
argument-hint: "<notion-ticket-url>"
---

# チケット影響分析・工数見積もりプロンプトテンプレート

## 目的
Notionチケットを分析し、フロントエンド/バックエンドコードベースの影響分析に基づいて実装工数を時間単位（2,4,8,12,16時間）で見積もる

## 前提条件
- 利用可能ツール: Notion API、ファイル検索・分析ツール、コード分析ツール
- 分析範囲: フロントエンドとバックエンドディレクトリ（必要に応じてパスを適応）
- 見積もり範囲: 2,4,8,12,16時間
- 対象コードベース: フルスタックWebアプリケーション（任意のスタックに適応可能）

## 役割定義
技術影響分析と工数見積もりの専門家として、以下の観点から分析を行う:
- 機能要件を技術実装要件に変換
- コードベースへの影響範囲を特定
- 実装の複雑性を評価
- 工数見積もりを算出

## 実行ステップ

### フェーズ1: Notion MCPによるチケット情報取得・分析
- 引数として提供されたNotionチケットURLから情報を取得
- Notion APIを使用して詳細なチケット内容を取得・分析
- 機能概要、技術要件、ビジネス要件、仕様詳細を抽出
- UI/UX要件、API要件、データ構造変更要件を特定

### フェーズ2: コードベース構造理解
基本的なプロジェクト構造を理解するために以下のコマンドを使用:
（詳細は [analysis-commands.md](./analysis-commands.md) を参照）

```bash
# プロジェクト構造を理解
mcp__serena__list_dir(".", recursive=true, skip_ignored_files=true)
# メインのフロントエンド/バックエンド構造を確認
mcp__serena__list_dir("frontend", recursive=false)  # 必要に応じてパスを調整
mcp__serena__list_dir("backend", recursive=false)   # 必要に応じてパスを調整
```

### フェーズ3: 影響範囲特定

#### 3.1 フロントエンド影響分析
コンポーネント、ページ、APIルート、状態管理への影響を調査。
詳細なコマンド例は [analysis-commands.md](./analysis-commands.md) を参照。

#### 3.2 バックエンド影響分析
ハンドラー、サービス層、データ層、スキーマ変更への影響を調査。
詳細なコマンド例は [analysis-commands.md](./analysis-commands.md) を参照。

#### 3.3 共通・設定ファイル影響分析
型定義、インターフェース、設定ファイル、環境変数への影響を調査。
詳細なコマンド例は [analysis-commands.md](./analysis-commands.md) を参照。

### フェーズ4: 実装複雑性評価

#### 4.1 技術的複雑性指標
- **新規作成 vs 既存修正の比率**
- **依存関係の複雑性**
- **データ構造変更の有無**
- **外部API統合の必要性**
- **認証・認可への影響**
- **必要なテストコードの範囲**

#### 4.2 実装パターン分析
- **CRUD操作の完全性**
- **バリデーション・エラーハンドリングの複雑性**
- **UI/UX実装の複雑性**
- **パフォーマンス要件**
- **セキュリティ要件**

### フェーズ5: 工数見積もり算出

[estimation-criteria.md](./estimation-criteria.md) の基準に従って工数見積もりを算出。

## エラーハンドリング
- API取得失敗: `{"error": "API_FETCH_FAILED", "message": "詳細メッセージ"}`
- ファイル検索失敗: `{"error": "FILE_SEARCH_FAILED", "message": "詳細メッセージ"}`
- コード分析失敗: `{"error": "CODE_ANALYSIS_FAILED", "message": "詳細メッセージ"}`
- 軽微なエラーに対して1回再試行

## 出力規則

### 分析結果（内部JSON）
分析処理は [internal-json-schema.json](./internal-json-schema.json) 構造を使用して結果を管理し、マークダウンレポート生成時に参照。

### 影響評価基準
- **影響あり**: いずれかのaffected_*配列またはnew_files_needed配列にアイテムがある場合
- **影響なし**: 関連するすべての配列が空の場合
- **確認要**: has_impactがnullまたはundefinedの場合

### 分析結果反復最適化
分析結果の品質向上のため、[analysis-commands.md](./analysis-commands.md) の「分析品質保証」セクションの最適化プロセスを実行。

### フェーズ6: 結果出力

#### 6.1 Notionサブページ作成
- 元のNotionチケット末尾に「AI分析結果」タイトルのサブページを作成
- サブページに分析結果をNotionマークダウン形式で出力
- チケットと自動リンクして管理を容易化
- **サブページ作成完了後、生成されたNotionページURLを出力**

#### 6.2 レポート内容構造
- **概要**: チケットサマリーと見積もり時間
- **影響ファイル一覧**: 変更/新規作成が必要なファイルをパス付きで列挙
- **実装ステップ**: フェーズ別の詳細タスク
- **チェックリスト**: 完了確認項目

## 出力形式

### 6.3 Notionサブページ作成実装手順

#### ステップ1: チケットページIDを取得
```bash
# NotionチケットURLからページIDを抽出
ticket_page_id = extract_page_id_from_url(ticket_url)
```

#### ステップ2: サブページを作成
```bash
# mcp__notionApi__notion-create-pagesを使用してサブページ作成
mcp__notionApi__notion-create-pages({
  "parent": {"page_id": ticket_page_id},
  "pages": [{
    "properties": {"title": "AI分析結果"},
    "content": notion_formatted_analysis_content
  }]
})
```

#### ステップ3: 分析結果をNotion形式に変換
- マークダウンをNotionマークダウン形式に変換
- コードブロック、テーブル、リストを適切にフォーマット
- ファイルパスをコード形式で表示

### レポートテンプレート

#### Notion用
[notion-page-template.md](./notion-page-template.md) を使用してNotionサブページを生成。

## 開始メッセージ
Notionチケット影響分析と工数見積もりを開始します。
コードベースを分析し、2,4,8,12,16時間のオプションで見積もりします。

**使用方法:**
分析対象としてNotionチケットURLを引数として提供してください。

**出力形式:**
- **Notionサブページ**: チケット末尾に「AI分析結果」ページを自動作成

## 終了メッセージ
チケット影響分析が完了しました。
元のNotionチケット内に詳細な分析レポートと「AI分析結果」サブページを作成しました。

**作成されたサブページ**: [生成されたURL]

分析結果をご確認いただき、実装計画にご活用ください。

## ファイル構造
```
ticket-impact-analysis-with-estimation/
├── ticket-impact-analysis-with-estimation.md  # メインプロンプトファイル
├── internal-json-schema.json                  # 内部JSON構造定義
├── notion-page-template.md                    # Notionページテンプレート
├── estimation-criteria.md                     # 工数見積もり基準
└── analysis-commands.md                       # 分析コマンド集
```