#  Azure Data Factory — Sales Data Cleaning Pipeline

This project builds an **end-to-end ETL pipeline** using **Azure Data Factory (ADF)** to clean and transform a raw, messy sales dataset. The goal is to automate the processing of raw sales data, handle common data quality issues, and output a cleansed dataset ready for analytics and reporting.
---

##  Overview

Raw CSV files often contain:
-  Missing or invalid values
-  Duplicate or incomplete records
-  Inconsistent date formats
-  Negative quantities or prices

This pipeline addresses those issues by leveraging **Azure Data Factory's Mapping Data Flows** to apply a series of data quality rules and transformations, producing a clean, analysis-ready dataset.

---

## Architecture
The pipeline follows a standard ETL flow:


| Component | Azure Service | Purpose |
|-----------|---------------|---------|
| **Source** | Azure Blob Storage | Stores the raw `sales.csv` file |
| **Orchestration** | Azure Data Factory | Coordinates the ETL workflow |
| **Transformation** | Mapping Data Flow | Applies cleaning rules and transformations |
| **Sink** | Azure Blob Storage | Stores the cleaned `cleaned_sales.csv` output |

---

## Data Flow & Transformations

The Mapping Data Flow applies the following cleaning steps:

| Transformation | Description |
|----------------|-------------|
| **Filter** | Remove rows with missing `order_id`, `customer_id`, or `product` |
| **Derived Column** | Standardize `category` to lowercase (`electronics`) |
| **Derived Column** | Convert `order_date` to consistent `yyyy-MM-dd` format |
| **Conditional Split** | Filter out rows with `quantity <= 0` or `unit_price <= 0` |
| **Select** | Keep only essential columns: `order_id`, `order_date`, `customer_id`, `product`, `category`, `unit_price`, `Total Amount` |
| **Aggregate** | (Optional) Remove duplicate `order_id` records |


Prerequisites
Active Azure Subscription

Azure Data Factory instance (V2)

Azure Blob Storage account with a container

Setup Instructions
Upload Raw Data
Upload the sales.csv file to your Azure Blob Storage container.

Import the Pipeline

In ADF Studio, go to Author → Pipelines → Import from pipeline template (or manually create the pipeline).

Use the provided pipeline JSON (if available) or recreate the Data Flow as shown above.

Configure Linked Services

Create a Linked Service for Azure Blob Storage.

Create Datasets for the source CSV and the sink CSV.

Run the Pipeline

Click Debug to test with a subset of data.

Click Trigger Now to run the full pipeline.

Verify Output

Check your Blob Storage container for the cleaned_sales.csv file.

Compare with the sample output provided in this repo.

Before (Raw sales.csv):

order_id,order_date,customer_id,product,category,quantity,unit_price,Total Amount
103,,cust002,Headphones,,2,-100,-200
93,2024-01-01,C-003,Phone,Elec,-1,-100,100
15,2024-01-01,cust002,Phone,Elec,3,200,600
107,01/02/2024,CUST001,Headphones,Elec,3,1000,3000

After (Cleaned cleaned_sales.csv):

order_id,order_date,customer_id,product,category,unit_price,Total Amount
101,2024-01-01,CUST001,Phone,electronics,500,1000
106,01/02/2024,CUST001,Headphones,electronics,50,50
107,01/02/2024,CUST001,Headphones,electronics,1000,3000
113,2024/04/05,004,Monitor,electronics,200,400

| File | Description |
|------|-------------|
| sales.csv | Raw, unprocessed sales data |
| cleaned_sales.csv | Output after ETL pipeline |
| cloud final.pdf | Additional documentation / report |
| README.md | Project documentation |


## Requirements

| Requirement | Details |
|-------------|---------|
| Azure Subscription | Required to deploy ADF and Blob Storage |
| Azure Data Factory | Version V2 (with Data Flow enabled) |
| Azure Blob Storage | General-purpose V2 storage account |
| Permissions | Contributor or Owner role on the resource group |

Acknowledgments
Inspired by real-world data cleaning challenges in retail analytics.

Built as a hands-on project to demonstrate Azure Data Factory capabilities for data engineering portfolios.

Contact
Author: Dov-elhacker
Project Link: https://github.com/Dov-elhacker/Azure-DataFactory-Sales-Task
