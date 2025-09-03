# Daily Report – 9 August 2025  
**Topic:** Using Geospatial Analytics for Route Optimization  
**Dummy Project:** Analyzing synthetic GPS data for shortest routes  
**Focus:** BI dashboards for operational efficiency  

---

## 1. Summary of Today’s Work  
Today’s research and hands-on activity focused on **geospatial analytics** and its application in **route optimization** for ride-hailing platforms like **Bimride**.  

The dummy project involved creating **synthetic GPS data** for trips, applying **basic route analysis**, and designing how **BI dashboards** could visualize route efficiency for operations teams.  

---

## 2. Step-by-Step Dummy Project Implementation  

### **Step 1: Generating Synthetic GPS Data**  
- Created a dataset of 200 trips in Barbados with fields:  
  - `Trip ID`  
  - `Driver ID`  
  - `Passenger ID`  
  - `Start Location (lat/long)`  
  - `End Location (lat/long)`  
  - `Actual Distance (km)`  
  - `Time Taken (minutes)`  
- Added **GPS trace points** (lat/long every ~500m) to simulate route progression.  
- Example trip:  
  - Start: Bridgetown (13.0975, -59.6167)  
  - End: Oistins (13.0650, -59.5432)  
  - Actual Path: 12 km (with detours).  

---

### **Step 2: Calculating Shortest Routes**  
- Used **Haversine formula** to calculate direct distances between start and end points.  
- Defined "shortest route" as **90% of Haversine distance** (approximation).  
- Compared:  
  - **Actual route distance vs shortest route estimate.**  
  - Trips with **>20% deviation** flagged as inefficient.  

---

### **Step 3: Identifying Inefficient Trips**  
- Out of 200 trips:  
  - 150 trips followed efficient routes.  
  - 50 trips had detours adding **15–40% extra distance**.  
- Dummy findings:  
  - Avg. detour: **3.2 km extra per inefficient trip**.  
  - Potential operational loss (fuel + time): **~$1.20 per trip**.  

---

### **Step 4: Designing BI Dashboard (Mock-up)**  
(Since dashboards are treated as company proprietary product, mock dashboards with mock data are not allowed to disclose publicly to avoid disclosing metrics and corresponding color schemes)
Key dashboard metrics:  

| Metric                                | Value (Dummy) |
|---------------------------------------|---------------|
| Total Trips Analyzed                  | 200           |
| Avg. Distance Efficiency              | 87%           |
| % Trips with >20% Deviation           | 25%           |
| Avg. Detour Distance                  | 3.2 km        |
| Potential Cost Loss per 1,000 Trips   | $1,200        |

Visualization mock-ups (planned for BI):  
- **Heatmap:** Highlight routes with frequent inefficiencies.  
- **Bar chart:** Compare drivers by route efficiency.  
- **Trend line:** Efficiency improvements after interventions (training, rerouting algorithms).  

---

### **Step 5: Embedding into PM Framework**  
- **Epic:** Route Optimization with Geospatial Analytics.  
- **User Story:** As an operations manager, I want to identify inefficient routes so that I can reduce costs and improve customer satisfaction.  
- **Sprint Deliverable:** BI dashboard with route efficiency KPIs.  
- **Future Task:** Integrate real GPS logs from Bimride fleet into analytics pipeline.  

---

## 3. Challenges Faced  
1. **Synthetic GPS Data Realism** – Creating believable route deviations required adding “random detours,” but balancing realism with simplicity was tricky.  
2. **Shortest Route Calculation** – Real roads are not straight lines; Haversine distance was too simplistic. A road network graph (like OpenStreetMap) would be better.  
3. **False Inefficiency Signals** – Some detours may be legitimate (road closures, traffic congestion, passenger pickup preferences).  
4. **Scalability** – Analyzing thousands of trips requires efficient geospatial libraries (GeoPandas, PostGIS) which were not simulated today.  

---

## 4. Application to Bimride  

If applied to **Bimride**, this system can:  
1. **Optimize Driver Routes** – Provide drivers with near-optimal routes based on real-time traffic + historical data.  
2. **Reduce Costs** – Lower fuel consumption and improve driver utilization.  
3. **Improve Customer Satisfaction** – Shorter, predictable trips increase trust in the platform.  
4. **Operational Insights** – Managers can see which drivers/areas frequently have inefficiencies.  

**Future Expansion:**  
- Integrate with **real-time traffic APIs** for dynamic rerouting.  
- Build **driver efficiency scoring system** to link route efficiency with incentive programs.  
- Use **machine learning models** to predict optimal routes during peak vs non-peak hours.  

---

## 5. Conclusion  
The dummy project demonstrated how **geospatial analytics** can be used to detect and visualize route inefficiencies. While today’s exercise was simplified, it shows a clear path to scaling this into a **BI-powered optimization engine** for **Bimride** .  

**Key Lesson:** By combining **geospatial data, BI dashboards, and PM frameworks**, Bimride can cut costs, improve efficiency, and deliver a better rider experience.  
