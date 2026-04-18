# Logistics-Dashboard-

A Power BI template (`.pbit`) dashboard built to monitor and analyze logistics operations across shipments, fleet assets, and environmental conditions.

---

## Project Overview

This dashboard provides a centralized view of key logistics KPIs — from shipment performance and asset utilization to temperature and humidity tracking. The underlying data was manually cleaned before being loaded into the report.

---

## Dashboard Pages

### 1. Overview
High-level operational summary including:
- **KPI Cards** — Total Shipments, On-Time %, Delayed %, Transaction Amount, and Avg Utilization
- **Shipment Status Overview** — Line chart tracking shipment status trends over time
- **Fleet Utilization** — Line chart showing asset utilization over time
- **Top Locations by Volume** — Clustered bar chart ranking cities/states by shipment volume
- **Delay Reason Analysis** — Donut chart breaking down the causes of logistics delays
- **Slicers** — Interactive filters for date, city/state, and shipment status

### 2. Weather Monitoring
Environmental conditions tracking including:
- **Temperature & Humidity Monitoring** — Line chart showing sensor readings over time
- **KPI Cards** — Snapshot metrics for weather-related fields
- **Slicers** — Filters for time period and location

---

## Data Model

### Table: `LogisticsData` (Main Fact Table)
| Column | Type | Description |
|---|---|---|
| Asset_ID | Text | Unique identifier for each logistics asset |
| InventoryLevel | Integer | Current inventory count |
| ShipmentStatus | Text | Status of the shipment (e.g., On-Time, Delayed) |
| Temperature | Decimal | Recorded temperature at time of shipment |
| Humidity | Decimal | Recorded humidity level |
| Traffic_Status | Text | Traffic conditions at the time |
| WaitingTime | Integer | Time spent waiting (minutes) |
| UserTransactionAmount | Integer | Transaction value associated with the shipment |
| UserPurchaseFrequency | Integer | How frequently the user makes purchases |
| LogisticsDelayReason | Text | Reason for any delay |
| AssetUtilization | Decimal | Utilization rate of the asset (0–1) |
| DemandForecast | Integer | Forecasted demand for the period |
| LogisticsDelay | Integer | Binary flag — 1 = delayed, 0 = on-time |
| Date | Date/Time | Date of the shipment record |
| Time | Date/Time | Time of the shipment record |
| City | Text | City of the shipment |
| State | Text | State of the shipment |

### Table: `Date` (Calendar/Date Dimension)
Standard date table used for time intelligence, joined to `LogisticsData` on the `Date` field. Includes Year, Quarter, Month, Week, Day, and Day of Week columns.

### Table: `_Measures`
Dedicated measures table containing all DAX calculations:

| Measure | Logic |
|---|---|
| Total Shipments | Count of all rows in LogisticsData |
| On-Time% | % of shipments where LogisticsDelay = 0 |
| Delayed% | 1 minus On-Time% |
| Transaction Amount | Sum of UserTransactionAmount |
| Avg Utilization | Average of AssetUtilization |

---

## Relationships

| From | To | Type |
|---|---|---|
| `LogisticsData[Date]` | `Date[Date]` | Many-to-One |

---

## Data Preparation Notes

The source data was cleaned prior to being loaded into Power BI. Cleaning steps may have included:
- Removing duplicates or null records
- Standardizing text fields (e.g., ShipmentStatus, City, State)
- Formatting date/time columns
- Encoding the LogisticsDelay field as a binary flag (0/1)

---

## File Info

| Property | Value |
|---|---|
| File | `Logistics_Dashboard.pbit` |
| Type | Power BI Template |
| Compatibility Level | 1600 |
| Theme | CY25SU12 (Power BI 2025) |
| Created | April 2026 |
