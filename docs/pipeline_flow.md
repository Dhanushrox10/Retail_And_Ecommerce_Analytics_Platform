# Data Pipeline Workflow
## 1. Environment setup
- Create a new workspace folder for the project.
- Organize notebooks by layers
- Create catalog, schema and volumes.
- Create connection between kaggle and Databricks by kaggle API.

## 2. Data Ingestion
- Transfer the CSV files (Customers, Products, Stores, Employees, Discounts, Transactions)
- Store it in volumes

## 3. Bronze layer
- Read the CSV files
- Sanitize column names
- Add ingestion metadata
- Write it in Delta format

Sample Output:
```
- retail_analytics.bronze.customers
- retail_analytics.bronze.products
```

## 4. Silver layer
- Remove duplicates and clean the data
- Handle null values
- Standardize values
- Trim strings, normalize case

Sample Output:
```
- retail_analytics.silver.customers
- retail_analytics.silver.products
```

## 5. Gold layer
- Enable fast analytics using star schema
- Store measurable business events
- Generate surrogate keys
- Optimized for dashboards

Dimension Tables:
- dim_date
- dim_customers
- dim_products
- dim_stores
- dim_employees
- dim_discounts

Fact Tables:
- fact_sales
- fact_returns

## 6. Dashboard & visualization
- Created 15+ KPI metrics
- Clean visuals and dashboards
- Databricks SQL queries
