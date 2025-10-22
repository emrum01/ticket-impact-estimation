# コードベース分析コマンド集

## フロントエンド分析

### コンポーネント影響分析
```bash
# 関連コンポーネントの検索とシンボル分析
mcp__serena__search_for_pattern("related_keyword", relative_path="frontend/src/components", paths_include_glob="*.{ts,tsx}")
mcp__serena__find_symbol("related_component_name", relative_path="frontend/src/components")
mcp__serena__get_symbols_overview("frontend/src/components/RelatedComponent.tsx")
```

### ページ/ルーティング影響分析
```bash
# 関連ページの検索とシンボル分析
mcp__serena__search_for_pattern("related_keyword", relative_path="frontend/src", paths_include_glob="**/pages/**/*.{ts,tsx}")
mcp__serena__search_for_pattern("related_keyword", relative_path="frontend/src", paths_include_glob="**/app/**/*.{ts,tsx}")
mcp__serena__get_symbols_overview("frontend/src/pages/RelatedPage.tsx")
```

### APIルート影響分析
```bash
# APIルートの検索とハンドラー分析
mcp__serena__find_file("*.ts", "frontend/src/pages/api")
mcp__serena__find_file("*.ts", "frontend/src/app/api")
mcp__serena__find_symbol("handler", relative_path="frontend/src/pages/api")
mcp__serena__find_symbol("GET|POST|PUT|DELETE", relative_path="frontend/src/pages/api", substring_matching=true)
```

### 状態管理・フック影響分析
```bash
# フック/ストア/コンテキストの検索とシンボル分析
mcp__serena__search_for_pattern("related_keyword", relative_path="frontend/src", paths_include_glob="**/hooks/**/*.ts")
mcp__serena__search_for_pattern("related_keyword", relative_path="frontend/src", paths_include_glob="**/store/**/*.ts")
mcp__serena__search_for_pattern("related_keyword", relative_path="frontend/src", paths_include_glob="**/context/**/*.ts")
mcp__serena__find_symbol("use*", relative_path="frontend/src/hooks", substring_matching=true)
```

## バックエンド分析

### ハンドラー影響分析
```bash
# ハンドラーの検索とシンボル分析
mcp__serena__search_for_pattern("related_keyword", relative_path="backend", paths_include_glob="**/handler/**/*.{js,ts,go,py}")
mcp__serena__search_for_pattern("related_keyword", relative_path="backend/cmd", paths_include_glob="**/*.{js,ts,go,py}")
mcp__serena__find_symbol("Handle*", relative_path="backend/internal/handler", substring_matching=true)
mcp__serena__get_symbols_overview("backend/internal/handler/RelatedHandler.go")
```

### サービス層影響分析
```bash
# サービス/ユースケース層の検索とシンボル分析
mcp__serena__search_for_pattern("related_keyword", relative_path="backend", paths_include_glob="**/service/**/*.{js,ts,go,py}")
mcp__serena__search_for_pattern("related_keyword", relative_path="backend", paths_include_glob="**/usecase/**/*.{js,ts,go,py}")
mcp__serena__find_symbol("*Service", relative_path="backend/internal/service", substring_matching=true)
mcp__serena__find_symbol("*Usecase", relative_path="backend/internal/usecase", substring_matching=true)
```

### データ層影響分析
```bash
# リポジトリ/モデルの検索とシンボル分析
mcp__serena__search_for_pattern("related_keyword", relative_path="backend", paths_include_glob="**/repository/**/*.{js,ts,go,py}")
mcp__serena__search_for_pattern("related_keyword", relative_path="backend", paths_include_glob="**/model/**/*.{js,ts,go,py}")
mcp__serena__find_symbol("*Repository", relative_path="backend/internal/repository", substring_matching=true)
mcp__serena__find_symbol("type", relative_path="backend/internal/model", substring_matching=true, include_kinds=[23]) # struct (Go) / class (other languages)
```

### スキーマ・マイグレーション影響分析
```bash
# マイグレーション/スキーマファイルの検索とシンボル分析
mcp__serena__find_file("*.sql", "backend")
mcp__serena__find_file("*migration*", "backend")
mcp__serena__search_for_pattern("related_keyword", relative_path="backend", paths_include_glob="**/*.sql")
mcp__serena__search_for_pattern("CREATE TABLE", relative_path="backend", paths_include_glob="**/*.sql")
```

## 共通・設定ファイル分析

### 型定義・インターフェース
```bash
# TypeScript型定義の検索とシンボル分析
mcp__serena__search_for_pattern("related_keyword", relative_path="frontend/src", paths_include_glob="**/types/**/*.ts")
mcp__serena__find_symbol("interface", relative_path="frontend/src/types", substring_matching=true, include_kinds=[11]) # interface
mcp__serena__find_symbol("type", relative_path="frontend/src/types", substring_matching=true, include_kinds=[26]) # type parameter

# バックエンド型定義の検索とシンボル分析（使用言語に合わせて調整）
mcp__serena__search_for_pattern("related_keyword", relative_path="backend", paths_include_glob="**/types/**/*.{js,ts,go,py}")
mcp__serena__find_symbol("type", relative_path="backend/internal/types", substring_matching=true, include_kinds=[11, 23]) # interface, struct/class

# 型参照関係の分析
mcp__serena__find_referencing_symbols("related_type_name", relative_path="frontend/src/types/RelatedTypeDefinition.ts")
```

### 設定ファイル・環境変数
```bash
# 設定ファイルの検索と分析
mcp__serena__find_file(".env*", ".")
mcp__serena__find_file("*.config.*", ".")
mcp__serena__search_for_pattern("related_config_keyword", relative_path=".", paths_include_glob="**/.env*")
mcp__serena__search_for_pattern("related_config_keyword", relative_path=".", paths_include_glob="**/*.config.*")

# 設定ファイル構造の分析
mcp__serena__get_symbols_overview("frontend/next.config.js")
mcp__serena__read_file(".env.example")
```

## プロジェクト構造理解

### 基本構造確認
```bash
# プロジェクト構造を理解
mcp__serena__list_dir(".", recursive=true, skip_ignored_files=true)

# メインフロントエンド構造を確認
mcp__serena__list_dir("frontend", recursive=false)

# メインバックエンド構造を確認
mcp__serena__list_dir("backend", recursive=false)

# 設定ファイルの存在を確認
mcp__serena__find_file("package.json", ".")
mcp__serena__find_file("requirements.txt", ".")  # Python
mcp__serena__find_file("go.mod", ".")            # Go
mcp__serena__find_file("Gemfile", ".")           # Ruby
```

## 分析品質保証

### 分析結果検証
```bash
# 分析結果の妥当性を確認
mcp__serena__think_about_collected_information()

# 見落としをチェック
mcp__serena__search_for_pattern("TODO|FIXME|BUG", relative_path=".", paths_include_glob="**/*.{ts,tsx,js,jsx,go,py,rb}")

# 追加の依存関係検証
mcp__serena__find_referencing_symbols("related_symbol", relative_path="specific_file")

# インポート/エクスポート関係をチェック
mcp__serena__search_for_pattern("import.*related_keyword|from.*related_keyword", relative_path="frontend/src")

# 分析の完全性をチェック
mcp__serena__think_about_task_adherence()

# 最終チェック
mcp__serena__think_about_whether_you_are_done()
```