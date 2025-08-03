# COVID-19 Data Engineering Pipeline (Azure End-to-End Project)

This project demonstrates a **scalable, cloud-based data engineering solution** using Microsoft Azure services. The pipeline ingests, transforms, and serves COVID-19 data by following the **Medallion architecture** — enabling clean, reliable, and structured data layers for analytics and visualisation.

---

## Project Overview

This project processes public COVID-19 datasets using Azure Data Services in a **modular, secure, and scalable** pipeline. The architecture is designed using:

- **Azure Data Factory (ADF)** – Orchestrates the pipeline (ETL)
- **Azure Data Lake Storage (ADLS Gen2)** – Central data storage
- **Azure Databricks** – Performs data transformation with PySpark
- **Azure Synapse Analytics** – Enables querying and reporting
- **Azure Key Vault** – Secures credentials and tokens

The project is structured around the **Medallion architecture** with **Bronze**, **Silver**, and **Gold** data layers.

---

## Architecture

### Bronze Layer (Raw)
- Stores raw, unprocessed CSV files ingested from GitHub.
- Data is directly copied into **ADLS** using ADF.

### Silver Layer (Cleaned)
- Basic data cleansing and transformations performed using **Databricks (PySpark)**.
- Standardised column names, removed nulls, fixed schema issues.

### Gold Layer (Aggregated)
- Data is transformed to serve business-specific use cases:
  - **Country-wise Aggregation**
  - **Region-wise Aggregation**
- Final data is exposed to **Azure Synapse Analytics** for reporting and visualisation.

---

## Security and Configuration

### Azure Key Vault
- All sensitive information like:
  - ADF connection strings
  - Databricks personal access token
- Are stored securely in **Azure Key Vault** and accessed dynamically via linked services.

### Linked Services and Integration
- Linked Services in ADF and Databricks reference Azure Key Vault secrets.
- Application registration with **Azure Active Directory** enables secure, token-based access across services.

---

## Pipeline Flow

1. **ADF Pipeline** triggers data ingestion from GitHub to ADLS (Bronze).
2. **Metadata-driven ForEach loop** processes multiple datasets.
3. **Databricks Notebooks** transform data from Bronze to Silver and Silver to Gold using PySpark.
4. Final Gold tables are made available to **Synapse SQL views** for BI tools.

---

## Tech Stack

| Tool/Service          | Purpose                                  |
|----------------------|------------------------------------------|
| Azure Data Factory    | Orchestration and data ingestion         |
| Azure Data Lake       | Scalable cloud storage (Gen2)            |
| Azure Databricks      | Data transformation using PySpark        |
| Azure Synapse         | SQL-based querying and reporting         |
| Azure Key Vault       | Secret and credential management         |
| GitHub                | Source for raw COVID data                |
