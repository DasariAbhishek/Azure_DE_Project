# 🚀 Enterprise Sales & Finance Data Platform on Azure

## 📌 Project Overview

This project demonstrates the design and implementation of an **enterprise-grade Azure Lakehouse architecture** simulating a real-world **Sales & Finance data platform (HP-like use case)**.

The solution handles **batch + streaming data ingestion**, implements **CDC (Change Data Capture)** and **SCD Type 2**, and delivers curated analytics-ready datasets using **Medallion Architecture (Bronze, Silver, Gold)**.

---

## 🎯 Business Problem

Enterprises like HP generate large volumes of **sales and financial transactions** from multiple systems (ERP, CRM, payment systems).

Challenges:

* Handling large-scale batch and real-time data
* Tracking historical customer changes
* Ensuring data quality and governance
* Optimizing cost and performance

---

## 🏗️ Architecture Overview

### 🔹 High-Level Flow:

```
Batch Source (CSV/API)        Streaming Source (Event Hub)
         ↓                           ↓
   Azure Data Factory         Azure Event Hub
         ↓                           ↓
          ----------- ADLS (Bronze Layer) ----------
                              ↓
                     Azure Databricks
            (Delta Lake + Medallion Architecture)
       Bronze → Silver → Gold + SCD Type 2 + CDC
                              ↓
                Azure Synapse Serverless
                              ↓
                       Power BI Dashboard
                              ↓
                    CI/CD (Azure DevOps)
```

---

## 🧱 Tech Stack

* **Data Ingestion:** Azure Data Factory, Event Hub
* **Storage:** ADLS Gen2
* **Processing:** Azure Databricks (PySpark, Delta Lake)
* **Serving Layer:** Azure Synapse Serverless SQL
* **Visualization:** Power BI
* **Security:** Azure Key Vault, Managed Identity
* **CI/CD:** Azure DevOps

---

## 📂 Data Architecture (Medallion)

### 🥉 Bronze Layer (Raw)

* Stores raw data as-is from source
* Supports reprocessing and auditing
* Includes metadata columns:

  * ingestion_timestamp
  * source_file

---

### 🥈 Silver Layer (Cleaned & Processed)

* Data cleansing (null handling, deduplication)
* Schema enforcement
* Data quality checks:

  * Null validation
  * Record count reconciliation
  * Schema validation

---

### 🥇 Gold Layer (Business Ready)

* Aggregated datasets for reporting
* Examples:

  * Total Revenue per Day
  * Customer Lifetime Value
  * Sales by Category

---

## 🔁 Data Engineering Features

### ✅ Incremental Load

* Implemented using watermark (timestamp column)
* Reduces processing time and cost

---

### 🔄 Change Data Capture (CDC)

* Detects inserts/updates from source systems
* Enables efficient data updates

---

### 🔁 Slowly Changing Dimension (SCD Type 2)

* Applied on Customer Dimension
* Tracks historical changes

**Columns Used:**

* start_date
* end_date
* is_current

---

### ⚡ Streaming Pipeline

* Real-time transaction ingestion using Event Hub
* Processed via Databricks Autoloader

---

## 🔐 Security & Governance

* Secrets managed using Azure Key Vault
* Access control using RBAC & Unity Catalog
* Secure data access with Managed Identity

---

## 🔄 CI/CD Implementation

* Git-based version control
* Azure DevOps pipelines for deployment
* Automated deployment of:

  * ADF pipelines
  * Databricks notebooks
  * Infrastructure configs

---

## 📊 Data Model

### Fact Table:

* Transactions

### Dimension Tables:

* Customer (SCD Type 2)
* Product
* Account

---

## 📈 Power BI Dashboard

* Sales Trends
* Revenue Analysis
* Customer Segmentation
* Financial KPIs

---

## ⚠️ Challenges Faced

* Handling late-arriving data
* Managing duplicate records
* Schema drift in streaming data
* SCD merge conflicts
* Databricks cluster auto-termination
* Cost optimization for large datasets

---

## 💡 Optimizations Implemented

* Partitioning strategy for large datasets
* Delta Lake OPTIMIZE and VACUUM
* Z-ordering for faster queries
* Auto-termination for Databricks clusters
* Incremental data processing

---

## 📌 Key Learnings

* Designing scalable Lakehouse architectures
* Handling real-time + batch hybrid pipelines
* Implementing enterprise data governance
* Optimizing cloud cost and performance

---

## 📷 Architecture Diagram

*(Add your diagram here)*

---

## 📁 Project Structure

```
enterprise-finance-lakehouse/
│
├── adf/
├── databricks/
├── streaming/
├── sql/
├── cicd/
├── docs/
└── README.md
```

---

## 🚀 Future Enhancements

* Delta Live Tables (DLT)
* Data Quality Framework
* Monitoring with Azure Log Analytics
* GenAI-based anomaly detection

---

## 👨‍💻 Author

**Abhishek Dasari**
Azure Data Engineer | Databricks | Lakehouse Architect
