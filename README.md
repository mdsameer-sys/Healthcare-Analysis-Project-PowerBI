# 🏥 Patient Encounter Cost & Risk Analysis in Healthcare Systems

> **Interactive Power BI dashboard analyzing healthcare encounter costs, payer coverage, high-cost patient utilization, procedure trends, and geographic patterns to support financial and operational decision-making.**

---

## 🚀 Project Overview

Healthcare organizations generate large volumes of patient, encounter, procedure, and payer data. Without a consolidated analytical view, it can be difficult to identify **high-cost utilization, financial exposure, payer coverage gaps, and operational patterns**.

This project transforms healthcare records into an interactive Power BI decision-support dashboard. The solution combines Python for initial data cleaning and preparation, SQL Server for data analysis and business-question validation, and Power BI for transformation, data modeling, DAX calculations, and interactive visualization across encounter, patient, procedure, payer, organization, and date information.

---
## 🔗 Live Power BI Dashboard

👉 **[View the Interactive Dashboard](https://app.powerbi.com/view?r=eyJrIjoiNjU3ZDM1ZDItMTgzZi00MjFhLThlYTYtNTgyZDc2NmQwMTcxIiwidCI6ImM2ZTU0OWIzLTVmNDUtNDAzMi1hYWU5LWQ0MjQ0ZGM1YjJjNCJ9)**

The dashboard is designed to answer a practical business question:

> **Where are healthcare costs and utilization concentrated, what is driving financial risk, and which areas require management attention?**


## 🏥 Healthcare Business Problem

Healthcare providers need visibility into both **patient utilization and financial exposure**.

The analysis focuses on several challenges:

- High-cost patient encounters can increase financial and operational pressure.
- Payer coverage gaps can leave a significant portion of claim costs uncovered.
- Different encounter classes can have substantially different cost profiles.
- Procedure costs can vary over time and by diagnosis/reason.
- Geographic differences in patient encounters can reveal areas of higher utilization.
- Repeated high-cost encounters may require targeted care-management review.

The project therefore brings these dimensions together into a single analytical environment.

---

## 🎯 Business Objectives

The Power BI solution was designed around five core analytical requirements.

### 1. Encounter Cost Distribution

Analyze the distribution of **base encounter cost and total claim cost** across encounter classes such as:

- Ambulatory
- Emergency
- Inpatient
- Outpatient
- Urgent Care
- Wellness

**Business question:**  
Which encounter classes contribute most to healthcare cost, and how does average cost differ across them?

### 2. High-Cost Patient Identification

Identify patients with repeated high-cost encounters and quantify their contribution to total claim cost.

**Business question:**  
Which patients show recurring high-cost utilization and may require targeted care-management attention?

### 3. Uncovered Costs by Payer & Reason

Analyze payer coverage against total claim cost and identify uncovered financial exposure across payer and diagnosis/reason combinations.

**Business question:**  
Which payer groups and encounter reasons contribute most to uncovered healthcare costs?

### 4. Procedure Cost Trends & Diagnosis Correlation

Analyze procedure costs over time and evaluate how procedure expenses vary across diagnosis/reason categories.

**Business question:**  
Which procedure/reason categories are associated with higher costs, and how does procedure cost change over time?

### 5. Geographic Analysis of Encounters & Cost

Map patient encounter activity using geographic coordinates and compare encounter volume with average encounter cost.

**Business question:**  
Where are patient encounters concentrated, and which locations show higher average encounter costs?

---

## 📊 Dataset

The dashboard uses five healthcare source tables plus a dedicated date dimension.

| Table | Records | Business Purpose |
|---|---:|---|
| `encounters` | **27,891** | Encounter activity, encounter class, claim cost, payer coverage and reason codes |
| `procedures` | **47,701** | Procedures, procedure costs and associated reason codes |
| `patients` | **974** | Patient demographic and geographic information |
| `payers` | **10** | Insurance/payer information |
| `organizations` | **1** | Healthcare organization details |
| `Dim_Date` | Derived | Date and time-based analysis |

### Key Encounter Fields

- `START`
- `STOP`
- `PATIENT`
- `ORGANIZATION`
- `PAYER`
- `ENCOUNTERCLASS`
- `TOTAL_CLAIM_COST`
- `PAYER_COVERAGE`
- `REASONCODE`
- `REASONDESCRIPTION`

### Key Procedure Fields

- `START`
- `STOP`
- `PATIENT`
- `ENCOUNTER`
- `CODE`
- `DESCRIPTION`
- `BASE_COST`
- `REASONCODE`
- `REASONDESCRIPTION`

### Patient Attributes

The patient table provides demographic and geographic dimensions including:

- Gender
- Race
- Ethnicity
- Marital status
- City
- State
- County
- Latitude
- Longitude

---

## 🛠️ Tools & Technologies

| Tool / Technology | Purpose |
|---|---|
| **Python** | Initial data cleaning and preparation |
| **Power BI Desktop** | Dashboard development and interactive visualization |
| **Power Query** | Data preparation and transformation |
| **DAX** | KPI calculations and analytical measures |
| **SQL Server / T-SQL** | Source analysis and business-question validation |
| **CSV** | Source healthcare datasets |
| **Power BI Data Model** | Relational analysis across healthcare tables |

---

## 🧹 Data Preparation


The raw healthcare datasets were prepared through a multi-stage data preparation workflow before being used for analysis and dashboard development.

Python (Pandas) — Initial Data Cleaning

Python and Pandas were used for initial data cleaning and preparation of the raw healthcare datasets before the analytical workflow.

SQL Server — Data Analysis

SQL Server was used to explore the relational datasets, validate business questions, and perform analytical queries across healthcare tables.

Power Query — Additional Transformation

Power Query was used within Power BI for additional transformation and preparation required for the reporting and analytical model.

### Key Preparation Activities

- Reviewed the five source tables and their relationships.
- Standardized field types for analytical use.
- Converted encounter and procedure timestamps into usable date/time fields.
- Created a dedicated `Dim_Date` table for time-based analysis.
- Prepared patient latitude and longitude for geographic visualization.
- Connected payer and organization identifiers to encounter records.
- Connected procedure records to their corresponding encounters and patients.
- Validated cost and coverage fields before KPI creation.
- Prepared business-friendly fields for Power BI visuals and measures.

The preparation stage ensured that the dashboard could support **consistent filtering, aggregation, and cross-table analysis**.

---

## 🗂️ Data Model

The Power BI model contains the five healthcare source tables and a dedicated date dimension.

### Model Components

**Core healthcare tables**

- `encounters`
- `patients`
- `procedures`
- `payers`
- `organizations`

**Analytical tables**

- `Dim_Date`
- `key_measures`

The model connects encounter activity with patient, payer, organization, procedure, and date information, allowing the dashboard to analyze healthcare performance from multiple perspectives.

### Analytical Relationship Flow

```text
                 Dim_Date
                    │
                    ▼
Patients ─────► Encounters ◄───── Payers
    │               │
    │               │
    │               ▼
    └──────────► Procedures

              Organizations
                    │
                    ▼
                 Encounters
```

### Modeling Principles

- Relational table design
- Centralized date dimension
- Reusable DAX measure layer
- Consistent filter propagation
- Separation of source data from analytical measures
- Cross-table analysis using business keys

---

## 📐 KPI Framework

The dashboard uses a dedicated `key_measures` table to organize analytical measures.

### 💰 Financial KPIs

#### Total Claim Cost

Measures the total healthcare claim amount across the selected analysis context.

**Dataset total:** approximately **$101.51M**

#### Total Payer Coverage

Measures the amount of claim cost covered by payers.

**Dataset total:** approximately **$31.10M**

#### Financial Risk / Uncovered Cost

Calculated as:

**Financial Risk = Total Claim Cost − Payer Coverage**

**Dataset total:** approximately **$70.42M**

#### Average Encounter Cost

Measures the average total claim cost per encounter.

**Dataset average:** approximately **$3.64K**

---

## 📊 Dashboard Design

The Power BI report contains two analytical pages.

### Page 1 — Cost & Encounter Overview

![Alt text](https://github.com/mdsameer-sys/Healthcare-Analysis-Project-PowerBI/blob/b3e9aeceb00f493bca262eb0f33009502a6d9616/cost_encounter_overview)

This page provides the primary healthcare cost and utilization view.

#### KPI Cards

- Total Claim Cost
- Total Payer Coverage
- Financial Risk
- Average Encounter Cost

#### Encounter Cost Analysis

Analyzes **base encounter cost and total claim cost by encounter class**.

This enables comparison of cost patterns across inpatient, ambulatory, emergency, outpatient, urgent-care, and wellness encounters.

#### High-Cost Patient Analysis

A patient-level view highlights:

- Patient name
- Number of high-cost encounters
- Total claim cost
- Contribution percentage

This supports identification of recurring high-cost utilization.

#### Payer & Reason Analysis

A detailed view evaluates:

- Payer
- Reason
- Payer Coverage
- Uncovered Cost
- Uncovered %

This provides visibility into financial exposure by payer and diagnosis/reason.

---

### Page 2 — Cost Trends & Geographic Insights

![Alt text](https://github.com/mdsameer-sys/Healthcare-Analysis-Project-PowerBI/blob/c330789c7c9b151750d08a7ef0d1b9efcc9dc602/cost_trend_geographic)

The second page focuses on **time trends, procedures, payer performance, and geographic patterns**.

#### Procedure Cost Trend

Tracks procedure base cost over time using the date dimension.

#### Dynamic Procedure Analysis

The dashboard supports dynamic **Top/Bottom analysis** of procedure/reason categories using an interactive parameter.

This allows users to switch between higher- and lower-cost categories instead of relying on a fixed ranking.

#### Geographic Analysis

Patient city coordinates are used to visualize:

- Encounter volume
- Average encounter cost
- Geographic distribution of healthcare activity

#### Payer Comparison

Payer-level metrics allow users to compare claim cost and coverage performance.

---

## 🎛️ Interactive Features

The dashboard is designed for exploration rather than static reporting.

Key capabilities include:

- Year slicer
- Payer filtering
- Encounter-class filtering
- Dynamic Top/Bottom selection
- Parameter-driven analysis
- Interactive map
- Cross-filtering between visuals
- KPI cards
- Dynamic titles
- Detailed patient-level analysis
- Drill-oriented visual exploration

---

## 💡 Key Insights & Findings

### 💰 1. Significant Uncovered Financial Exposure

Across the dataset:

- **Total Claim Cost:** ~$101.51M
- **Payer Coverage:** ~$31.10M
- **Uncovered Cost / Financial Risk:** ~$70.42M

This means a substantial portion of total claim cost remains outside payer coverage in the analyzed records.

**Business implication:** payer coverage and reimbursement patterns represent a major area for financial-risk monitoring.

---

### 🏥 2. Inpatient Encounters Had the Highest Average Cost

Average claim cost by encounter class shows inpatient encounters as the most expensive on a per-encounter basis.

| Encounter Class | Avg. Claim Cost |
|---|---:|
| **Inpatient** | **~$7.76K** |
| Urgent Care | ~$6.37K |
| Emergency | ~$4.63K |
| Wellness | ~$4.26K |
| Ambulatory | ~$2.89K |
| Outpatient | ~$2.24K |

Although ambulatory encounters have much higher volume, inpatient encounters have the highest average cost.

---

### 🚨 3. 287 Patient-Year Records Showed Repeated High-Cost Utilization

The analysis identified **287 patient-year records** where patients had more than **3 encounters in a year**, with each qualifying encounter exceeding the **$10,000 claim-cost threshold**.

One patient-year reached **42 qualifying high-cost encounters**, demonstrating the potential value of targeted utilization review.

---

### 🏦 4. Payer Coverage Varied Significantly

The dataset shows substantial differences in uncovered claim percentages across payers.

Examples:

| Payer | Uncovered % |
|---|---:|
| **NO_INSURANCE** | **100.00%** |
| **Anthem** | **100.00%** |
| Cigna Health | ~99.96% |
| Humana | ~99.94% |
| Aetna | ~99.93% |
| UnitedHealthcare | ~99.85% |
| Blue Cross Blue Shield | ~30.90% |
| Medicare | ~22.04% |
| Dual Eligible | ~10.75% |
| Medicaid | ~5.99% |

**Business implication:** payer-level coverage differences can help prioritize reimbursement and financial-risk investigations.

---

### 🩺 5. Normal Pregnancy Was the Largest Reason-Code Financial Exposure

**Normal pregnancy** generated approximately **$13.41M in uncovered cost**, making it the largest uncovered-cost reason category in the dataset.

This demonstrates that financial exposure can be concentrated in specific healthcare conditions rather than being evenly distributed across all reasons.

---

### 🔁 6. Repeated Procedure Patterns Were Identified

The analysis identified **291 patient–reason combinations** involving multiple procedures across different encounters for the same reason code.

These patterns can be reviewed to understand whether repeated procedures represent expected ongoing treatment or opportunities for utilization management.

---

### 📍 7. Geographic Analysis Enables Location-Based Monitoring

The dashboard uses patient latitude and longitude to visualize encounter activity by city.

This allows stakeholders to compare **patient traffic and average encounter cost geographically**, helping identify locations with relatively high utilization or cost.

---

### ⏱️ 8. Inpatient Encounters Had the Longest Average Duration

Average encounter duration was approximately:

- **Inpatient:** ~36.8 hours
- Ambulatory: ~9.5 hours
- Outpatient: ~5.9 hours
- Emergency: ~1.5 hours

The analysis also identified encounters exceeding the **24-hour threshold**, providing a basis for operational review of extended stays.

---

## 💼 Business Recommendations

### 1. Prioritize Payer Coverage Review

Investigate payer groups with consistently high uncovered percentages to understand reimbursement, eligibility, or coverage-related gaps.

### 2. Monitor Recurring High-Cost Patients

Create a recurring utilization-monitoring process for patient-year groups with multiple high-cost encounters.

### 3. Review High-Exposure Reason Codes

Prioritize diagnosis/reason categories contributing the largest uncovered costs, with **Normal pregnancy** being the leading category in this dataset.

### 4. Monitor Inpatient Utilization

Because inpatient encounters have the highest average claim cost and longest average duration, extended inpatient activity should be monitored for operational opportunities.

### 5. Investigate Repeated Procedures

Use the repeated-procedure patterns to support clinical utilization review and distinguish necessary recurring treatment from potentially avoidable repetition.

### 6. Use Geographic Insights for Resource Planning

Use encounter volume and average cost by location to support resource allocation and identify areas requiring additional operational attention.

---


## 🏁 Conclusion

**Patient Encounter Cost & Risk Analysis in Healthcare Systems** demonstrates how Power BI can transform relational healthcare data into an interactive business intelligence solution.

By combining **financial KPIs, patient utilization, payer coverage, procedure trends, encounter duration, and geographic analysis**, the dashboard provides a consolidated view of healthcare cost and risk.

The solution helps stakeholders move from **raw healthcare records → analytical insights → targeted financial and operational decisions**.

---

## ⭐ Portfolio Highlight

**Power BI | DAX | Power Query | Data Modeling | SQL Server | Healthcare Analytics**

> **Analyzed 27.9K+ encounters and 47.7K+ procedures to quantify ~$101.5M in claim costs, ~$70.4M in uncovered financial exposure, identify 287 high-cost patient-year records, and surface payer, procedure, utilization, and geographic risk patterns through an interactive Power BI dashboard.**
