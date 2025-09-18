# Report: Customer Acquisition & Retention Dashboards + Workflow Automation for Scaling Operations  
**Date:** 6–12 September  
**Topics:**  
1. Tableau Dashboards on Customer Acquisition & Retention Strategies (B2C Growth Playbook)  
2. Scaling Operations with Workflow Automation (Case: Dispatch & Customer Support)  

---

## 📌 Overview
This week I worked on two interconnected dummy projects:  
1. Designing **Tableau dashboards** to track and improve **customer acquisition & retention**.  
2. Implementing a **workflow automation prototype** for **ride dispatch & customer support** operations.  

Both initiatives simulate how **Bimride** can scale strategically while keeping **customer satisfaction and operational efficiency** at the core.

---

## 🛠️ Dummy Project Work (Step by Step)

### Part 1: Tableau Dashboards – Customer Acquisition & Retention (B2C Growth Playbook)

#### Step 1: Data Preparation
- Collected **dummy datasets**:
  - Rider sign-ups per month.  
  - Active riders vs churned riders.  
  - Ride frequency per user.  
  - CAC (Customer Acquisition Cost) per marketing channel (ads, referrals, promotions).  
  - LTV (Lifetime Value) per rider cohort.  

- Cleaned data using Excel → imported into **Tableau**.  

---

#### Step 2: Building KPIs
Defined key KPIs to monitor:  
- **Customer Acquisition Cost (CAC)** = Total Marketing Spend ÷ New Riders.  
- **Lifetime Value (LTV)** = Avg Ride Value × Ride Frequency × Retention Months × Commission %.  
- **Retention Rate** = (Active Users at End of Period ÷ Active Users at Start) × 100.  
- **Churn Rate** = 100 – Retention Rate.  
- **Cohort Analysis** = Rider retention by signup month.  

---

#### Step 3: Creating Dashboards
Designed **3 dashboards in Tableau**:  

1. **Acquisition Dashboard**  
   - CAC by channel (ads, referral, partnerships).  
   - Conversion funnel (App downloads → Account creation → First ride).  

2. **Retention Dashboard**  
   - Rider cohort analysis (e.g., % of riders retained after 1, 3, 6 months).  
   - Average rides per rider over time.  

3. **Revenue Impact Dashboard**  
   - LTV vs CAC ratio.  
   - Break-even analysis by customer segment.  

---

#### Step 4: Insights (Dummy Example Results)
- Facebook Ads CAC = $12, Referral CAC = $5 → referrals most cost-efficient.  
- Cohort analysis showed **40% of riders stop after first month** → onboarding improvements needed.  
- LTV:CAC ratio = 4:1 (healthy, but can be improved with better retention).  

---

### Part 2: Workflow Automation – Dispatch & Customer Support

#### Step 1: Mapping Existing Workflow
Mapped out Bimride’s current operations:  
- Ride request → Driver match → Driver confirmation → Ride completion.  
- Support requests → Manual ticket handling → Resolution.  

---

#### Step 2: Identifying Pain Points
- Dispatch delays when multiple requests hit peak hours.  
- Drivers rejecting trips, causing delays.  
- Customer complaints not always resolved quickly (manual follow-ups).  

---

#### Step 3: Dummy Automation Prototype
Using **n8n (workflow automation tool)**, I simulated:  
- **Automated Dispatch Rules:**  
  - Assign ride request to nearest driver within 5 seconds.  
  - Auto-reassign if driver doesn’t respond in 15 seconds.  

- **Customer Support Automation:**  
  - New complaint → auto-log in CRM → auto-assign to available agent.  
  - FAQ-type complaints auto-responded via chatbot integration.  

---

#### Step 4: Test Scenarios
- Simulated **100 dummy ride requests** → automated dispatch reduced avg assignment time from **30s → 8s**.  
- Simulated **50 dummy customer complaints** → chatbot resolved 40% instantly.  

---

## ⚠️ Challenges Faced
1. **Tableau Data Limitations** – Dummy datasets lacked complexity (no real-world noise like failed payments, multi-device logins).  
2. **Customer Retention Complexity** – Hard to simulate behavioral triggers (seasonal effects, price sensitivity).  
3. **Automation Pitfalls** – Automated dispatch sometimes created **overlapping requests** (two drivers assigned to same rider).  
4. **Customer Support AI Limitations** – Chatbot couldn’t handle nuanced complaints (e.g., disputes about ride fare).  
5. **Scalability Concerns** – Simulated automations worked well on dummy data but may strain real systems under 10k+ concurrent users.  

---

## 🚖 Application in Bimride (Ride-Hailing)

### Tableau Dashboards
- **Investor Relations:** Dashboards provide **visual evidence** of customer growth & retention strategy.  
- **Management:** Helps monitor CAC & retention in real time.  
- **Strategy:** Insights allow targeted marketing (e.g., expand referral programs).  

### Workflow Automation
- **Faster Dispatch:** Improves rider satisfaction → higher retention.  
- **Efficient Support:** Reduced response time → stronger trust in Bimride brand.  
- **Cost Savings:** Less manual intervention in support & dispatch.  

---

## ✅ Conclusion
This week’s dummy projects provided a **dual perspective**:  
- **Strategic (Tableau Dashboards):** Show how Bimride can track and optimize **B2C growth metrics** (acquisition, retention, LTV).  
- **Operational (Workflow Automation):** Demonstrate how **scaling processes** like dispatch & support can be automated for efficiency.  

Together, these two initiatives directly support **Bimride’s long-term growth strategy** – both from an **investor storytelling perspective** and a **day-to-day operational execution perspective**.

---
