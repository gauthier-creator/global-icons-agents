---
name: data-context-extractor
description: >
  Generate or improve a company-specific data analysis skill by extracting tribal knowledge from analysts.

  BOOTSTRAP MODE - Triggers: "Create a data context skill", "Set up data analysis for our warehouse",
  "Help me create a skill for our database", "Generate a data skill for [company]"
  → Discovers schemas, asks key questions, generates initial skill with reference files

  ITERATION MODE - Triggers: "Add context about [domain]", "The skill needs more info about [topic]",
  "Update the data skill with [metrics/tables/terminology]", "Improve the [domain] reference"
  → Loads existing skill, asks targeted questions, appends/updates reference files

  Use when data analysts want Claude to understand their company's specific data warehouse,
  terminology, metrics definitions, and common query patterns.
---

# Data Context Extractor

A meta-skill that extracts company-specific data knowledge from analysts and generates tailored data analysis skills.

## How It Works

This skill has two modes:

1. **Bootstrap Mode**: Create a new data analysis skill from scratch
2. **Iteration Mode**: Improve an existing skill by adding domain-specific reference files

---

## Bootstrap Mode

Use when: User wants to create a new data context skill for their warehouse.

### Phase 1: Database Connection & Discovery

**Step 1: Identify the database type**

Ask: "What data warehouse are you using?"

Common options:
- **BigQuery**
- **Snowflake**
- **PostgreSQL/Redshift**
- **Databricks**

Use `~~data warehouse` tools (query and schema) to connect. If unclear, check available MCP tools in the current session.

**Step 2: Explore the schema**

Use `~~data warehouse` schema tools to:
1. List available datasets/schemas
2. Identify the most important tables (ask user: "Which 3-5 tables do analysts query most often?")
3. Pull schema details for those key tables

Sample exploration queries by dialect:
```sql
-- BigQuery: List datasets
SELECT schema_name FROM INFORMATION_SCHEMA.SCHEMATA

-- BigQuery: List tables in a dataset
SELECT table_name FROM `project.dataset.INFORMATION_SCHEMA.TABLES`

-- Snowflake: List schemas
SHOW SCHEMAS IN DATABASE my_database

-- Snowflake: List tables
SHOW TABLES IN SCHEMA my_schema
```

### Phase 2: Core Questions (Ask These)

After schema discovery, ask these questions conversationally (not all at once):

**Entity Disambiguation (Critical)*

> "When people here say 'user' or 'customer', what exactly do they mean? Are there different types?"

Listen for:
- Multiple entity types (user vs account vs organization)
- Relationships between them (1:1, 1:many, many:many)
- Which ID fields link them together

**Primary Identifiers**
> "What's the main identifier for a [customer/user/account]? Are there multiple IDs for the same entity?"

Listen for:
- Primary keys vs business keys
- UUID vs integer IDs
- Legacy ID systems

**Key Metrics**
> "What are the 2-3 metrics people ask about most? How is each one calculated?"

Listen for:
- Exact formulas (ARR = monthly_revenue � 12)
- Which tables/columns feed each metric
- Time period conventions (trailing 7 days, calendar month, etc.)

**Data Hygiene**
> "What should ALWAYS be filtered out of queries? (test data, fraud, internal users, etc.)"

Listen for:
- Standard WHERE clauses to always include
- Flag columns that indicate exclusions (is_test, is_internal, is_fraud)
- Specific values to exclude (status = 'deleted')

**Common Gotchas**
> "What mistakes do new analysts typically make with this data?"

Listen for:
- Confusing column names
- Timezone issues
- NULL handling quirks
- Historical vs current state tables

### Phase 3: Generate the Skil
