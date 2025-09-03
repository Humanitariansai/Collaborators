# Daily Report – 8 August 2025  
**Topic:** Fraud Detection in Ride-Hailing Using BI Standards  
**Dummy Project:** Simulating fraudulent ride patterns and anomaly detection  
**Focus:** Leveraging BI and PM frameworks to build anti-fraud features  

---

## 1. Summary of Today’s Work  
Today, I explored how **fraud detection mechanisms** can be built for a ride-hailing platform like **Bimride** by simulating fraudulent ride patterns and detecting anomalies using **BI standards** and **Project Management (PM) frameworks**.  

The goal was to:  
- Create **synthetic ride data** with both normal and fraudulent patterns.  
- Apply **basic anomaly detection logic** (dummy rules + BI insights).  
- Document how this can evolve into a **full-scale fraud monitoring system**.  

---

## 2. Step-by-Step Dummy Project Implementation  

### **Step 1: Preparing Synthetic Ride Data**
- Created a dataset of 1,000 rides with attributes:  
  - `Ride ID`  
  - `Driver ID`  
  - `Passenger ID`  
  - `Pickup Location`  
  - `Dropoff Location`  
  - `Fare Amount`  
  - `Distance (km)`  
  - `Ride Time (minutes)`  
  - `Timestamp`  
- Injected **fraudulent scenarios**, such as:  
  - **Short rides with unusually high fares.**  
  - **Multiple rides by the same driver in impossible time frames.**  
  - **Same passenger ID used across multiple cities at the same time.**  

---

### **Step 2: Defining Fraud Indicators**
- Marked potential **fraud triggers**:  
  - High Fare-to-Distance ratio.  
  - Unusual Ride Frequency (e.g., >10 rides in 30 minutes).  
  - Geographic anomalies (pickup/drop-off >100 km apart in <10 minutes).  
  - Same credit card/passenger linked to multiple accounts.  

---

### **Step 3: Applying Rule-Based Detection**
- Built **dummy BI logic**:  
  - Flag rides where `fare/km > 5`.  
  - Flag drivers completing `>20 rides per day`.  
  - Flag rides with `distance < 1 km` but `fare > $50`.  
- Counted flagged anomalies → roughly **6% of rides** were marked as suspicious.  

---

### **Step 4: Simulating BI Dashboard (Mock-up)**
- Designed a **mock dashboard view (since actual prices are now allowed to disclose publicly)**:  

| Metric                          | Normal Range | Anomaly Detected |
|---------------------------------|--------------|------------------|
| Avg. Fare per km                | $2.5 – $3.2  | **$7.8 (alert)** |
| Avg. Rides per Driver (per day) | 10 – 15      | **35 (alert)**   |
| Duplicate Passenger Accounts    | <2           | **12 (alert)**   |
| % Suspicious Rides              | <2%          | **6% (alert)**   |

---

### **Step 5: Embedding into PM Framework**
- Applied **Agile + BI reporting standards**:  
  - **Epic:** Fraud Detection System.  
  - **User Story:** As a fraud analyst, I want to view anomaly reports so I can take quick action.  
  - **Sprint Goal:** Implement rules for fare anomalies and frequency anomalies.  
  - **BI Deliverable:** Dashboard with fraud KPIs.  

---

## 3. Challenges Faced  
1. **Synthetic Data Realism** – Ensuring dummy fraud patterns resembled real-world ride-hailing abuse.  
2. **False Positives** – Some flagged rides were legitimate (e.g., surge pricing made fares high).  
3. **Scalability Concern** – Simple rules work for small data but fail at scale → would need ML models.  
4. **Balancing Fraud Detection with User Experience** – Too many false alerts could unfairly block drivers or passengers.  

---

## 4. Application to Bimride  

If implemented in Bimride, this system could:  
1. **Prevent Revenue Loss** – Catch fraudulent rides before payouts to drivers.  
2. **Enhance Trust** – Passengers trust Bimride when fake rides/scams are minimized.  
3. **Operational Efficiency** – Fraud analysts focus only on **flagged cases**, not every ride.  
4. **Data-Driven Scaling** – Use anomaly dashboards as part of **BI strategy** to continuously refine fraud detection.  

**Future Expansion:**  
- Integrate **ML anomaly detection models** (e.g., Isolation Forests, Autoencoders).  
- Connect fraud alerts directly to **customer support workflows**.  
- Use **blockchain-based identity verification** to reduce fake accounts.  

---

## 5. Conclusion  
Today’s dummy project showed how **BI-driven fraud detection** can be prototyped using simple rule-based logic and expanded into **enterprise-level anomaly detection**.  

By linking BI dashboards with PM workflows, Bimride can ensure:  
- **Continuous monitoring** of fraudulent ride activity.  
- **Clear KPIs** for fraud analysts.  
- A framework that balances **security with user experience**.  

**Key Lesson:** Fraud detection is not just a technical problem—it requires **BI standards, project management alignment, and continuous refinement**.  

---
