# Weekly Work Report: Customer Scamming – Ride Completion but Credit Card Disputes (Chargeback Fraud)**  
### **Period: 20–27 September**  

# 📌 1. Overview  
This week was focused entirely on **research, analysis, and brainstorming** around a significant issue Bimride is experiencing:  
**Customers completing rides but later disputing payments with credit card companies, causing chargeback losses.**

All work conducted was **exploratory and strategic** — no feature development or implementation occurred.  
The objective was to understand the problem deeply and outline *possible* technical, operational, and financial solutions for future decisions.

---

# 🛠️ 2. Step-by-Step Work (Exploration & Discussions Only)

---

# **20 September – Understanding the Scope of the Problem**  
### ✔️ Activities
- Reviewed recent chargeback cases to understand patterns and triggers.  
- Studied the ride-hailing payment flow to see where fraudulent disputes typically occur.  
- Identified pain points, including:
  - Weak evidence trail  
  - No formal trip completion verification  
  - Easy for customers to claim they didn't take the ride  

### ✔️ Output
- Documented key vulnerabilities in current billing + trip-completion processes.  
- Prepared a summary of recurring dispute reasons (friendly fraud, intentional fraud, unauthorized card use).

---

# **21 September – Fraud Patterns Research (Dummy Dataset)**  
### ✔️ Activities  
- Created a dummy dataset to simulate fraud patterns (for learning + analysis only).  
- Explored typical fraud behaviors:
  - Users repeatedly disputing small fares  
  - New accounts with risky patterns  
  - Device mismatch between booking and ride location  
- Studied how credit card companies evaluate chargeback disputes.  

### ✔️ Output  
- High-level notes on what evidence strengthens Bimride’s position during disputes.  
- No actual system or scoring model implemented — only designed the concept.

---

# **22 September – Cross-Team Discussions (Conceptual Only)**  
### ✔️ Teams Involved  
- Finance  
- Customer Support  
- Product/Tech  
- Operations  

### ✔️ Topics Discussed  
- How disputes impact business (losses, driver dissatisfaction).  
- What kind of verification data we currently have vs. what is needed.  
- Which potential solutions are feasible and which need deeper investigation.

### ✔️ Nature of Work  
All discussions were **conceptual**, focused on evaluating options — not making decisions or starting implementation.

---

# **23 September – Drafting Potential Approaches (Exploration Stage)**  
Three high-level solution paths were explored:

---

## **Solution A: Strong Trip Verification (Concept Only)**  
- OTP confirmation at drop-off  
- Map snapshots  
- Improved ride receipts  

No system built — only discussed the idea.

---

## **Solution B: Fraud Scoring System (Initial Concept)**  
- Score users based on behavior (disputes, device mismatch, etc.)  
- Possibly require extra verification for high-risk users  

Again, only conceptual design — no development or testing.

---

## **Solution C: Enhanced Payment Security (Discovery Only)**  
- Pre-authorization holds  
- 3D Secure payments  
- Chargeback insurance  

No integration decisions or prioritization yet — we only mapped possibilities.

---

# **24 September – Evaluating Pros & Cons (Strategic Discussion)**  
### ✔️ Activities  
- Compared solutions based on cost, friction, risk, and feasibility.  
- Shared early-stage analysis with internal team for feedback.  

### ✔️ Output  
- A combined approach (A + B) looks promising in theory — but **not finalized**.  
- No timeline defined; implementation requires future approval.

---

# **25 September – Designing Conceptual Workflows (No Execution)**  
### ✔️ Activities  
- Created draft workflows for how verification *could* work.  
- Outlined how evidence packets might be assembled for banks.  
- Discussed what data Ops & Support would need access to.  

### ✔️ Important Note  
These workflows are **purely illustrative** and not connected to any actual system.

---

# **26 September – Pilot Planning (Hypothetical Only)**  
### ✔️ Activities  
- Discussed what a pilot test *could* look like if approved.  
- Identified KPIs and potential metrics to track.  
- Considered risks and user-experience impacts.  

### ✔️ Output  
- A draft pilot plan document — **no pilot started**.  
- Requires leadership approval before moving forward.

---

# **27 September – Final Documentation (Exploratory Week Summary)**  
### ✔️ Activities  
- Compiled all research notes and solution comparisons.  
- Finalized the weekly article draft.  
- Outlined next steps required *before* implementation can begin:
  - Prioritization meetings  
  - Feasibility analysis  
  - Budget & timeline estimation  

---

# 📉 3. Challenges Faced  
### **1. Limited Historical Fraud Data**  
Difficult to analyze patterns without structured data.

### **2. Stakeholder Alignment Issues**  
Opinions varied on how much friction can be added to the customer journey.

### **3. Not Enough Technical Information Yet**  
Technical team needs deeper discovery before confirming feasibility.

### **4. Unclear Bank Requirements**  
Different banks require different forms of proof.

### **5. High Risk of Customer Friction**  
Any verification must be balanced with ease-of-use.

---

# 🚖 4. How This Work Applies to Bimride (Conceptual Level Only)

Even though implementation has not yet started, this week’s analysis provides:

### ✔️ Clear understanding of the chargeback risk  
This helps leadership plan resource allocation.

### ✔️ Early-stage solution map  
Bimride now has a clearer idea of:
- Operational steps  
- Technical considerations  
- Financial implications  

### ✔️ Strategic insights for future development  
The system can evolve into:
- Automated fraud scoring  
- Stronger dispute evidence  
- Verified trip completion  
- Smarter payment authentication

All of this is still **theoretical** — real implementation will depend on:
- Engineering bandwidth  
- Legal review  
- Budget  
- User experience design  

---

# ✍️ 5. Article Summary  
**Topic:** Customer Scamming by Taking Rides and Disputing Transactions  
This week’s article is centered around:
- Why fraud happens  
- How chargebacks harm ride-hailing businesses  
- What solutions exist in the industry  
- What Bimride *could* adopt in the future  
- Strategic thinking behind fraud prevention  

---

# ✅ Conclusion  
This week was dedicated to **exploration, conceptual planning, and stakeholder discussions**.  
No implementation or engineering work occurred.  
The outcome is a deeply researched foundation that will help guide Bimride toward choosing the right fraud-prevention strategy in upcoming phases.