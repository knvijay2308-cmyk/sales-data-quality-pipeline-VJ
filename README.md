## End-to-End Sales Data Quality Pipeline with Azure Databricks, Delta Lake and Automated Logging

# 1. Overview

This project implements a complete data quality pipeline for retail sales transactions using Azure Databricks and Delta Lake.
The pipeline validates raw data using four core data quality checks and maintains automated logging for full auditability.

The goal is to demonstrate practical data engineering skills with structured notebooks, reusable validation logic, Delta Lake storage, and automated reporting.

# 2. Features Implemented

2.1 Data Quality Checks

The raw dataset is validated using the following rules:

Null Check: Ensures no required fields contain missing values.

Duplicate Check: Detects duplicate transaction records based on all columns.

Schema Check: Compares expected schema with the actual schema and reports mismatches.

Threshold Check: Validates business rules on numeric fields such as amount and quantity.

Each rule writes its results to a Delta table for traceability.

2.2 Automated Logging Framework

A reusable logging function records data quality outcomes with the following fields:

rule_name

status (PASS or FAIL)

failed_count

timestamp

file_name


Log entries are stored in a Delta table at the following location:

/mnt/salesdq/validated/dq_results.delta

This enables historical tracking, auditability, and downstream reporting.

2.3 Notebook and Pipeline Structure

The Databricks notebook is organized into clear, modular sections:

1. Load raw data

2. Create validated results Delta table

3. Logging function

4. Null Check

5. Duplicate Check

6. Schema Check

7. Threshold Check

8. Run all validations and log results

This structure makes the pipeline easy to understand, maintain, and extend.

# 3. Architecture Overview

Bronze Layer

Stores raw CSV input.

No transformations applied.

Silver Layer

Contains cleaned and validated datasets.

Outputs from data quality rules.

Gold Layer

Final reporting tables for dashboards and analysis.

Includes aggregates and summaries based on validation logs.

# 4. Technology Stack

Azure Databricks

PySpark

Delta Lake

Azure Storage (mounted using DBFS)

Databricks SQL

# 5. Dashboard

A Databricks SQL dashboard was created to view data quality results.
It provides:
Rule-wise failure counts

Pass/Fail distribution

Historical trends

Drill-down into specific validation failures

This enables teams to monitor data reliability easily.

# 6. How to Run the Pipeline

1. Upload the raw CSV file into the Bronze storage location.

2. Mount Azure Storage to Databricks.

3. Open the Databricks notebook provided in the repository.

4. Run initialization cells (load data and create log table).

5. Execute each validation cell or run the combined “Run All Checks” cell.

6. View results in the Delta table /mnt/salesdq/validated/dq_results.delta.

7. Use the SQL dashboard to analyze data quality outcomes.

# 7. Folder Structure

sales-data-quality-pipeline/
│
├── code/
│   └── dq_pipeline.py
│
├── notebooks/
│   └── databricks_notebook_export.py
│
├── dashboard/
│   ├── notebook_dashboard_screenshots/
│   └── sql_dashboard_screenshots/
│
├── docs/
│   └── architecture.png
│
└── README.md

# 8. Outcomes

This project demonstrates:

Designing a structured data quality framework

Implementing validation logic using PySpark

Using Delta Lake for reliable data logging

Creating dashboards in Databricks SQL

Organizing a data engineering project for real-world usage

# 9. Future Enhancements

Add unit tests for validation methods

Automate the pipeline using Databricks Workflows

Integrate alerting when failures exceed thresholds

Extend dashboards with additional insights



