# Report: Building Executive Analytics Dashboard in Power BI (Power Query & DAX)
**Date:** 1 – 7 November  
**Topics:**  
1. Executive Dashboard Design for Business Analytics  
2. Data Modeling and Transformation using Power Query  
3. Advanced DAX Measures and Measure Table Design  

---

## Overview
This week focused on building a **high-level executive analytics dashboard in Power BI** for BimRide, designed to support leadership decision-making across operations, growth, and performance monitoring.  
The emphasis was on creating **clear, reliable, and scalable reporting** over a large analytical dataset, rather than one-off visualizations.

Work centered around structuring multiple reports, designing a dedicated **Measure Table**, and implementing **DAX-based calculations** to ensure metric consistency, performance, and reusability across dashboards.

---

## Project Work (Step by Step)

### Part 1: Dashboard Planning and Executive Requirements

#### Step 1: Defining Executive KPIs
- Identified core executive-level metrics such as trips, revenue, growth trends, cancellations, and utilization.  
- Focused on **decision-oriented KPIs** rather than operational noise.  
- Structured reports to answer “what changed,” “why it changed,” and “where to act.”  

#### Step 2: Report Structure and Layout
- Designed multiple report pages aligned to executive use cases (overview, trends, comparisons).  
- Prioritized clarity, minimalism, and consistent visual hierarchy.  
- Ensured dashboards remained intuitive even with large underlying datasets.  

---

### Part 2: Data Transformation with Power Query

#### Step 3: Data Preparation and Shaping
- Used **Power Query** to clean, standardize, and transform data from multiple analytical tables.  
- Applied transformations at the query layer to reduce downstream DAX complexity.  
- Standardized date handling, categorical fields, and numeric formats for consistency.  

#### Step 4: Scalable Data Model Design
| **Modeling Area** | **Approach** | **Benefit** |
|---|---|---|
| Star Schema | Fact and dimension separation | Improved performance |
| Relationship Design | Clear cardinality and filters | Predictable aggregations |
| Pre-Aggregation | Query-level shaping | Faster report load times |
| Reusable Queries | Centralized transformations | Easier maintenance |

- Designed the model to support **multiple reports without duplication**.  

---

### Part 3: DAX Measures and Measure Table

#### Step 5: Measure Table Strategy
- Created a **dedicated Measure Table** to store all DAX calculations.  
- Centralized metric logic to avoid inconsistencies across reports.  
- Structured measures by category (core KPIs, growth, efficiency, ratios).  

#### Step 6: Advanced DAX Calculations
| **Measure Category** | **Purpose** | **Business Value** |
|---|---|---|
| Core Metrics | Standard KPIs | Single source of truth |
| Time Intelligence | YoY, MoM, trends | Executive performance tracking |
| Ratios & Rates | Efficiency indicators | Better comparability |
| Conditional Logic | Status-based metrics | Accurate segmentation |

- Implemented DAX for **every calculation**, avoiding hard-coded values.  
- Optimized measures for performance and readability.  

---

## Challenges Faced
1. **Metric Consistency** – Ensuring the same KPI definition across multiple reports.  
2. **DAX Complexity** – Managing a large number of interdependent measures.  
3. **Performance Optimization** – Balancing rich calculations with dashboard responsiveness.  
4. **Executive Usability** – Presenting complex data in a simple, decision-ready format.  

---

## BimRide Application (Ride-Hailing)

### Executive Visibility
The Power BI executive dashboard provides leadership with a consolidated view of business performance, enabling faster, data-driven decisions without manual reporting effort.

### Scalable Reporting Framework
By using Power Query for transformations and a centralized DAX Measure Table, BimRide can easily extend reporting to new metrics and datasets without rework.

### Trusted Decision-Making
Consistent DAX-driven KPIs ensure that executives, operations, and analytics teams all reference the same numbers, reducing misalignment and confusion.

---

## Conclusion
This week’s work demonstrated how **Power BI can support executive analytics at scale** when supported by strong data modeling, Power Query transformations, and disciplined DAX design.  
The combination of multiple report views and a centralized Measure Table ensures consistency, performance, and long-term maintainability.

This dashboard framework positions BimRide to scale executive reporting as data volume, business complexity, and analytical needs continue to grow.
