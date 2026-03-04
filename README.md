# Data-Warehouse-Project
A modern, end-to-end data warehouse built with SQL Server, implementing the Medallion Architecture (Bronze → Silver → Gold) with full ETL pipelines, dimensional data modelling, and an analytics layer designed to generate actionable business insights.

🎯 Built as a portfolio project to demonstrate industry best practices in data engineering and analytics.


📋 Table of Contents

Project Overview
Architecture
Repository Structure
Data Flow
Data Model
Analytics & Reporting

📌 Project Overview
This project demonstrates a complete data warehousing and analytics solution, including:

ETL Pipelines — Extract, Transform, and Load data through layered stages
Data Modelling — Star schema with fact and dimension tables for efficient querying
Data Quality — Cleansing, deduplication, and standardisation at the Silver layer
Analytics — SQL-based reporting and KPI generation at the Gold layer

🏛️ Architecture

This warehouse follows the Medallion Architecture:
Raw Sources
    │
    ▼
┌─────────────┐
│   BRONZE    │  ← Raw ingestion, no transformation
│  (Staging)  │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│   SILVER    │  ← Cleansed, standardised, deduplicated
│  (Cleaned)  │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│    GOLD     │  ← Business-ready star schema for analytics
│ (Analytics) │
└─────────────┘

LayerPurposeSchema NameBronzeRaw data as-is from sourcesbronzeSilverCleaned and validated datasilverGoldAggregated, analytics-readygold

📁 Repository Structure
SQL-Data-Warehouse-Project/
│
├── datasets/               # Raw source data (CSV files)
│   ├── crm/                # CRM system exports
│   └── erp/                # ERP system exports
│
├── docs/                   # Documentation and diagrams
│   ├── data_architecture.png
│   ├── data_flow.png
│   └── data_model.png
│
├── scripts/                # All SQL scripts, organised by layer
│   ├── bronze/             # DDL + stored procedures for raw ingestion
│   ├── silver/             # Transformation and cleansing scripts
│   ├── gold/               # Dimensional model views and tables
│   └── init_database.sql   # Database and schema initialisation
│
├── tests/                  # Data quality checks and validation queries
│
├── README.md
└── LICENSE

🔄 Data Flow

Ingest — Raw CSV files (CRM + ERP) are loaded into bronze tables via stored procedures
Cleanse — The silver layer applies transformations: trim whitespace, normalise dates, handle NULLs, and deduplicate records
Model — The gold layer builds a Star Schema with fact and dimension tables ready for reporting
Analyse — SQL analytics queries and views surface KPIs and business metrics

📊 Data Model
The Gold layer implements a Star Schema:
                    ┌──────────────────┐
                    │   dim_customers  │
                    └────────┬─────────┘
                             │
┌──────────────┐    ┌────────▼─────────┐    ┌──────────────┐
│  dim_products │────│   fact_sales     │────│   dim_date   │
└──────────────┘    └────────┬─────────┘    └──────────────┘
                             │
                    ┌────────▼─────────┐
                    │  dim_locations   │
                    └──────────────────┘
TableTypeDescriptionfact_salesFactOrder-level sales transactionsdim_customersDimensionCustomer attributes from CRMdim_productsDimensionProduct catalogue from ERPdim_dateDimensionDate/time hierarchy for time seriesdim_locationsDimensionGeographic data for regional analysis

📈 Analytics & Reporting
The Gold layer exposes pre-built SQL views for common business questions:
ReportDescriptionreport_sales_by_regionRevenue breakdown by geographyreport_top_productsBest-selling products by quantity & revenuereport_customer_segmentsCustomer groupings by purchase behaviourreport_monthly_trendsMonth-over-month revenue trends



