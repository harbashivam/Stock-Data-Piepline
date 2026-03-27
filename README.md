📊 NIFTY & NSE Stock Data Pipeline
Project Overview

This project implements a multi-layered stock data pipeline using Databricks, PySpark, and Unity Catalog. It ingests raw NIFTY and NSE stock market data, cleans and transforms it, and generates aggregated insights for analytical and reporting purposes.

The pipeline follows a Bronze → Silver → Gold architecture:

Pipeline Architecture
               
              
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
              
Layer Details

1. Bronze Layer
Stores raw NIFTY and NSE stock data from CSV files in the data lake.
Preserves original data for auditability and recovery.
Example Table: nifty_catalog.nifty_schema.stock_raw

3. Silver Layer
Cleans and structures the raw data.
Transformations include:
Correcting data types
Handling missing or corrupt values
Standardizing column names
Example Table: nifty_catalog.nifty_schema.stock_cleaned

5. Gold Layer
Aggregated, business-ready data stored as Delta tables for performance, reliability, and versioning.
Daily and monthly aggregations include:
Open, Close, High, Low prices
Average closing price
Total traded volume and turnover

Example Tables:
gold_daily – Daily OHLC and volume per symbol
gold_monthly – Monthly OHLC and volume per symbol
Delta tables enable time travel and incremental updates for fast queries on dashboards.
Dashboards
Use Databricks built-in dashboard feature to visualize Gold layer tables.

Dashboards show:
Daily and monthly trends per stock symbol
Volume and turnover analytics
Open, Close, High, Low price charts
Can be parameterized by symbol or date range for interactive analysis.

Key Features
Delta Lake for ACID compliance and versioning
PySpark for scalable transformations
Unity Catalog for centralized governance and access control
Parameterized queries for symbol-specific analysis
Easily extensible for additional metrics or stock indices

Benefits
Centralized data warehouse for NIFTY and NSE stocks
Supports business reporting and dashboards
Enables daily and monthly trend analysis
Provides actionable insights for traders and analysts
Interactive dashboards help decision-makers monitor stock performance in real-time
