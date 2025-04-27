# Jaffle Shop: A dbt Features Study Guide

This repository contains a sample dbt project that demonstrates various dbt features and best practices. It serves as a study guide for the dbt Analytics Engineer certification.

## Features Implemented

### Project Structure
- **[Model Organization](jaffle_shop/models/)**: Uses a layered architecture pattern
  - **[Staging Layer](jaffle_shop/models/staging/)**: Simple models that clean raw data
  - **[Marts Layer](jaffle_shop/models/marts/)**: Business-specific transformations organized by domain (finance, marketing)

### Sources
- **[Source Definitions](jaffle_shop/models/sources.yml)**: Defines external data sources
- **Freshness Checks**: Configured for order and payment data with warn/error thresholds
- **Source Documentation**: Descriptions for sources, tables, and columns

### Materializations
- **Views**: All staging models configured as views (defined in dbt_project.yml)
- **Tables**: All marts models configured as tables (defined in dbt_project.yml)

### Referencing
- **Source Function**: `{{ source('jaffle_shop', 'customers') }}` to reference raw data
- **Ref Function**: `{{ ref('stg_customers') }}` to reference other models

### Testing
- **Generic Tests**: 
  - `unique` and `not_null`: Applied to primary keys
  - `accepted_values`: Validating status fields
  - `relationships`: Enforcing referential integrity
- **Singular Tests**: Custom SQL tests (e.g., [assert_positive_total_for_payments.sql](jaffle_shop/tests/assert_positive_total_for_payments.sql))

### Documentation
- **Model Descriptions**: In schema.yml files
- **Column Descriptions**: Detailed explanations of important columns

### SQL Techniques
- **CTEs**: For readable transformations
- **Aggregations**: Sum, count, min/max functions
- **Join Operations**: Primarily left joins between related data

### Configuration
- **Project Config**: In [dbt_project.yml](jaffle_shop/dbt_project.yml)
- **Model Configs**: Materializations defined at directory level

## Running the Project

Basic commands:
```bash
# Run all models
dbt run

# Run specific models
dbt run --models staging
dbt run --models marts.marketing.customers

# Test all models
dbt test

# Generate documentation
dbt docs generate
dbt docs serve
```

## Study Tips

When studying for the Analytics Engineer certification:
1. Understand the difference between staging and marts models
2. Practice writing effective tests
3. Learn how to document your models properly
4. Understand performance implications of different materializations
5. Practice referencing models and sources correctly