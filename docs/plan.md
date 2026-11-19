# NYC Yellow Taxi – Project Plan

## 1. Dataset

**Dataset:** NYC Yellow Taxi Trip Records

**Source:** New York City Taxi and Limousine Commission (TLC)

**Format:** Parquet

**Selected delivery:** January 2026 (`yellow_tripdata_2026-01.parquet`)

**Description:**

The project uses NYC Yellow Taxi trip records to build a data engineering pipeline in Databricks following the Medallion Architecture (Bronze, Silver, and Gold).

Each record represents a taxi trip and contains information about pickup and drop-off timestamps, pickup and drop-off locations, trip distance, passenger count, and payment information.

The primary objective is to transform raw taxi trip data into reliable, structured, and aggregated datasets that help business stakeholders understand taxi demand and operational performance across New York City.

The project will also use the NYC TLC Taxi Zone Lookup dataset to enrich location IDs with zone names and borough information.

## 2. Business Questions

The following business questions will guide the Gold layer design.

| # | Business question | Who asks? | How often? | Gold table |
|---|---|---|---|---|
| 1 | How many taxi trips occur each day, and how does the daily trip volume change over time? | Operations Manager | Daily | `gold_daily_trip_volume` |
| 2 | Which pickup and drop-off zones have the highest number of taxi trips? | Dispatch Manager | Daily | `gold_zone_demand` |
| 3 | What are the busiest hours and days of the week based on taxi pickup volume? | Fleet Manager | Weekly | `gold_hourly_demand` |
| 4 | What are the average trip duration and distance for each pickup zone? | Operations Analyst | Weekly | `gold_trip_performance` |
| 5 | How does taxi demand vary across NYC boroughs over time? | Operations Manager | Monthly | `gold_borough_demand` |
| 6 | How many rows were rejected during processing, and what were the reasons for rejection? | Data Engineer | Every pipeline run | `gold_data_quality_summary` |

## 3. Data Readers and Access

The project will have three main reader roles.

| Reader | Access permissions | Purpose |
|---|---|---|
| Operations Manager | Access to all Gold tables. No access to raw Bronze data. | Monitor overall taxi demand and operational performance. |
| Operations Analyst | Access to all Gold tables, containing aggregated and business-ready data. No access to raw Bronze or Silver data. | Perform operational analysis and identify demand patterns. |
| Data Engineer | Access to Bronze, Silver, Gold, quarantine, and data quality results. | Maintain pipelines, investigate rejected records, and monitor data quality. |

### Access principles

- Business users should access curated Gold datasets rather than raw trip records.
- Operations Managers and Analysts should only access aggregated, business-ready data.
- Data Engineers require access to all pipeline layers to investigate and resolve data quality issues.
- Access permissions will be implemented using Unity Catalog grants and appropriate schemas or views during Phase 4.

## 4. Project Scope

The project focuses on:

- Building an automated data pipeline in Databricks.
- Implementing the Bronze, Silver, and Gold layers.
- Cleaning and validating taxi trip records.
- Enriching taxi location IDs using the Taxi Zone Lookup dataset.
- Creating aggregated Gold tables to answer operational business questions.
- Implementing data quality checks and quarantine handling.
- Applying access control through Unity Catalog.

The project focuses on historical trip records. It does not measure real-time vehicle availability, passenger waiting times, or unfulfilled ride requests.
