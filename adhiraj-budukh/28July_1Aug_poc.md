# Report for 28 July to August1 2025  
**Topic:** Driver Incentive Programs Powered by Data Insights  
**Dummy Project:** Designing a rewards program and simulating driver engagement data  
**Focus:** Measuring impact with BI metrics (driver retention, availability)  

---

## 1. Work Done Today (Dummy Project)

### Step 1: Designing the Rewards Program
- Drafted a **multi-tier incentive system** for drivers:  
  - **Tier 1 – Bronze:** Complete 30 rides/week → $20 bonus  
  - **Tier 2 – Silver:** Complete 50 rides/week → $40 bonus  
  - **Tier 3 – Gold:** Complete 80 rides/week → $75 bonus + priority ride dispatch  
- Added **non-monetary rewards** such as recognition badges, leaderboard rankings, and exclusive driver perks (e.g., fuel vouchers).  

### Step 2: Simulating Driver Engagement Data
- Created a **synthetic dataset** with 500 drivers.  
- Columns included:  
  - `driver_id`  
  - `rides_completed` (weekly)  
  - `tier_achieved`  
  - `bonus_amount`  
  - `driver_availability_hours`  
  - `driver_retention_status` (active vs. churned)  
- Simulated driver performance across 8 weeks.  
- Injected variability to reflect **different driving patterns** (part-time vs. full-time drivers).  

### Step 3: Analyzing Engagement Patterns
- Used **Python + Pandas** to calculate:  
  - % of drivers in each tier per week.  
  - Average driver retention across weeks.  
  - Correlation between incentives earned and **driver availability hours**.  
- Found that **Gold tier drivers contributed 40% more availability hours** than non-participants.  

### Step 4: BI Dashboard Setup
- Loaded simulated dataset into **Power BI**.  
- Created visuals for:  
  - **Driver Retention Trend:** % of drivers active over 8 weeks.  
  - **Incentive Participation Rate:** Share of drivers in Bronze/Silver/Gold.  
  - **Impact on Availability:** Avg. driver online hours vs. incentive tier.  
- Configured **DAX measures** to track KPIs:  
  - Retention Rate = Active Drivers ÷ Total Drivers  
  - Availability Increase % = (Hours w/ Incentives – Hours w/o Incentives) ÷ Hours w/o Incentives  

### Step 5: Scenario Testing
- Simulated outcomes of adjusting thresholds:  
  - Lowering Bronze threshold (20 rides/week) → +15% participation, but reduced profitability.  
  - Increasing Gold payout → Boosted top-tier retention but increased incentive cost.  

---

## 2. Challenges Faced

1. **Balancing Incentives with Profitability**  
   - Too generous → drivers earn more, but margins shrink.  
   - Too strict → drivers disengage, retention drops.  
   - Needed multiple scenario tests to find balance.  

2. **Synthetic Data Limitations**  
   - Engagement behavior lacked factors like **weather, local events, or competing apps**.  
   - Hard to fully capture **real-world churn drivers**.  

3. **Attribution of Impact**  
   - Difficult to prove whether **retention was due to incentives** or other factors (e.g., seasonal demand).  
   - Solution: Designed control vs. experiment groups in simulation.  

4. **Data Integration into BI**  
   - Configuring **calculated measures in Power BI** (e.g., retention vs. availability) was challenging.  
   - Required fine-tuned DAX queries for accurate KPI tracking.  

---

## 3. Application in Bimride

### a. Driver Retention
- Bimride can use **data-driven incentive programs** to reduce churn by rewarding consistent drivers.  
- Example: Target **new drivers in their first 3 months** with tiered rewards to increase early retention.  

### b. Driver Availability
- Linking incentives to **peak-hour availability** ensures enough drivers during high-demand times.  
- Example: Bonus for completing 10 rides in morning rush hours.  

### c. Cost Optimization
- BI dashboards enable leadership to **track ROI of incentive programs**.  
- Insights help optimize thresholds to **maximize retention at lowest cost**.  

### d. Continuous Improvement
- Feedback loops can be embedded where:  
  - Drivers rate the fairness of incentives.  
  - Data insights update the incentive thresholds monthly.  
- Ensures the program remains **adaptive and effective**.  

---

## 4. Conclusion
Today’s dummy project highlighted the potential of **driver incentive programs powered by BI metrics**. By simulating engagement data, designing dashboards, and testing scenarios, I demonstrated how incentives can **boost driver retention and availability**. For Bimride, this approach could lead to **fewer ride cancellations, shorter passenger wait times, and stronger driver loyalty**, all while maintaining profitability.  

This framework lays the foundation for a **dynamic incentive engine** that adapts to market conditions and driver behaviors.

---
