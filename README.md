<!DOCTYPE html>

# Pharmacy Analytics Data Warehouse 💊

<div align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&pause=1000&color=00B4D8&center=true&vCenter=true&width=600&lines=Clinical+Pharmacy+Data+Warehouse;MIMIC-III+%7C+Kimball+Star+Schema;SSIS+ETL+%7C+SSRS+Reports+%7C+Tableau;Neo4j+Graph+Database+%7C+CQL+Queries;MSc+Data+Analytics+%E2%80%94+Dublin+Business+School" alt="Typing Animation" />
</div>

<p align="center">
  <img alt="SQL Server" src="https://img.shields.io/badge/SQL_Server-CC2927?style=for-the-badge&logo=microsoftsqlserver&logoColor=white"/>
  <img alt="SSIS" src="https://img.shields.io/badge/SSIS-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white"/>
  <img alt="SSRS" src="https://img.shields.io/badge/SSRS-5C2D91?style=for-the-badge&logo=microsoft&logoColor=white"/>
  <img alt="Neo4j" src="https://img.shields.io/badge/Neo4j-008CC1?style=for-the-badge&logo=neo4j&logoColor=white"/>
  <img alt="Tableau" src="https://img.shields.io/badge/Tableau-E97627?style=for-the-badge&logo=tableau&logoColor=white"/>
  <img alt="Visual Studio" src="https://img.shields.io/badge/Visual_Studio_2022-5C2D91?style=for-the-badge&logo=visualstudio&logoColor=white"/>
</p>

<p align="center">
  <img alt="Stars" src="https://img.shields.io/github/stars/abinraju23/pharmacy-analytics-dw?style=flat-square&color=00B4D8"/>
  <img alt="License" src="https://img.shields.io/badge/license-MIT-00B4D8?style=flat-square"/>
  <img alt="MSc" src="https://img.shields.io/badge/MSc-Data_Analytics-0077B6?style=flat-square"/>
  <img alt="DBS" src="https://img.shields.io/badge/Dublin_Business_School-B9DA111-003566?style=flat-square"/>
</p>

---

## 🏥 What This Project Does

A **proof-of-concept clinical pharmacy data warehouse** built on the **MIMIC-III PhysioNet dataset**, designed to surface actionable intelligence from ICU prescription and medication administration records.

The pipeline runs end-to-end: raw clinical data is staged in an **operational SQL Server database**, transformed and loaded via **SSIS**, stored in a **Kimball star schema warehouse**, reported through **SSRS**, visualised in **Tableau**, and cross-compared with a **Neo4j graph database** implementation.

---

## 🗂️ Architecture Overview

```
MIMIC-III Clinical DB (Source)
        │
        ▼
┌─────────────────────┐
│  Operational DB      │  ← Raw clinical tables (prescriptions, admissions,
│  (PharmacyOps)       │    patients, drug events, caregivers)
└─────────┬───────────┘
          │  SSIS ETL (Extract → Transform → Load)
          ▼
┌─────────────────────┐
│  Data Warehouse      │  ← Kimball Star Schema
│  (PharmacyDW)        │    Fact: FactMedication
└─────────┬───────────┘    Dims: DimPatient, DimDrug, DimDate,
          │                       DimAdmission, DimCaregiver
          ├──► SSRS Reports (4 paginated reports)
          ├──► Tableau Dashboard (4 visualisations)
          └──► Neo4j Graph DB (7 SQL ↔ CQL comparisons)
```

---

## ✨ Key Features

<div align="center">

| 🏗️ **Data Warehouse Design** | ⚙️ **ETL Pipeline** | 📊 **BI & Reporting** |
|---|---|---|
| Kimball Star Schema | SSIS Visual Pipelines | 4 SSRS Paginated Reports |
| SCD Type 2 Tracking | Staging → Cleanse → Load | Tableau Dashboard |
| Surrogate Key −1 (Unknown) | Derived Date Dimension | Drill-through & Filters |
| Atomic Grain Fact Table | NULL handling & type casting | KPIs & Trend Analysis |

| 🔗 **Graph Database** | 🧠 **Schema Design** |
|---|---|
| Neo4j Nodes & Relationships | Entity-Relationship Diagram |
| 7 Matched SQL ↔ CQL Queries | Visio / Draw.io Schema Diagram |
| Traversal vs. Join Performance | Normalised Operational Source |
| MIMIC-III as Data Source | Denormalised Star Schema DW |

</div>

---

## 📁 Repository Structure

