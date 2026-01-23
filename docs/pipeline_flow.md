Data Pipeline Workflow
##1. Data Ingestion (Raw → Bronze)

Source

CSV files (Customers, Products, Stores, Employees, Discounts, Transactions)

Actions

Read raw CSV files from cloud storage

Infer schema

Preserve original column names

Add ingestion metadata

Output

retail_analytics.bronze.* Delta tables

Key points

No business logic

No deduplication

Append-only

##2. Data Standardization & Cleaning (Bronze → Silver)

Purpose
Create analytics-ready, trusted datasets.

Actions

Sanitize column names (snake_case, no spaces)

Remove duplicates using business keys

Handle null values (Not available)

Standardize values (e.g., M → Male, F → Female)

Trim strings, normalize case

Add derived columns (e.g., ingestion_date)

Output

retail_analytics.silver.customers

retail_analytics.silver.products

retail_analytics.silver.stores

retail_analytics.silver.employees

retail_analytics.silver.discounts

retail_analytics.silver.transactions

##3. Dimensional Modeling (Silver → Gold – Dimensions)

Purpose
Enable fast analytics using star schema.

Dimension Tables

dim_customers (SCD-1)

dim_products

dim_stores

dim_employees

dim_discounts

dim_date

Actions

Generate surrogate keys (*_sk)

Add metadata columns:

_created_at

_updated_at

Use MERGE for upserts

##4. Fact Table Creation (Silver → Gold – Facts)

Purpose
Store measurable business events.

Fact Tables

fact_sales

fact_returns

Actions

Filter transaction types (Sale / Return)

Join with dimension tables

Generate foreign keys (*_sk)

Calculate measures:

sales_amount

quantity_sold

refund_amount

##5. Gold Layer Output

Schema

Star schema (Facts + Dimensions)

Optimized for BI & dashboards

Used For

KPIs

Aggregations

Time-series analysis

Customer & product analytics

##6. Analytics & Dashboards

Platform

Databricks SQL (Community Edition)

Dashboards

Sales Performance

Customer Lifetime Value (CLV)

Product Performance

Store Performance

Returns Analysis