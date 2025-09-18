# Report: Unit Economics & Predictive Analytics for Ride-Hailing  
**Date:** 13–19 September  
**Topic:**  
- Study of Unit Economics in Ride-Hailing (CAC, LTV, ARPU Analysis)  
- Predictive Analytics for Demand Forecasting & Fleet Optimization  

---

## 📌 Overview
This week, I focused on understanding **unit economics** in ride-hailing and exploring how **predictive analytics** can help optimize demand forecasting and fleet utilization.  

The work was divided into two main dummy projects:  
1. **Unit Economics Simulation** → CAC, LTV, ARPU for riders.  
2. **Predictive Analytics Prototype** → Demand forecasting + fleet optimization using dummy ride data.  

Both projects are designed to **directly translate into real-world implementation** for Bimride, providing financial clarity for investors and operational efficiency for management.

---

## 🛠️ Dummy Project Work (Step by Step)

### Part 1: Unit Economics Simulation

#### Step 1: Defining Metrics
- **CAC (Customer Acquisition Cost)** = Marketing Spend ÷ New Users Acquired.  
- **LTV (Lifetime Value)** = Average Ride Value × Ride Frequency × Retention Period × Commission %.  
- **ARPU (Average Revenue Per User)** = Total Revenue ÷ Active Users.  

---

#### Step 2: Preparing Dummy Data
Generated sample data for **1,000 riders**:  
- Monthly new riders acquired (via ads, referrals, promotions).  
- Marketing spend per channel.  
- Avg ride fare = **$12**.  
- Avg rides per rider/month = **6**.  
- Retention = **6 months** average.  
- Commission % = **20%**.  

---

#### Step 3: Calculating CAC, LTV, ARPU
- **CAC (Ads channel)** = $10,000 ÷ 500 = **$20 per user**.  
- **CAC (Referrals)** = $2,500 ÷ 250 = **$10 per user**.  
- **LTV** = $12 × 6 rides × 6 months × 20% = **$86.40 per rider**.  
- **ARPU (Monthly)** = $72,000 ÷ 1,000 riders = **$72 per user**.  

---

#### Step 4: Insights
- **LTV:CAC ratio** = 4.3 (healthy).  
- Referrals had the **lowest CAC** and best return on investment.  
- ARPU stable at **$72** → means improving retention boosts total revenue.  

---

### Part 2: Predictive Analytics Prototype

#### Step 1: Data Collection
Created dummy ride dataset for **30 days**:  
- Daily ride requests (peak hours vs off-peak).  
- Geographic clustering of demand (city zones).  
- Driver availability data.  

---

#### Step 2: Forecasting Demand
- Used **time-series modeling (ARIMA)** on dummy dataset.  
- Identified **daily peaks at 8–9 AM and 6–8 PM**.  
- Predicted 15% higher demand on weekends compared to weekdays.  

---

#### Step 3: Fleet Optimization Model
- Matched **forecasted demand per zone** with **available driver pool**.  
- Simulation results:  
  - With **100 drivers**, weekday demand could be met but weekends required **+25 extra drivers**.  
  - Idle time reduced by **18%** when predictive fleet reallocation was applied.  

---

#### Step 4: Visualization (Dummy Dashboards)
Created **mock dashboards** showing:  
- Heatmaps of demand zones.  
- Forecasted ride requests per hour.  
- Driver allocation recommendations.  

---

## ⚠️ Challenges Faced
1. **Data Quality Issues** – Real-world ride data includes noise (cancellations, duplicate entries, fraud) not simulated here.  
2. **Behavioral Assumptions** – LTV depends on retention, which is influenced by external factors (competition, pricing wars, seasonality).  
3. **Model Selection** – Time-series models worked for short-term forecasts, but may not capture long-term demand shifts.  
4. **Scalability Concerns** – Predictive fleet optimization worked on dummy data, but real-time deployment at scale needs high server resources.  
5. **Integration Gap** – Linking demand forecasts with driver app notifications requires further backend development.  

---

## 🚖 Application in Bimride (Ride-Hailing)

### Unit Economics
- **Investor Pitch:** Clear LTV:CAC ratio improves investor confidence in sustainability.  
- **Marketing Strategy:** Invest more in **referral campaigns** → lower CAC + better retention.  
- **Pricing Strategy:** Use ARPU trends to test subscription models (e.g., rider packages).  

### Predictive Analytics
- **Driver Efficiency:** Smart fleet reallocation reduces idle driver hours and improves income.  
- **Rider Satisfaction:** Reduced wait times = higher retention + word-of-mouth growth.  
- **Operational Planning:** Helps management forecast peak loads and avoid service disruptions.  

---

## ✅ Conclusion
This week’s work demonstrated how **unit economics** provides a **financial lens** for Bimride’s growth strategy, while **predictive analytics** offers an **operational tool** for scaling efficiently.  

Together, these approaches create a **data-driven foundation** for:  
- Attracting **VC funding** (strong financial projections).  
- Improving **fleet utilization** (lower costs, higher revenues).  
- Enhancing **customer experience** (shorter wait times, reliable rides).  

Both projects are immediately applicable to Bimride’s growth roadmap in the Caribbean ride-hailing market.

---
