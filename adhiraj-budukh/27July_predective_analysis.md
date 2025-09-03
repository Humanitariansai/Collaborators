# Report for 27 July 2025  
**Topic:** Predictive Analytics for Demand Forecasting in Bimride  
**Dummy Project:** Using historical trip data (synthetic) to forecast peak hours  
**Focus:** Linking machine learning with BI dashboards  

---

## 1. Work Done Today (Dummy Project)

### Step 1: Setting Up Synthetic Data
- Created a synthetic dataset simulating **Bimride’s trip records** for the last 6 months.  
- Columns included:  
  - `trip_id`  
  - `date`  
  - `time_of_day`  
  - `pickup_location`  
  - `drop_location`  
  - `ride_duration`  
  - `fare_amount`  
- Generated realistic ride volumes to mimic weekday vs. weekend trends.  

### Step 2: Preprocessing the Data
- Cleaned missing values (e.g., incomplete trips).  
- Converted `time_of_day` into categorical bins like **Morning (6-10AM), Afternoon (10-4PM), Evening (4-8PM), Night (8-12PM)**.  
- Aggregated rides per hour to detect **patterns of demand surges**.  

### Step 3: Applying Machine Learning Model
- Used **time series forecasting (ARIMA and Prophet)** to predict demand peaks.  
- Trained models on the past 6 months of trip data.  
- Identified **recurring demand spikes** during weekdays (7-9 AM & 5-7 PM) and **weekend nightlife spikes** (9 PM – 1 AM).  

### Step 4: Linking with BI Dashboards
- Exported model predictions into a **PostgreSQL database**.  
- Built a **Power BI dashboard** displaying:  
  - Hourly demand forecast  
  - Heatmap of pickup hotspots by time of day  
  - Trendline of predicted vs. actual demand  
- Added filters for **date ranges, day of week, and location zones**.  

### Step 5: Simulating Real-World Application
- Ran "what-if" scenarios:  
  - **Peak pricing optimization** → Predict when surge pricing could be triggered.  
  - **Driver allocation** → Estimate how many drivers are needed per zone.  
- Exported results as **automated reports** (daily demand forecasts).  

---

## 2. Challenges Faced
1. **Synthetic Data Limitations**  
   - The dataset lacked real-world complexity (e.g., weather, local events, or flight arrivals that affect demand).  
   - Solution: Added simulated event spikes (e.g., concerts on Fridays).  

2. **Model Selection**  
   - ARIMA worked well for short-term forecasts but struggled with weekly seasonality.  
   - Prophet handled seasonality better but required more hyperparameter tuning.  

3. **Integration with BI Tools**  
   - Exporting predictions in real-time to Power BI dashboards required setting up **ETL pipelines**.  
   - Challenge was maintaining sync between live trip data and forecast outputs.  

4. **Performance & Scalability**  
   - Scaling predictions across all zones of a city increased compute costs.  
   - Solution: Batched forecasts per zone rather than running all at once.  

---

## 3. Application in Bimride

### a. Driver Supply Optimization
- Forecasted demand allows Bimride to **position drivers in advance** in hotspots (e.g., airports during peak hours).  
- Reduces customer wait time and increases completed rides.  

### b. Dynamic Pricing
- Machine learning models can trigger **automated surge pricing** when demand exceeds supply.  
- Ensures fairness by balancing ride availability with driver incentives.  

### c. Operational Planning
- Predictive analytics helps **plan driver incentives** (bonus hours during high-demand slots).  
- Assists customer support teams by anticipating **service load spikes**.  

### d. Business Intelligence Reporting
- Linking ML outputs to BI dashboards provides management with **real-time insights**.  
- Helps leadership track **demand trends** and make **data-driven decisions**.  

---

## 4. Conclusion
Today’s dummy project demonstrated how predictive analytics, powered by machine learning, can be linked with BI dashboards to forecast ride demand. Despite challenges in data quality and integration, the approach has strong potential for **optimizing driver allocation, reducing wait times, and boosting revenue in Bimride**.  

This experiment provides a foundation for deploying a **full-scale predictive demand forecasting engine** within Bimride’s production environment.

---
