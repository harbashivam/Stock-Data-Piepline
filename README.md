┌────────────────────────────┐
│  Stock APIs / CSV / JSON   │
└────────────────────────────┘
             │
             ▼
┌────────────────────────────┐
│      Bronze Layer          │
│    Raw Delta in ADLS       │
└────────────────────────────┘
             │
             ▼
┌────────────────────────────┐
│      Silver Layer          │
│  • Remove duplicates &     │
│    missing values          │
│  • Standardize columns &   │
│    data types              │
│  • Add derived columns:    │
│    year, month, week       │
└────────────────────────────┘
             │
             ▼
┌────────────────────────────┐
│       Gold Layer           │
│  • Daily, weekly, monthly  │
│    aggregations            │
│  • avg_close, max_high,    │
│    min_low                 │
│  • KPI ready for dashboards│
└────────────────────────────┘
             │
             ▼
┌────────────────────────────┐
│       Delta Table          │
│  • Optimized for fast      │
│    queries                 │
│  • Partitioned by symbol & │
│    date                    │
└────────────────────────────┘
             │
             ▼
┌────────────────────────────┐
│   Databricks Dashboards    │
└────────────────────────────┘



Stock Market Data Pipeline

This project implements a robust and scalable stock market data pipeline using Delta Lake and Databricks on Azure Data Lake Storage (ADLS). It is designed to ingest raw stock data from multiple sources, clean and enrich it, perform time-based aggregations, and provide actionable insights through interactive Databricks dashboards. The pipeline follows modern data engineering best practices to ensure high data quality, reliability, and performance.

Project Overview

  The pipeline handles large volumes of stock market data from APIs and CSV/JSON files. It follows a layered architecture to          progressively refine and structure the data:

Bronze Layer:
    nStores raw, unprocessed data exactly as ingested, preserving full traceability and data lineage.
Silver Layer:
     Processes and cleans the data by removing duplicates and handling missing values. Standardizes schemas and enriches the dataset with derived fields such as year, month, and week.
Gold Layer:
     Produces analysis-ready, aggregated datasets optimized for performance. Provides daily, weekly, and monthly metrics including average      closing price, maximum highs, minimum lows, and total trading volumes.
     All processed data is stored as Delta Tables, optimized for fast queries and partitioned by symbol and date to support scalable            analytics.

Key Features
     Incremental Data Ingestion: Efficiently loads stock data from multiple sources.
     Data Cleaning & Enrichment: Ensures high data quality, removes duplicates, and standardizes schemas.
     Time-based Aggregations: Supports daily, weekly, and monthly metrics for in-depth analysis.
     Delta Lake Storage: Provides ACID-compliant tables for reliability and query performance.
     Interactive Dashboards: Visualize key stock metrics directly in Databricks.
     Modular and Extensible Architecture: Easy to maintain and extend for future requirements.
     
Technologies Used
     Databricks (PySpark, SQL) – Data processing and analytics platform.
     Azure Data Lake Storage (ADLS) Gen2 – Scalable and secure cloud storage.
     Delta Lake – ACID-compliant storage layer optimized for analytics.
     
Getting Started
     Configure access to your Azure Data Lake Storage and Databricks workspace.
     Create storage containers following the Bronze → Silver → Gold layer structure.
     Deploy and schedule data ingestion jobs to load raw stock data into the Bronze layer.
     Execute transformation notebooks to clean, enrich, and aggregate data through Silver and Gold layers.
     Use Databricks dashboards to analyze and visualize the processed metrics.
