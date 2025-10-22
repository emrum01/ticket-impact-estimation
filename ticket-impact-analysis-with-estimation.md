---
title: Ticket Impact Analysis & Time Estimation Prompt Template
description: Analyze input Notion tickets and estimate implementation time (2,4,8,12,16 hours) based on impact analysis of frontend/backend codebase
version: 1.0.0
created: 2025-01-17
allowed-tools: ["Read", "Glob", "Grep", "mcp__notionApi__*", "mcp__serena__read_file", "mcp__serena__list_dir", "mcp__serena__find_file", "mcp__serena__search_for_pattern", "mcp__serena__get_symbols_overview", "mcp__serena__find_symbol", "mcp__serena__find_referencing_symbols", "mcp__serena__think_about_*", "TodoWrite", "WebFetch"]
argument-hint: "<notion-ticket-url>"
---

# Ticket Impact Analysis & Time Estimation Prompt Template

## Purpose
Analyze input Notion tickets and estimate implementation effort in hours (2,4,8,12,16 hours) based on impact analysis of frontend/backend codebase

## Prerequisites
- Available Tools: Notion API, File search & analysis tools, Code analysis tools
- Analysis Scope: Frontend and backend directories (adapt paths as needed)
- Estimation Range: 2,4,8,12,16 hours
- Target Codebase: Full-stack web application (adaptable to any stack)

## Role Definition
Act as a technical impact analysis and effort estimation expert, analyzing from these perspectives:
- Convert functional requirements to technical implementation requirements
- Identify impact scope on codebase
- Evaluate implementation complexity
- Calculate effort estimation

## Execution Steps

### Phase 1: Notion MCP for Ticket Information Retrieval & Analysis
- Retrieve information from Notion ticket URL provided as argument
- Use Notion API to fetch and analyze detailed ticket content
- Extract functional overview, technical requirements, business requirements, specification details
- Identify UI/UX requirements, API requirements, data structure change requirements

### Phase 2: Codebase Structure Understanding
Use these commands to understand basic project structure:
(See [analysis-commands.md](./analysis-commands.md) for details)

```bash
# Understand project structure
mcp__serena__list_dir(".", recursive=true, skip_ignored_files=true)
# Check main frontend/backend structure
mcp__serena__list_dir("frontend", recursive=false)  # adjust path as needed
mcp__serena__list_dir("backend", recursive=false)   # adjust path as needed
```

### Phase 3: Impact Scope Identification

#### 3.1 Frontend Impact Analysis
Investigate impact on components, pages, API routes, and state management.
See [analysis-commands.md](./analysis-commands.md) for detailed command examples.

#### 3.2 Backend Impact Analysis
Investigate impact on handlers, service layer, data layer, and schema changes.
See [analysis-commands.md](./analysis-commands.md) for detailed command examples.

#### 3.3 Common & Configuration File Impact Analysis
Investigate impact on type definitions, interfaces, configuration files, and environment variables.
See [analysis-commands.md](./analysis-commands.md) for detailed command examples.

### Phase 4: Implementation Complexity Evaluation

#### 4.1 Technical Complexity Indicators
- **New creation vs existing modification ratio**
- **Dependency complexity**
- **Data structure changes presence**
- **External API integration necessity**
- **Authentication/authorization impact**
- **Required test code scope**

#### 4.2 Implementation Pattern Analysis
- **CRUD operation completeness**
- **Validation & error handling complexity**
- **UI/UX implementation complexity**
- **Performance requirements**
- **Security requirements**

### Phase 5: Effort Estimation Calculation

Calculate effort estimation according to criteria in [estimation-criteria.md](./estimation-criteria.md).

## Error Handling
- API fetch failure: `{"error": "API_FETCH_FAILED", "message": "detail message"}`
- File search failure: `{"error": "FILE_SEARCH_FAILED", "message": "detail message"}`
- Code analysis failure: `{"error": "CODE_ANALYSIS_FAILED", "message": "detail message"}`
- Retry once for minor errors

## Output Rules

### Analysis Results (Internal JSON)
Analysis processing manages results using [internal-json-schema.json](./internal-json-schema.json) structure, referenced during markdown report generation.

### Impact Assessment Criteria
- **Has Impact**: When any affected_* array or new_files_needed array has items
- **No Impact**: When all related arrays are empty
- **Needs Confirmation**: When has_impact is null or undefined

### Analysis Result Iterative Optimization
Execute optimization process from "Analysis Quality Assurance" section in [analysis-commands.md](./analysis-commands.md) to improve analysis result quality.

### Phase 6: Result Output

#### 6.1 Notion Subpage Creation
- Create "AI Analysis Results" titled subpage at end of original Notion ticket
- Output analysis results in Notion markdown format to subpage
- Automatically link to ticket for easy management
- **Output generated Notion page URL after subpage creation completion**

#### 6.2 Report Content Structure
- **Overview**: Ticket summary and estimated time
- **Affected Files List**: Enumerate files needing changes/new creation with paths
- **Implementation Steps**: Detailed tasks by phase
- **Checklist**: Completion confirmation items

## Output Format

### 6.3 Notion Subpage Creation Implementation Steps

#### Step 1: Get Ticket Page ID
```bash
# Extract page ID from Notion ticket URL
ticket_page_id = extract_page_id_from_url(ticket_url)
```

#### Step 2: Create Subpage
```bash
# Use mcp__notionApi__notion-create-pages to create subpage
mcp__notionApi__notion-create-pages({
  "parent": {"page_id": ticket_page_id},
  "pages": [{
    "properties": {"title": "AI Analysis Results"},
    "content": notion_formatted_analysis_content
  }]
})
```

#### Step 3: Convert Analysis Results to Notion Format
- Convert markdown to Notion markdown format
- Properly format code blocks, tables, lists
- Display file paths in code format

### Report Template

#### For Notion
Use [notion-page-template.md](./notion-page-template.md) to generate Notion subpage.

## Start Message
Starting Notion ticket impact analysis and effort estimation.
Analyzing codebase and estimating with 2,4,8,12,16 hours options.

**Usage:**
Provide Notion ticket URL as argument for analysis target.

**Output Format:**
- **Notion Subpage**: Automatically create "AI Analysis Results" page at end of ticket

## End Message
Completed ticket impact analysis.
Created "AI Analysis Results" subpage in original Notion ticket with detailed analysis report.

**Created Subpage**: [Generated URL]

Please review analysis results and use for implementation planning.

## File Structure
```
ticket-impact-analysis-with-estimation/
├── ticket-impact-analysis-with-estimation.md  # Main prompt file
├── internal-json-schema.json                  # Internal JSON structure definition
├── notion-page-template.md                    # Notion page template
├── estimation-criteria.md                     # Effort estimation criteria
└── analysis-commands.md                       # Analysis command collection
```