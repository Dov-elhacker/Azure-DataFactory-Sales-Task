# 🧹 Azure Data Factory — Sales Data Cleaning Pipeline

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

## 🔄 Data Flow & Transformations

The Mapping Data Flow applies the following cleaning steps:

| Transformation | Description |
|----------------|-------------|
| **Filter** | Remove rows with missing `order_id`, `customer_id`, or `product` |
| **Derived Column** | Standardize `category` to lowercase (`electronics`) |
| **Derived Column** | Convert `order_date` to consistent `yyyy-MM-dd` format |
| **Conditional Split** | Filter out rows with `quantity <= 0` or `unit_price <= 0` |
| **Select** | Keep only essential columns: `order_id`, `order_date`, `customer_id`, `product`, `category`, `unit_price`, `Total Amount` |
| **Aggregate** | (Optional) Remove duplicate `order_id` records |

**Example Transformation (Derived Column for Date):**
```javascript
// Convert various date formats to yyyy-MM-dd
toString(toDate(order_date, 'yyyy-MM-dd'), 'yyyy-MM-dd')
