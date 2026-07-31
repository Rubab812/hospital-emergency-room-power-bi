# Hospital Emergency Room Dashboard

!\[Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?logo=powerbi\&logoColor=black)
!\[Power Query](https://img.shields.io/badge/Power%20Query-Data%20Preparation-217346)
!\[DAX](https://img.shields.io/badge/DAX-Data%20Analysis-16324F)
!\[Status](https://img.shields.io/badge/Status-Portfolio%20Project-1F7A8C)

## Project Overview

This project is an interactive **Hospital Emergency Room Dashboard** developed in Microsoft Power BI.

The report analyzes emergency-room activity across patient volume, waiting time, admission status, department referrals, patient demographics, and satisfaction. It is designed to help stakeholders monitor operational performance, identify service bottlenecks, and support data-driven staffing and process-improvement decisions.

The current Power BI report contains three pages:

1. **Monthly View**
2. **Consolidated View**
3. **Patient Details**

\---

## Business Objectives

The dashboard was developed to answer the following business questions:

* How many patients visit the emergency room?
* What is the average patient waiting time?
* What percentage of patients are seen within 30 minutes?
* What is the average patient satisfaction score?
* How many patients are admitted?
* How many patients are referred to other departments?
* Which departments receive the highest number of referrals?
* How does patient volume vary by month, weekday, day, and time band?
* Which patient groups experience longer waiting times?
* How can patient-level records be investigated using filters and slicers?

\---

## Key Performance Indicators

|KPI|Description|
|-|-|
|Total Patients|Number of emergency-room visits in the selected period|
|Average Wait Time|Average patient waiting time in minutes|
|Seen Within 30 Minutes|Percentage of visits handled within 30 minutes|
|Average Satisfaction|Average available patient satisfaction score|
|Admission Rate|Percentage of patients admitted|
|Referral Rate|Percentage of patients referred to a department|
|Referred Patients|Number of patients referred to another department|

\---

## Dashboard Pages

### 1\. Monthly View

The Monthly View provides a single-month operational summary.

Main visuals include:

* Patient KPI with month-over-month comparison
* Average wait KPI
* Percentage seen within 30 minutes
* Average satisfaction KPI
* Referred-patient KPI
* Daily patient volume area chart
* Admission-status donut chart
* Gender distribution
* Department referral ranking
* Patient age distribution
* Day-and-time heatmap

!\[Monthly View](images/monthly\_view.png)

\---

### 2\. Consolidated View

The Consolidated View provides an aggregated summary for a selected date range.

Main visuals include:

* Total patient count
* Average wait time
* Percentage seen within 30 minutes
* Average satisfaction score
* Admission rate
* Referral rate
* Monthly patient volume and average wait
* Admission status by month
* Visits by weekday
* Referral volume by department
* Department referral treemap

!\[Consolidated View](images/consolidated\_view.png)

\---

### 3\. Patient Details

The Patient Details page supports detailed filtering and record-level analysis.

Main features include:

* Selected-patient count
* Admitted-patient count
* Not-admitted count
* Average wait time
* Date-range filter
* Patient search
* Gender filter
* Age-band filter
* Department filter
* Admission-status filter
* Reset Filters button
* Patient detail table
* Wait-time distribution
* Top referral departments

!\[Patient Details](images/patient\_details.png)

\---

## Data Model

The report uses a simple star-schema-style model with:

* A primary **ER Visits** fact table
* A dedicated **Date** table
* A one-to-many relationship from `Date\[Date]` to `ER Visits\[Admission Date]`
* Single-direction filtering from Date to ER Visits

!\[Data Model](images/data\_model.png)

\---

## Dataset Summary

The source dataset contains emergency-room visit records covering approximately:

* **9,216 visits**
* **April 2023 to October 2024**
* Patient demographics
* Admission date and time
* Wait time
* Admission status
* Department referrals
* Satisfaction score

\---

## Data Preparation

Data preparation was completed in Power Query.

The main transformation steps included:

1. Connecting to the original CSV file
2. Promoting headers
3. Removing unnecessary or sensitive columns
4. Renaming columns
5. Trimming and cleaning text values
6. Converting admission date and time using the correct locale
7. Assigning appropriate data types
8. Replacing missing or inconsistent department values
9. Creating admission status
10. Creating age bands and sort columns
11. Creating wait-time bands and sort columns
12. Creating time bands
13. Creating a dedicated admission date
14. Creating privacy-safe patient identifiers
15. Loading the final dataset into the Power BI model

\---

## DAX Measures

Examples of measures used in the report are shown below.

### Total Patients

```DAX
Total Patients =
DISTINCTCOUNT('ER Visits'\[Patient ID])
```

### Average Wait Time

```DAX
Average Wait Time (Min) =
AVERAGE('ER Visits'\[Wait Time (Min)])
```

### Patients Within 30 Minutes

```DAX
Patients Within 30 Min =
CALCULATE(
    \[Total Patients],
    KEEPFILTERS('ER Visits'\[Wait Time (Min)] <= 30)
)
```

### Patients Within 30 Minutes Percentage

```DAX
Patients Within 30 Min % =
DIVIDE(
    \[Patients Within 30 Min],
    \[Total Patients]
)
```

### Admitted Patients

```DAX
Admitted Patients =
CALCULATE(
    \[Total Patients],
    KEEPFILTERS('ER Visits'\[Admission Flag] = TRUE())
)
```

### Admission Rate

```DAX
Admission Rate =
DIVIDE(
    \[Admitted Patients],
    \[Total Patients]
)
```

### Referred Patients

```DAX
Referred Patients =
CALCULATE(
    \[Total Patients],
    KEEPFILTERS('ER Visits'\[Department Referral] <> "Not Referred")
)
```

### Referral Rate

```DAX
Referral Rate =
DIVIDE(
    \[Referred Patients],
    \[Total Patients]
)
```

\---

## Key Findings

Based on the full reporting period:

* The dashboard contains approximately **9,216 emergency-room visits**.
* Average patient wait time is approximately **35.3 minutes**.
* Approximately **40.7%** of patients were seen within 30 minutes.
* Approximately **59.3%** waited longer than 30 minutes.
* The admission rate is approximately **50%**.
* The referral rate is approximately **41.4%**.
* Saturday recorded the highest total visit volume.
* General Practice and Orthopedics received the highest referral volumes.
* Satisfaction results should be interpreted carefully because only a portion of visits contain a satisfaction response.

\---

## Recommended Actions

* Review staffing levels during high-volume weekdays and time bands.
* Investigate the operational causes of waits longer than 30 minutes.
* Review referral workflows for high-volume departments.
* Track department-level wait times and referral turnaround.
* Improve satisfaction-response coverage.

\---

## Tools and Technologies

* Microsoft Power BI Desktop
* Power Query
* DAX
* CSV
* Microsoft PowerPoint
* Git
* GitHub

\---

## How to Open the Project

1. Clone or download this repository.
2. Open the `.pbix` file in Microsoft Power BI Desktop.
3. If the data source cannot be found, update the CSV path:

   * Open **File**
   * Select **Options and settings**
   * Select **Data source settings**
   * Update the source path
4. Select **Refresh**.

Use the slicers and navigation buttons to explore the report.

