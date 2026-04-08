# 🚀 Enterprise Sales, Finance & Supply Chain Lakehouse on Azure

## 📌 Project Overview

This project demonstrates the design and implementation of an enterprise-grade Azure Lakehouse architecture inspired by Hewlett-Packard (HP).

It simulates a real-world data platform handling:

* 🛒 Sales Data
* 💰 Finance Data
* 📦 Supply Chain Data

The solution supports batch + real-time data ingestion, implements CDC (Change Data Capture) and SCD Type 2, and delivers analytics-ready datasets using the Medallion Architecture (Bronze, Silver, Gold).

---

## 🎯 Business Problem

Enterprises like HP generate massive volumes of data from multiple systems such as ERP, CRM, and payment platforms.

### Key Challenges:

* Handling large-scale batch and streaming data
* Tracking historical changes in dimensions
* Ensuring data quality and governance
* Optimizing cost and performance

---

## 🏗️ Architecture Overview

### 🔹 High-Level Flow

```
Batch Source (CSV/API)        Streaming Source (Event Hub)
         ↓                           ↓
Azure Data Factory         Azure Event Hub
         ↓                           ↓
      ----------- ADLS Gen2 (Bronze Layer) -----------
                              ↓
                     Azure Databricks
     (Delta Lake + Medallion + CDC + SCD Type 2)
                              ↓
                Azure Synapse Serverless SQL
                              ↓
                       Power BI Dashboard
                              ↓
                    Azure DevOps (CI/CD)
```

---

## 🧱 Tech Stack

| Layer         | Technology                                       |
| ------------- | ------------------------------------------------ |
| Ingestion     | Azure Data Factory, Event Hub                    |
| Storage       | ADLS Gen2                                        |
| Processing    | Azure Databricks (PySpark, Delta Lake)           |
| Query Layer   | Azure Synapse Serverless SQL                     |
| Visualization | Power BI                                         |
| Security      | Azure Key Vault, Managed Identity, Unity Catalog |
| CI/CD         | Azure DevOps                                     |

---

## 📂 Medallion Architecture

### 🥉 Bronze Layer (Raw Data)

* Stores raw data as-is from source systems
* Supports reprocessing and auditing
* Schema-on-read approach
* Metadata columns:

  * ingestion_timestamp
  * source_system

---

### 🥈 Silver Layer (Cleaned & Processed)

* Data cleansing (null handling, deduplication)
* Schema enforcement
* CDC logic implementation
* Data quality checks:

  * Null validation
  * Duplicate removal
  * Schema validation

---

### 🥇 Gold Layer (Business Ready)

* Aggregated and analytics-ready datasets

#### Example Metrics:

* 📊 Daily Revenue
* 📦 Inventory Turnover
* 💰 Customer Lifetime Value
* 🚚 Order Fulfillment Time

---

## 🔁 Data Engineering Features

### ✅ Incremental Load

* Implemented using watermark (timestamp column)
* Processes only new or updated records

---

### 🔄 Change Data Capture (CDC)

* Detects inserts and updates from source systems
* Avoids full data reload

---

### 🔁 Slowly Changing Dimension (SCD Type 2)

Applied on Customer and Product dimensions to track history.

Columns Used:

* start_date
* end_date
* is_current

---

### ⚡ Real-Time Streaming

* Event-based ingestion using Azure Event Hub
* Processed using Databricks Structured Streaming / Autoloader

---

## 📊 Data Model

### Fact Tables:

* fact_transactions
* fact_orders

### Dimension Tables:

* dim_customer (SCD Type 2)
* dim_product
* dim_supplier

---

## 🔐 Security & Governance

* Secrets managed using Azure Key Vault
* Access control using RBAC
* Managed Identity for secure access
* Unity Catalog for data governance

---

## 🔄 CI/CD Implementation

* Git-based version control
* Azure DevOps pipelines
* Automated deployment of:

  * ADF pipelines
  * Databricks notebooks
  * Infrastructure configurations

---

## 📁 Project Structure

```
enterprise-lakehouse-hp/
│
├── data/
├── adf/
├── databricks/
│   ├── bronze/
│   ├── silver/
│   ├── gold/
│
├── streaming/
├── sql/
├── cicd/
├── docs/
│   ├── architecture.png
│   ├── challenges.md
│   ├── debugging.md
│
└── README.md
```

---

## ⚠️ Challenges Faced

* Handling late-arriving data
* Managing duplicate records in streaming
* Schema drift in incoming data
* SCD merge conflicts
* Event Hub throttling
* Databricks cluster auto-termination

---

## 🛠️ Debugging & Issue Tracking

All real-time issues, fixes, and learnings are documented in:

```
docs/challenges.md
docs/debugging.md
```

---

## 💡 Optimizations Implemented

* Delta Lake OPTIMIZE and VACUUM
* Z-Ordering for faster queries
* Partitioning strategy (date-based)
* Incremental processing
* Cluster auto-scaling and auto-termination

---

## 📈 Power BI Dashboard

* Sales Trends
* Revenue Analysis
* Customer Segmentation
* Financial KPIs

---

## 🚀 Future Enhancements

* Delta Live Tables (DLT)
* Data Quality Framework
* Monitoring using Azure Log Analytics
* GenAI-based anomaly detection

---

## 👨‍💻 Author

Abhishek Dasari
Azure Data Engineer | Databricks | Lakehouse Architect

---

## ⭐ How to Use This Project

1. Deploy Azure resources (Free Tier optimized)
2. Run batch + streaming pipelines
3. Execute Databricks notebooks
4. Query using Synapse
5. Visualize in Power BI

---

## 📌 Interview Pitch

“I built an enterprise-grade Azure Lakehouse simulating HP’s sales, finance, and supply chain systems, handling both batch and real-time data with CDC and SCD Type 2 using Databricks and Delta Lake.”
