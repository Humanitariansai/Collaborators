# ⚡ Dynamic Pricing & Surge Calculation in Bimride

## 🎯 Objective
Design and implement a dynamic pricing engine for Bimride that adjusts fares in real time based on supply-demand imbalances, time of day, location, and historical ride data — similar to how Uber and Lyft apply surge multipliers.

---

## 🔍 Why This Matters
- **Maximizes driver earnings** during peak hours.
- **Encourages more drivers to get online** when demand spikes.
- **Balances demand** by incentivizing riders to shift rides to lower-priced times.
- **Increases Bimride's revenue** through demand-based fare multipliers.

---

## 🧠 Core Inputs for Pricing Algorithm

| Input Type        | Data Sources / Examples                                       |
|-------------------|---------------------------------------------------------------|
| Demand Signals    | Number of ride requests per zone in last X minutes            |
| Supply Signals    | Number of available drivers in zone                           |
| Time-based Factors| Rush hour, weekends, holidays, events                         |
| Geo Factors       | Specific high-demand areas (airport, stadium, business hub)   |
| Historical Trends | Historical surge patterns in the same area & time             |
| External Factors  | Weather conditions, public transport strikes, traffic events  |

---

## 🏗️ Architecture Overview

### 1. **Data Collection Layer**
- Streams real-time rider requests and driver availability via **Kafka** or **Redis Pub/Sub**.
- Ingests historical ride & pricing data from **PostgreSQL**.
- Optionally integrates with **weather APIs** and **event APIs**.

### 2. **Zone Partitioning**
- Divide the operational area into geo-hash grids (e.g., **GeoHash Level 6** for ~1 km²).
- Maintain supply-demand stats per zone.

### 3. **Pricing Engine**
- Runs every 1–2 minutes for each zone.
- Formula:
```
surge_multiplier = base_multiplier + demand_factor - supply_factor + special_event_bonus
```
- Clamps multiplier between configured min/max (e.g., 1.0x to 3.0x).

### 4. **API Layer**
- **GET /pricing** → Returns calculated fare & surge multiplier for a trip request.
- **POST /pricing/override** → Allows admin/event-based manual adjustments.

### 5. **Caching**
- Use **Redis** to store surge multipliers for quick retrieval (<50 ms).
- Expire surge cache after recalculation.

---

## 📊 Example Calculation

**Scenario:**  
- Zone: Bridgetown Airport (GeoHash: xyz123)  
- Supply: 8 active drivers  
- Demand: 24 active requests in last 5 mins  
- Base Fare: $10.00  
- Multiplier formula result: `1.8x`

**Calculated Fare:**  
```
final_fare = base_fare * surge_multiplier
final_fare = 10.00 * 1.8 = $18.00
```

---

## ⚡ Optimization Tactics

| Challenge                  | Strategy                                               |
|----------------------------|--------------------------------------------------------|
| Avoid price shocks         | Smooth multiplier changes over time (rolling averages) |
| Over-surging in low demand | Set a floor threshold for demand-supply ratio           |
| Latency in price updates   | Use in-memory caches with async database sync           |
| Fairness                   | Apply surge caps for rider trust                        |
| Driver exploitation risk   | Show transparent fare breakdowns in driver app          |

---

## 🔐 Security & Integrity
- All pricing calculations logged in **pricing_events** table for auditing.
- Only authorized admin users can override multipliers.
- All fare API calls signed with server-side authentication.
- Regular anomaly detection to prevent abuse.

---

## 🌍 Real-World Extensions
- **Heatmaps in Driver App** → Show drivers high-surge areas visually.
- **Predictive Surge Forecasting** → Use ML models to predict surges 15–30 mins in advance.
- **Special Event Mode** → Preload surge multipliers during concerts, sports events, or holidays.
- **Loyalty Discounts** → Offset surge for frequent riders.

---

## 🚗 Relevance to Bimride

| Feature / Benefit             | Impact on Bimride                                   |
|--------------------------------|----------------------------------------------------|
| Surge pricing                  | Boosts driver supply during high-demand periods    |
| Event-based adjustments        | Captures extra revenue during known peak events    |
| Historical data utilization    | Improves accuracy of surge predictions             |
| Transparency in fares          | Builds rider trust and reduces complaints          |

---

## 📌 Deliverables

- ✅ Defined surge calculation algorithm
- ✅ Zone-based supply-demand tracking
- ✅ API endpoints for surge retrieval and admin override
- ✅ Caching strategy for sub-50 ms response times
- ✅ Logging & auditing framework for fare changes