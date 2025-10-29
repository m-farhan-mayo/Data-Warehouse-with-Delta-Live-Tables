# Data-Warehouse-with-Delta-Live-Tables


This repository contains the complete source code for an end-to-end data pipeline built using Delta Live Tables (DLT) in Databricks. The project follows a Medallion Architecture to process raw sales-related data (Customers, Products, Sales) into a clean, analytics-ready dimensional model.

The pipeline ingests raw data, progressively refines it through Bronze, Silver, and Gold layers, and ends by building a star schema (Fact and Dimension tables) suitable for business intelligence and reporting.

Key Concepts & Project Recall (File Breakdown)
This project is organized by the DLT Medallion layers, making the data flow easy to trace:

bronze Folder (customers_injection.py, products_injection.py, ...)

Purpose (Extract/Load): This is the ingestion layer. These scripts define the DLT tables that read raw data from an external source (like S3, ADLS, or Kafka) and load it, unaltered, into the Bronze tables. This creates the initial copy of the source data.

silver Folder (transform_customers.py, transform_products.py, ...)

Purpose (Transform/Clean): This is the data refinement layer. These scripts read from the bronze tables and apply transformations:

Cleaning (handling nulls, duplicates)

Type casting (e.g., string to timestamp)

Applying business rules

The output is a set of clean, validated "Silver" tables that serve as a single source of truth.

gold Folder (dim_customers.py, fact_sales.py, ...)

Purpose (Business Model): This is the final analytics layer. These scripts read from the silver tables to create the business-facing data models.

dim_customers / dim_products: Create the Dimension tables, which hold descriptive attributes (who, what, where).

fact_sales: Creates the Fact table, which holds quantitative metrics (the "how many") and the keys linking to the dimension tables.

business_sales: Likely a final, aggregated view for a specific report.

Tutorial Folder (1_CoreComponents.py, 2_Dependency.py)

Purpose: These files are the learning/reference part of the project. They explain the core DLT syntax, like defining tables (@dlt.table) and managing the data flow (dependencies) between them.

utilities Folder (utils.py)

Purpose: A central script for reusable code. This file likely contains helper functions, such as custom UDFs, schema definitions, or constants (like file paths) that are imported by the other pipeline scripts to avoid repeating code.
