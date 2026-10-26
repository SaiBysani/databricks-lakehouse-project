# Databricks Lakehouse | Medallion Architecture Pipeline

An end-to-end data engineering project using **Databricks, PySpark, Delta Lake, and Unity Catalog** to process e-commerce data through Bronze, Silver, and Gold layers.

The project demonstrates raw data ingestion, data cleaning, deduplication, incremental upserts, workflow orchestration, and business reporting using Databricks AI/BI Dashboards.

## Architecture

```text
CSV Files
   |
   v
Bronze - Raw Data Ingestion
   |
   v
Silver - Cleaning, Validation & MERGE
   |
   v
Gold - Business Reporting Tables
   |
   v
AI/BI Dashboard
```

## Tech Stack

- **Databricks & PySpark** — Data processing and transformations
- **Delta Lake** — Reliable storage, table history, and `MERGE` operations
- **Unity Catalog** — Table organization and governance
- **Databricks Jobs** — Pipeline orchestration and task dependencies
- **AI/BI Dashboards** — Sales and product performance reporting

## Project Structure

```text
databricks_lakehouse/
├── data/
│   ├── initial_load/
│   └── incremental_load/
├── notebooks/
│   ├── 00_shared_config.py
│   ├── bronze/
│   │   └── 01_bronze_load.py
│   ├── silver/
│   │   ├── 02_silver_customers.py
│   │   ├── 03_silver_orders.py
│   │   ├── 04_silver_order_items.py
│   │   └── 05_silver_products.py
│   └── gold/
│       ├── 06_gold_daily_sales.py
│       └── 07_gold_product_performance.py
└── README.md
```

## Pipeline Overview

- **Bronze:** Loads source CSV files into Delta tables and adds audit columns for ingestion tracking.
- **Silver:** Cleans and validates records, removes duplicates, standardizes data, and uses Delta Lake `MERGE` to update or insert orders and order items.
- **Gold:** Builds reporting tables for daily sales and product performance, including revenue, transaction counts, units sold, and average selling prices.
- **Orchestration:** Uses a shared configuration notebook and Databricks Jobs to manage parameters and task dependencies.
- **Dashboard:** Visualizes sales trends, customer segments, and product performance using Gold tables.

## Getting Started

### Prerequisites

- A Databricks workspace with Unity Catalog enabled.
- Permissions to create tables, run notebooks, and configure Jobs.
- A SQL warehouse for the AI/BI Dashboard.

### Setup

1. Clone or download this repository:

   ```bash
   git clone https://github.com/arpitsirasao/databricks_lakehouse.git
   ```

2. Import the notebooks and make the sample data accessible in your Databricks workspace.

3. Update `workspace_root`, `catalog`, and `schema` in `00_shared_config.py` to match your environment.

4. Run the pipeline in **initial** mode to load the historical data and create the baseline tables.

5. Switch to **incremental** mode to process new order and order-item files.

6. Configure a Databricks Job to orchestrate the notebooks, then build an AI/BI Dashboard using the Gold tables.

**Note:** Bronze appends incremental file arrivals, so rerunning a batch can create additional raw rows. Silver upserts help prevent duplicate business keys from propagating, but production pipelines should also consider processed-file tracking and batch ordering.

## Key Concepts

Medallion Architecture · Delta Lake MERGE · Incremental Loads · PySpark · Data Quality · Unity Catalog · Databricks Jobs · AI/BI Dashboards

## Author

**Sai Kumar Bysani**

[GitHub Profile](https://github.com/SaiBysani)
