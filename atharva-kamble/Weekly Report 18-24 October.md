# Weekly Report: Pricing Fairness, Dashboards and Cross Model Documentation  
**Date:** October 18 to October 24  
**Topics Covered:**  
1. Pricing Fairness Prototype Refinement  
2. Dashboard Integration in BimRide Analytics Workspace  
3. Cross Model Outcome Documentation  

## Overview
This week was planned as the follow up to the earlier work on retention, incentive simulation and support forecasting.  
The focus moved from only running models to making them usable in practice through pricing fairness logic, shared dashboards and cross model documentation.  

All three goals faced blockers.  
Progress this week was mainly about surfacing missing data, unclear rules and technical gaps so that these can be solved cleanly in the next sprint.

---

## Day 1: Pricing Fairness Scope Review  

### Overview  
Revisited the goal of refining the pricing fairness prototype after the previous work on driver and rider balance.  

### Work Done  
1. Reviewed earlier simulation notes to understand current pricing behaviour.  
2. Listed all variables required for fairness such as distance, time window, demand zone and driver supply.  
3. Mapped which variables are already available from existing data and which ones are missing or noisy.  

### Blocker  
Key inputs are incomplete or inconsistent, which makes any new fairness rule impossible to trust.  

### Impact  
The team now has a clear view of what data must be fixed or added before pricing fairness can move forward.

---

## Day 2: Data Quality Check for Pricing Inputs  

### Overview  
Focused on checking the quality of trip and event data needed for pricing refinement.  

### Work Done  
1. Sampled trip records to compare expected fields against actual stored values.  
2. Noted gaps in demand clustering signals and driver availability markers.  
3. Recorded places where timestamps or locations are not reliable enough for fairness testing.  

### Blocker  
Without clean and stable data, any pricing prototype would give misleading results, so refinement is on hold.  

### Impact  
The week produced a concrete list of data issues that must be solved before pricing work can be resumed.

---

## Day 3: Dashboard Metric Mapping  

### Overview  
Attempted to start the integration of dashboards in the BimRide analytics workspace for retention, support and pricing.  

### Work Done  
1. Drafted a first pass layout for a shared operational dashboard.  
2. Listed core metrics for each area such as driver retention rate, forecast accuracy and pricing behaviour.  
3. Checked which metrics have stable output formats from the existing models.  

### Blocker  
Retention and forecasting models are running, but their outputs are not yet standardized into a common schema that a dashboard can use directly.  

### Impact  
Integration is blocked, but the requirements for metric format and structure are now clearly described.

---

## Day 4: Analytics Workspace Access and Schema Review  

### Overview  
Tried to connect real model outputs into the analytics workspace.  

### Work Done  
1. Tested sample connections from the existing data store to the analytics tool.  
2. Verified which tables and views are visible and which are still restricted.  
3. Compared schemas from retention, forecasting and pricing to see where they do not match.  

### Blocker  
Access permissions and schema differences prevent a single dashboard from pulling all three areas into one view.  

### Impact  
A short list of access changes and schema alignment tasks is now ready for the next sprint.

---

## Day 5: Cross Model Documentation Outline  

### Overview  
Started working on documentation to explain how retention, forecasting and pricing are expected to work together.  

### Work Done  
1. Collected previous weekly reports on retention, incentive simulation and support forecasting.  
2. Outlined a cross model document with sections for inputs, outputs and dependencies.  
3. Noted where pricing and dashboards are still too early to document as final behaviour.  

### Blocker  
Since pricing refinement and dashboard integration are blocked, any full documentation would be outdated quickly or simply wrong, so only an outline can be created for now.  

### Impact  
A skeleton structure exists, but final content must wait until the blocked tasks are unblocked.

---

## Day 6: Evaluation Criteria Draft  

### Overview  
Looked at how future evaluation of the three systems should be done once everything is running.  

### Work Done  
1. Brainstormed possible evaluation metrics such as retention uplift, ticket forecast accuracy and pricing satisfaction.  
2. Tried to link these metrics to business outcomes such as rider trust and driver earnings stability.  
3. Marked which metrics still need leadership input before they can be used as formal targets.  

### Blocker  
No confirmed evaluation framework from leadership yet, so cross model documentation and scoring cannot be finalized.  

### Impact  
The gaps are identified and can be addressed next week through clearer alignment.

---

## Day 7: Weekly Review and Blocker Summary  

### Overview  
Closed the week by reviewing why all three goals remain blocked and what must change next.  

### Work Done  
1. Summarized data issues that impact pricing refinement.  
2. Listed all schema and access problems that stop dashboard work.  
3. Collected open questions that must be answered before documentation can be completed.  

### Blocker  
No change in blocker status, but the unknowns are now written down instead of being vague.  

### Impact  
Next week can focus on solving the specific blockers instead of guessing.
