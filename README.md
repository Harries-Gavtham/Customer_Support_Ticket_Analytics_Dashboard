# Customer_Support_Ticket_Analytics_Dashboard

<img width="1291" height="652" alt="image" src="https://github.com/user-attachments/assets/b68cc061-8dc0-4ae0-b82e-4b6efeae2a7b" />

## 📄 Project Overview
Designed a single-page executive dashboard to monitor 15,000+ support interactions, tracking SLA Compliance, CSAT, and Resolution Time.

**Live Project File:** (Customer Support Ticket Analysis.pbix)

**Key Scope:**
* **Data State:** 100% Closed Tickets (Historical Data Analysis).
* **Focus Area:** Service Level Agreement (SLA) adherence and Category-based root cause analysis.

## 🛠️ Technical Workflow
* **Tool:** Microsoft Power BI Desktop
* **Data Transformation (Power Query):**
    * Filtered for valid 'Closed' ticket data to ensure accurate `Resolution Time` calculation.
    * Calculated `Resolution Hours` as a precise duration between Ticket Creation and Close Time.
* **DAX Measures:**
    * **SLA Compliance %:** dynamic calculation utilizing `KEEPFILTERS` to allow deep-diving into "Breached" datasets without context errors.
    * **Avg Resolution Hours:** Average time-to-close for completed tickets.

## 📊 Dashboard Breakdown
The report is designed as a focused **Single-Page Executive View**.

### 1. The "Scoreboard" (KPI Cards)
Located at the top for immediate visibility:
* **Total Tickets:** (Volume)
* **Avg Resolution Hours:** (Speed)
* **Avg CSAT:** (Quality)
* **SLA Compliance %:** (Reliability)

### 2. The Controls (Slicers)
Allows the user to "slice and dice" the data by:
* **Ticket Date:** To isolate specific months or quarters.
* **Priority Level:** To separate *Critical* issues from *Low* priority requests.
* **SLA Status:** To filter explicitly for "Breached" tickets and analyze the root causes of failure.

### 3. Visual Insights
* **Trend Analysis (Line & Clustered Column Chart):**
    * *Visual:* Total Tickets (Bars) vs. SLA Compliance % (Line) by Month.
    * *Insight:* Reveals correlations between workload and performance. (e.g., "Did SLA compliance drop when volume peaked in December?").
* **Root Cause Analysis (Stacked Bar Chart):**
    * *Visual:* Total Tickets by Issue Category.
    * *Insight:* Identifies which specific technical topics (e.g., "Login Error" vs. "Hardware") drive the most volume and which are most prone to SLA breaches.

## 🛠️ Tech Stack
* **Tool:** Microsoft Power BI Desktop
* **ETL & Cleaning:** Power Query Editor
* **Language:** DAX (Data Analysis Expressions)

## ⚙️ Key Technical Steps
### 1. Data Cleaning (Power Query)
* **Sanitized Timestamps:** Filtered out null resolution times and negative duration values caused by system logging errors to ensure statistical accuracy.
* **Duration Logic:** Created a custom `Resolution Hours` column to measure precise handling time.

### 2. Business Logic Engineering (DAX)
* **Dynamic SLA Target:** Engineered a conditional column to assign dynamic targets based on priority:
    * *Critical* = 4 Hours
    * *High* = 24 Hours
    * *Medium* = 48 Hours
    * *Low* = 72 Hours
* **SLA Compliance Measure:** Created a DAX measure using `KEEPFILTERS` to accurately calculate compliance percentages even when sliced by "Breached" status.
    ```dax
    SLA Compliance % =
    VAR MetCount = CALCULATE([Total Tickets], KEEPFILTERS(Tickets[SLA_Status] = "Met"))
    RETURN DIVIDE(MetCount, [Total Tickets], 0)
    ```

## 🔍 Key Insights Discovered
Engineered DAX measures to calculate SLA Adherence based on dynamic priority targets (4hr/24hr/48hr/72hr).
Detected that Technical Issue tickets caused 35% of SLA breaches, highlighting a critical training gap.

---
*Created by Harries Gavtham*
