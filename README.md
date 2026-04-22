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