```
pharmacy-analytics-dw/
│
├── 📂 sql/
│   ├── operational_db/          # DDL scripts for source DB (PharmacyOps)
│   ├── data_warehouse/          # DDL scripts for DW (PharmacyDW)
│   └── queries/                 # Analytical SQL queries
│
├── 📂 ssis/
│   └── PharmacyETL/             # Visual Studio SSIS project (.dtsx packages)
│
├── 📂 ssrs/
│   └── PharmacyReports/         # SSRS project + exported PDFs
│
├── 📂 neo4j/
│   ├── cypher_queries.cql       # All 7 CQL queries
│   └── screenshots/             # Neo4j Browser output screenshots
│
├── 📂 tableau/
│   ├── PharmacyDashboard.twbx   # Packaged Tableau workbook
│   └── screenshots/             # Dashboard & visualisation exports
│
├── 📂 docs/
│   ├── schema_diagram.vsdx      # Visio ER & star schema diagram
│   ├── report.docx              # Full group report
│   └── individual_report.docx   # Individual contribution report
│
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites

- Microsoft SQL Server 2019+ with SSMS
- Visual Studio 2022 with SSIS/SSDT extension
- Neo4j Desktop 5.x
- Tableau Desktop / Tableau Public
- MIMIC-III Clinical Database Demo v1.4 (requires PhysioNet credentialing)

### Setup Steps

```sql
-- 1. Create operational source database
USE master;
CREATE DATABASE PharmacyOps;

-- 2. Run DDL scripts to build source tables
-- /sql/operational_db/create_tables.sql

-- 3. Load MIMIC-III CSV data into source tables
-- /sql/operational_db/load_data.sql

-- 4. Create data warehouse database
CREATE DATABASE PharmacyDW;

-- 5. Run DW DDL to create dimensions and fact table
-- /sql/data_warehouse/create_dw_schema.sql
```

```
# 6. Open and run SSIS project in Visual Studio 2022
#    /ssis/PharmacyETL/PharmacyETL.sln

# 7. Open SSRS project for reports
#    /ssrs/PharmacyReports/PharmacyReports.sln

# 8. Open Tableau workbook
#    /tableau/PharmacyDashboard.twbx

# 9. Import Neo4j data and run CQL queries
#    /neo4j/cypher_queries.cql
```

---

## 📊 Sample Queries

**Most Prescribed Drug Classes (SQL — Data Warehouse)**
```sql
SELECT
    d.DrugName,
    d.DrugCategory,
    COUNT(f.MedicationKey) AS TotalPrescriptions,
    COUNT(DISTINCT f.PatientKey) AS UniquePatientsReceived
FROM FactMedication f
JOIN DimDrug d ON f.DrugKey = d.DrugKey
WHERE d.DrugKey <> -1
GROUP BY d.DrugName, d.DrugCategory
ORDER BY TotalPrescriptions DESC;
```

**Same Query — Neo4j (CQL)**
```cypher
MATCH (p:Patient)-[:RECEIVED]->(m:Medication)-[:IS_TYPE]->(d:DrugCategory)
RETURN d.name AS DrugCategory,
       COUNT(m) AS TotalPrescriptions,
       COUNT(DISTINCT p) AS UniquePatients
ORDER BY TotalPrescriptions DESC;
```

---

## 📈 SSRS Reports Produced

| # | Report Title | Key Metric |
|---|---|---|
| 1 | Monthly Prescription Volume by Drug | Trend over admission months |
| 2 | Top 10 High-Frequency Drugs per ICU Unit | Drug demand by care unit |
| 3 | Patient Admission & Medication Duration | Length of stay vs. drug days |
| 4 | Caregiver Prescription Activity Report | Prescriptions per caregiver |

---

## 🎨 Tableau Dashboard

The Tableau dashboard connects directly to **PharmacyDW** and surfaces four visualisations:

- 📉 **Prescription Trend Line** — Volume over time by drug category
- 🗺️ **Drug Frequency Heatmap** — Category × ICU unit cross-tab
- 🍩 **Route of Administration Donut** — IV vs. oral vs. other
- 📦 **Patient Risk Tier Bar Chart** — High/medium/low admission severity

---

## 🔬 Dataset

**MIMIC-III Clinical Database Demo v1.4**
PhysioNet — MIT Lab for Computational Physiology

> MIMIC-III is a large, freely-available database comprising de-identified health-related data associated with over 40,000 patients who stayed in critical care units of the Beth Israel Deaconess Medical Center between 2001 and 2012.

Key tables used: `PRESCRIPTIONS`, `ADMISSIONS`, `PATIENTS`, `INPUTEVENTS_CV`, `CAREGIVERS`, `D_ITEMS`

Access requires credentialed registration at [physionet.org](https://physionet.org/content/mimiciii-demo/1.4/).

---

## 👤 Author

**Abin Raju**
MSc Data Analytics — Dublin Business School (September 2025 cohort)
Module: B9DA111 — Data Storage Solutions for Data Analytics

<p>
  <a href="https://www.linkedin.com/in/YOUR_LINKEDIN_HERE">
    <img alt="LinkedIn" src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white"/>
  </a>
  <a href="https://github.com/abinraju23">
    <img alt="GitHub" src="https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white"/>
  </a>
</p>

---

## ⚠️ Disclaimer

This project was developed as part of an academic assessment at Dublin Business School. The MIMIC-III dataset is de-identified clinical data used strictly for educational and research purposes. This repository does not contain any patient data. All clinical data must be accessed independently through PhysioNet with appropriate credentialing.

---

<div align="center">
  <sub>Built with SQL Server · SSIS · SSRS · Neo4j · Tableau · Visual Studio 2022</sub><br/>
  <sub>© 2026 Abin Raju · MSc Data Analytics · Dublin Business School</sub>
</div>
