# チケット影響分析・工数見積もりツール

Notionチケットを分析してコードベースへの影響範囲を特定し、実装工数（2,4,8,12,16時間）を自動見積もりするAIプロンプト集です。

## 🏗️ システム構成

```
ticket-impact-analysis-with-estimation/
├── prompts/
│   ├── ticket-impact-analysis-with-estimation.md  # メインプロンプトテンプレート
│   ├── estimation-criteria.md                     # 工数見積もり基準定義
│   ├── analysis-commands.md                       # コードベース分析コマンド集
│   ├── notion-page-template.md                    # レポート出力テンプレート
│   └── internal-json-schema.json                  # 内部データ構造定義
├── examples/                                       # 見積もり作成例
│   ├── example-2hours-ui-fix.md                   # 2時間例（UI修正）
│   ├── example-8hours-feature-add.md              # 8時間例（機能追加）
│   ├── example-16hours-architecture-change.md     # 16時間例（大規模変更）
│   └── README.md                                   # 例の説明
└── README.md                                       # 本ドキュメント
```

## 📄 ファイル構成

- **`ticket-impact-analysis-with-estimation.md`**: メインプロンプト（6段階分析プロセス）
- **`estimation-criteria.md`**: 工数見積もり基準（2-16時間の範囲定義）
- **`analysis-commands.md`**: コードベース分析コマンド集
- **`notion-page-template.md`**: レポート出力テンプレート
- **`internal-json-schema.json`**: データ構造定義

## 🚀 使用方法

1. `prompts/ticket-impact-analysis-with-estimation.md` をAIアシスタントに読み込み
2. NotionチケットURLを指定して分析実行
3. 自動生成されたNotionサブページで結果確認

## 🎯 対象

フルスタックWebアプリケーション（React/Vue + Node.js/Go/Python等）

## 🔧 前提条件

- Notion API アクセス権限
- AIアシスタント（Claude、ChatGPT等）
- 構造化されたコードベース

## 📚 作成例

異なる複雑度レベルの実際の見積もり例を [examples/](examples/) ディレクトリに収録しています：

- **2時間例**: UI修正（ボタンスタイル変更）
- **8時間例**: 機能追加（プロフィール画像アップロード）
- **16時間例**: アーキテクチャ変更（リアルタイム通知システム）

---

**作成者**: h_iwakubo | **ライセンス**: MIT | **リポジトリ**: [ticket-impact-estimation](https://github.com/emrum01/ticket-impact-estimation)