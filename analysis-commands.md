# Codebase Analysis Command Collection

## Frontend Analysis

### Component Impact Analysis
```bash
# Search and symbol analysis for related components
mcp__serena__search_for_pattern("related_keyword", relative_path="frontend/src/components", paths_include_glob="*.{ts,tsx}")
mcp__serena__find_symbol("related_component_name", relative_path="frontend/src/components")
mcp__serena__get_symbols_overview("frontend/src/components/RelatedComponent.tsx")
```

### Page/Routing Impact Analysis
```bash
# Search and symbol analysis for related pages
mcp__serena__search_for_pattern("related_keyword", relative_path="frontend/src", paths_include_glob="**/pages/**/*.{ts,tsx}")
mcp__serena__search_for_pattern("related_keyword", relative_path="frontend/src", paths_include_glob="**/app/**/*.{ts,tsx}")
mcp__serena__get_symbols_overview("frontend/src/pages/RelatedPage.tsx")
```

### API Routes Impact Analysis
```bash
# Search API routes and handler analysis
mcp__serena__find_file("*.ts", "frontend/src/pages/api")
mcp__serena__find_file("*.ts", "frontend/src/app/api")
mcp__serena__find_symbol("handler", relative_path="frontend/src/pages/api")
mcp__serena__find_symbol("GET|POST|PUT|DELETE", relative_path="frontend/src/pages/api", substring_matching=true)
```

### State Management & Hooks Impact Analysis
```bash
# Search hooks/store/context and symbol analysis
mcp__serena__search_for_pattern("related_keyword", relative_path="frontend/src", paths_include_glob="**/hooks/**/*.ts")
mcp__serena__search_for_pattern("related_keyword", relative_path="frontend/src", paths_include_glob="**/store/**/*.ts")
mcp__serena__search_for_pattern("related_keyword", relative_path="frontend/src", paths_include_glob="**/context/**/*.ts")
mcp__serena__find_symbol("use*", relative_path="frontend/src/hooks", substring_matching=true)
```

## Backend Analysis

### Handler Impact Analysis
```bash
# Search handlers and symbol analysis
mcp__serena__search_for_pattern("related_keyword", relative_path="backend", paths_include_glob="**/handler/**/*.{js,ts,go,py}")
mcp__serena__search_for_pattern("related_keyword", relative_path="backend/cmd", paths_include_glob="**/*.{js,ts,go,py}")
mcp__serena__find_symbol("Handle*", relative_path="backend/internal/handler", substring_matching=true)
mcp__serena__get_symbols_overview("backend/internal/handler/RelatedHandler.go")
```

### Service Layer Impact Analysis
```bash
# Search service/usecase layer and symbol analysis
mcp__serena__search_for_pattern("related_keyword", relative_path="backend", paths_include_glob="**/service/**/*.{js,ts,go,py}")
mcp__serena__search_for_pattern("related_keyword", relative_path="backend", paths_include_glob="**/usecase/**/*.{js,ts,go,py}")
mcp__serena__find_symbol("*Service", relative_path="backend/internal/service", substring_matching=true)
mcp__serena__find_symbol("*Usecase", relative_path="backend/internal/usecase", substring_matching=true)
```

### Data Layer Impact Analysis
```bash
# Search repository/model and symbol analysis
mcp__serena__search_for_pattern("related_keyword", relative_path="backend", paths_include_glob="**/repository/**/*.{js,ts,go,py}")
mcp__serena__search_for_pattern("related_keyword", relative_path="backend", paths_include_glob="**/model/**/*.{js,ts,go,py}")
mcp__serena__find_symbol("*Repository", relative_path="backend/internal/repository", substring_matching=true)
mcp__serena__find_symbol("type", relative_path="backend/internal/model", substring_matching=true, include_kinds=[23]) # struct (Go) / class (other languages)
```

### Schema & Migration Impact Analysis
```bash
# Search migration/schema files and symbol analysis
mcp__serena__find_file("*.sql", "backend")
mcp__serena__find_file("*migration*", "backend")
mcp__serena__search_for_pattern("related_keyword", relative_path="backend", paths_include_glob="**/*.sql")
mcp__serena__search_for_pattern("CREATE TABLE", relative_path="backend", paths_include_glob="**/*.sql")
```

## Common & Configuration File Analysis

### Type Definitions & Interfaces
```bash
# Search TypeScript type definitions and symbol analysis
mcp__serena__search_for_pattern("related_keyword", relative_path="frontend/src", paths_include_glob="**/types/**/*.ts")
mcp__serena__find_symbol("interface", relative_path="frontend/src/types", substring_matching=true, include_kinds=[11]) # interface
mcp__serena__find_symbol("type", relative_path="frontend/src/types", substring_matching=true, include_kinds=[26]) # type parameter

# Search backend type definitions and symbol analysis (adapt for your language)
mcp__serena__search_for_pattern("related_keyword", relative_path="backend", paths_include_glob="**/types/**/*.{js,ts,go,py}")
mcp__serena__find_symbol("type", relative_path="backend/internal/types", substring_matching=true, include_kinds=[11, 23]) # interface, struct/class

# Analyze type reference relationships
mcp__serena__find_referencing_symbols("related_type_name", relative_path="frontend/src/types/RelatedTypeDefinition.ts")
```

### Configuration Files & Environment Variables
```bash
# Search configuration files and analysis
mcp__serena__find_file(".env*", ".")
mcp__serena__find_file("*.config.*", ".")
mcp__serena__search_for_pattern("related_config_keyword", relative_path=".", paths_include_glob="**/.env*")
mcp__serena__search_for_pattern("related_config_keyword", relative_path=".", paths_include_glob="**/*.config.*")

# Analyze configuration file structure
mcp__serena__get_symbols_overview("frontend/next.config.js")
mcp__serena__read_file(".env.example")
```

## Project Structure Understanding

### Basic Structure Confirmation
```bash
# Understand project structure
mcp__serena__list_dir(".", recursive=true, skip_ignored_files=true)

# Check main frontend structure
mcp__serena__list_dir("frontend", recursive=false)

# Check main backend structure
mcp__serena__list_dir("backend", recursive=false)

# Confirm configuration files exist
mcp__serena__find_file("package.json", ".")
mcp__serena__find_file("requirements.txt", ".")  # Python
mcp__serena__find_file("go.mod", ".")            # Go
mcp__serena__find_file("Gemfile", ".")           # Ruby
```

## Analysis Quality Assurance

### Analysis Result Verification
```bash
# Check analysis result validity
mcp__serena__think_about_collected_information()

# Check for oversights
mcp__serena__search_for_pattern("TODO|FIXME|BUG", relative_path=".", paths_include_glob="**/*.{ts,tsx,js,jsx,go,py,rb}")

# Additional dependency verification
mcp__serena__find_referencing_symbols("related_symbol", relative_path="specific_file")

# Check import/export relationships
mcp__serena__search_for_pattern("import.*related_keyword|from.*related_keyword", relative_path="frontend/src")

# Check analysis completeness
mcp__serena__think_about_task_adherence()

# Final check
mcp__serena__think_about_whether_you_are_done()
```