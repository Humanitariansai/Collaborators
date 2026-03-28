# Week 4 February Report (2026-02-21 → 2026-02-27)

---

## 🧾 Summary
Week 4 focused on **fleet economics, utilization intelligence, driver earnings balance, and subsidy efficiency** across the Bimride network.  
After Week 3 addressed tourism and event mobility, this week shifted toward the economics of operating a nonprofit transport platform sustainably at scale.

The team worked on:
- measuring true vehicle utilization,
- modeling idle time and deadhead inefficiency,
- improving earnings balance between drivers,
- evaluating subsidy effectiveness in low-density zones,
- analyzing route profitability under nonprofit constraints,
- and building financial-operational scorecards for leadership.

The objective was to ensure Bimride could continue expanding mobility access across Barbados while maintaining transparency, fairness, and cost discipline.

---

## ⚙️ Core Outcomes
- Built a **fleet utilization intelligence model** combining active time, idle time, and deadhead distance.
- Created a **driver earnings balance framework** to identify unfair distribution patterns.
- Implemented a **subsidy efficiency model** for underserved and socially important corridors.
- Launched a **deadhead reduction analytics workflow** for empty repositioning segments.
- Built a **route economics scorecard** combining cost, demand, and access value.
- Added a **vehicle productivity ranking framework** by zone and time band.
- Published a **fleet economics dashboard** for internal decision support.

---

## 🗓️ 2026-02-21 — Fleet Utilization Intelligence Model
**Author:** Shaun Noronha  

### 🎯 Objective
Measure how effectively the fleet is being used by quantifying active ride time, idle availability, and repositioning inefficiency.

### ⚙️ Architecture Overview
```
[Trip Logs]
[Driver Availability States]
[GPS Movement Data]
        ↓
[Utilization Feature Builder]
        ↓
[Fleet Utilization Model]
        ↓
[Zone / Vehicle Utilization Dashboard]
```

### 🧠 Algorithms Used
This model computed a utilization score using:
- active trip minutes,
- idle waiting minutes,
- deadhead movement,
- and availability consistency.

```python
utilization_score = (
    0.45 * active_time_ratio +
    0.25 * idle_inverse +
    0.20 * deadhead_inverse +
    0.10 * shift_stability
)
```

### 📋 Implementation Steps
1. Reconstructed vehicle state timelines from trip and GPS data.
2. Classified each interval as active, idle, repositioning, or unavailable.
3. Aggregated vehicle utilization by zone and time band.
4. Computed normalized utilization scores.
5. Published utilization heatmaps to the operations and finance dashboards.

### 🔍 Real-World Scenario
Vehicles serving **Bridgetown business corridors** had high active minutes but also high idle troughs between predictable peaks, while some coastal tourism corridors showed lower active trip volume but stronger continuity.  
This revealed that high raw ride counts did not always equal efficient utilization.

### 🧰 Tools & Technologies
| Tool | Purpose |
|------|---------|
| Python | utilization computation |
| PostgreSQL | trip and state storage |
| Pandas | state aggregation |
| Power BI | utilization dashboard |

### 📈 KPIs & Metrics
- Fleet utilization visibility improved across all active zones
- Idle interval measurement consistency improved
- Deadhead-adjusted utilization proved more informative than raw trip count
- Zone-level utilization refreshed daily for ops review

### ⚠️ Risks & Mitigations
| Risk | Mitigation |
|------|------------|
| State classification gaps | fallback heuristics on missing telemetry |
| GPS drift affects deadhead estimates | smoothing and map matching |
| Short rides inflate utilization | deadhead-adjusted scoring |
| Cross-zone comparison unfair | zone normalization bands |

### ✅ Conclusion
The utilization model gave Bimride a more realistic view of fleet productivity and exposed inefficiencies hidden by ride-count-only analysis.

---

## 🗓️ 2026-02-22 — Driver Earnings Balance Framework
**Author:** Shaun Noronha  

### 🎯 Objective
Assess whether driver earnings are being distributed fairly across zones, times, and dispatch patterns.

### ⚙️ Architecture Overview
```
[Driver Earnings]
[Trip Volume]
[Zone Assignment]
[Dispatch History]
        ↓
[Earnings Equity Analyzer]
        ↓
[Balance Score + Distribution Dashboard]
```

### 🧠 Algorithms Used
This framework calculated:
- earnings dispersion,
- trip-value concentration,
- zone opportunity imbalance,
- and temporal fairness.

**Balance score**
```python
balance_score = 1 - normalized_variance(driver_earnings_group)
```

### 📋 Implementation Steps
1. Grouped earnings by driver, zone, and time band.
2. Measured dispersion and concentration of high-value trips.
3. Compared dispatch opportunity vs realized earnings.
4. Built fairness summaries for operations and policy review.
5. Flagged extreme imbalance segments for further analysis.

### 🔍 Real-World Scenario
Drivers operating in **Warrens and Bridgetown** received more consistent mid-value work, while some peripheral drivers only received fragmented low-value opportunities.  
This raised questions around zone opportunity balance and dispatch fairness.

### 🧰 Tools & Technologies
| Tool | Purpose |
|------|---------|
| Python | balance and inequality calculations |
| PostgreSQL | earnings and dispatch history |
| Power BI | earnings fairness dashboard |
| Pandas | variance and concentration analysis |

### 📈 KPIs & Metrics
- Earnings distribution visibility improved substantially
- High-value trip concentration became measurable by zone
- Dispatch fairness review cycle shortened
- Extreme imbalance cases surfaced for manual review

### ⚠️ Risks & Mitigations
| Risk | Mitigation |
|------|------------|
| Earnings fairness confused with productivity differences | compare against opportunity metrics |
| Outliers distort balance score | robust dispersion statistics |
| Drivers compare raw totals without context | fairness score explanations |
| Small sample drivers skew results | minimum trip thresholds |

### ✅ Conclusion
The earnings balance framework helped Bimride evaluate equity in driver opportunity without ignoring legitimate performance differences.

---

## 🗓️ 2026-02-23 — Subsidy Efficiency Model
**Author:** Shaun Noronha  

### 🎯 Objective
Measure whether subsidies used to support low-density or socially important corridors are delivering meaningful mobility access efficiently.

### ⚙️ Architecture Overview
```
[Subsidized Routes]
[Ride Volume]
[Cost Records]
[Access Priority Metadata]
        ↓
[Subsidy Efficiency Model]
        ↓
[Corridor Efficiency Scores]
        ↓
[Policy Dashboard]
```

### 🧠 Algorithms Used
The model balanced:
- mobility access gained,
- rider coverage,
- route cost,
- and social priority weighting.

```python
subsidy_efficiency = (
    0.35 * access_gain +
    0.25 * rider_coverage +
    0.20 * social_priority +
    0.20 * cost_inverse
)
```

### 📋 Implementation Steps
1. Identified subsidized and partially subsidized routes.
2. Calculated subsidy spend per corridor.
3. Measured rider access gained and coverage stability.
4. Weighted corridors by social access priority.
5. Published corridor-level subsidy efficiency rankings.

### 🔍 Real-World Scenario
Some lower-density routes in **East Coast and interior zones** showed weaker cost efficiency but higher social value due to low transport alternatives.  
The model helped Bimride compare efficiency without erasing equity goals.

### 🧰 Tools & Technologies
| Tool | Purpose |
|------|---------|
| Python | efficiency scoring |
| PostgreSQL | cost and route records |
| Pandas | corridor analysis |
| Power BI | policy reporting |

### 📈 KPIs & Metrics
- Subsidy efficiency now measurable by corridor
- Tradeoff visibility between access and cost improved
- Better distinction between strategic and low-impact subsidy spend
- Policy review support improved for leadership

### ⚠️ Risks & Mitigations
| Risk | Mitigation |
|------|------------|
| Pure cost focus undervalues equity routes | social-priority weighting |
| Access gain hard to quantify | route coverage and usage proxies |
| Seasonal demand distorts route performance | rolling averages |
| Leadership misreads score as purely financial | annotate social access context |

### ✅ Conclusion
The subsidy model gave Bimride a more nuanced way to evaluate support spending while preserving its nonprofit access mission.

---

## 🗓️ 2026-02-24 — Deadhead Reduction Analytics
**Author:** Shaun Noronha  

### 🎯 Objective
Reduce empty repositioning distance and time between trips without hurting rider wait times.

### ⚙️ Architecture Overview
```
[Vehicle GPS History]
[Trip Endpoints]
[Zone Demand Forecast]
        ↓
[Deadhead Analyzer]
        ↓
[Repositioning Opportunity Engine]
        ↓
[Ops Recommendations]
```

### 🧠 Algorithms Used
The analytics workflow measured:
- deadhead distance,
- deadhead time,
- expected repositioning benefit,
- and zone demand probability.

**Opportunity score**
```python
opportunity_score = (
    0.40 * deadhead_reduction_potential +
    0.30 * demand_alignment +
    0.20 * idle_reduction +
    0.10 * route_stability
)
```

### 📋 Implementation Steps
1. Classified all non-passenger vehicle movement as deadhead or necessary transition.
2. Calculated deadhead rates by zone and time.
3. Compared repositioning outcomes against subsequent ride probability.
4. Ranked improvement opportunities by expected savings.
5. Delivered recommendations to operations review.

### 🔍 Real-World Scenario
Vehicles repositioning between **Holetown resort areas and surrounding coastal corridors** often drove farther empty than necessary because repositioning was based on intuition rather than demand-aligned guidance.  
The deadhead model surfaced these opportunities clearly.

### 🧰 Tools & Technologies
| Tool | Purpose |
|------|---------|
| Python | deadhead scoring |
| PostGIS | route movement analysis |
| PostgreSQL | vehicle state history |
| Power BI | deadhead dashboard |

### 📈 KPIs & Metrics
- Deadhead visibility improved materially
- Idle-empty transition mapping became standardized
- High-opportunity waste zones identified
- Savings potential quantified by corridor

### ⚠️ Risks & Mitigations
| Risk | Mitigation |
|------|------------|
| GPS classification errors | map matching and smoothing |
| Repositioning too aggressively hurts readiness | demand threshold gating |
| Deadhead necessary in low-density zones | context-aware adjustment |
| Teams over-prioritize savings over service | service quality guardrails |

### ✅ Conclusion
Deadhead analytics helped Bimride expose hidden inefficiency in empty vehicle movement and build a clearer path toward cost-aware repositioning.

---

## 🗓️ 2026-02-25 — Route Economics Scorecard
**Author:** Shaun Noronha  

### 🎯 Objective
Create a route-level scorecard that compares not only demand and cost, but also strategic access value and reliability.

### ⚙️ Architecture Overview
```
[Route Demand]
[Route Cost]
[Utilization Data]
[Access Value Metadata]
        ↓
[Route Economics Scoring Layer]
        ↓
[Economics Scorecard Dashboard]
```

### 🧠 Algorithms Used
The scorecard blended:
- demand strength,
- cost efficiency,
- utilization,
- reliability,
- and access importance.

```python
route_score = (
    0.25 * demand_strength +
    0.20 * cost_inverse +
    0.20 * utilization +
    0.15 * reliability +
    0.20 * access_priority
)
```

### 📋 Implementation Steps
1. Built route-level summaries from trip, cost, and reliability records.
2. Standardized route economics features.
3. Calculated composite scores and ranked route bands.
4. Added drilldowns by parish and time band.
5. Published scorecards for strategic review.

### 🔍 Real-World Scenario
A route may have appeared weak on revenue in **North Coast or East Coast service areas**, but when access priority and reliability were included, it was recognized as strategically important rather than purely low-value.

### 🧰 Tools & Technologies
| Tool | Purpose |
|------|---------|
| Python | score computation |
| PostgreSQL | route metrics |
| Power BI | route scorecard |
| Pandas | standardization |

### 📈 KPIs & Metrics
- Route comparison became more balanced and transparent
- Scorecards reduced oversimplified route profitability debates
- Better decision support for route redesign conversations
- Leadership review cycle improved with shared route metrics

### ⚠️ Risks & Mitigations
| Risk | Mitigation |
|------|------------|
| Composite score hides route detail | sub-score breakdowns |
| Revenue-heavy interpretation dominates | access-priority included explicitly |
| Score drift over seasons | monthly recalculation |
| Route identity shifts over time | route-family grouping logic |

### ✅ Conclusion
The route economics scorecard created a more complete way to evaluate network performance in a nonprofit mobility setting.

---

## 🗓️ 2026-02-26 — Vehicle Productivity Ranking Framework
**Author:** Shaun Noronha  

### 🎯 Objective
Rank vehicles and vehicle-shift combinations by productivity while controlling for route context and demand conditions.

### ⚙️ Architecture Overview
```
[Vehicle Trip Records]
[Availability States]
[Deadhead Data]
[Demand Context]
        ↓
[Productivity Ranker]
        ↓
[Vehicle Productivity Dashboard]
```

### 🧠 Algorithms Used
Vehicle productivity ranking considered:
- completed rides,
- active time,
- deadhead burden,
- revenue contribution,
- and demand context.

```python
productivity_score = (
    0.30 * rides_completed +
    0.25 * active_time_ratio +
    0.20 * revenue_efficiency +
    0.15 * deadhead_inverse +
    0.10 * demand_context_score
)
```

### 📋 Implementation Steps
1. Aggregated vehicle productivity metrics by shift.
2. Normalized scores by zone demand conditions.
3. Ranked vehicles and shift combinations.
4. Flagged low-productivity patterns requiring investigation.
5. Shared output with fleet and operations teams.

### 🔍 Real-World Scenario
Vehicles assigned to similar demand windows in **Bridgetown and surrounding commuter corridors** showed materially different productivity profiles once deadhead and availability consistency were included, revealing operational inefficiencies beyond raw trip count.

### 🧰 Tools & Technologies
| Tool | Purpose |
|------|---------|
| Python | ranking engine |
| PostgreSQL | trip and shift storage |
| Pandas | productivity aggregation |
| Power BI | productivity dashboard |

### 📈 KPIs & Metrics
- Productivity visibility improved at vehicle and shift level
- Low-performance shift patterns surfaced sooner
- Better separation between demand-poor shifts and execution-poor shifts
- Fleet manager review efficiency improved

### ⚠️ Risks & Mitigations
| Risk | Mitigation |
|------|------------|
| Ranking penalizes vehicles in weak demand zones | demand-context normalization |
| Revenue dominates score unfairly | weighted productivity mix |
| One unusual shift skews rank | rolling period averages |
| Misuse for punitive decisions | advisory-only governance policy |

### ✅ Conclusion
The productivity framework gave Bimride a more disciplined way to understand fleet performance without collapsing all evaluation into simple ride count or revenue totals.

---

## 🗓️ 2026-02-27 — Fleet Economics Dashboard
**Author:** Shaun Noronha  

### 🎯 Objective
Unify utilization, earnings balance, subsidy efficiency, deadhead analysis, route economics, and productivity into one decision-support dashboard.

### ⚙️ Architecture Overview
```
[Utilization Metrics]
[Earnings Equity Scores]
[Subsidy Efficiency Scores]
[Deadhead Analytics]
[Route Economics]
[Vehicle Productivity]
        ↓
[Fleet Economics Warehouse]
        ↓
[Leadership + Ops Dashboard]
```

### 🧠 Algorithms Used
This was a synthesis layer rather than a standalone predictive model.  
Its key function was to standardize, combine, and present operational-financial metrics in a single coherent framework.

### 📋 Implementation Steps
1. Standardized definitions for fleet economic metrics.
2. Created a shared warehouse table for route, vehicle, and corridor economics.
3. Joined score outputs from earlier analyses into one reporting layer.
4. Built operations and leadership dashboard variants.
5. Added trend views for weekly and monthly economics monitoring.

### 🔍 Real-World Scenario
Teams evaluating service strategy across **Bridgetown commuter corridors, tourism-heavy coasts, and lower-density rural access routes** could now compare cost, access value, and productivity in a single place rather than across multiple disconnected reports.

### 🧰 Tools & Technologies
| Tool | Purpose |
|------|---------|
| PostgreSQL | fleet economics warehouse |
| Python | metric synthesis |
| Power BI | dashboard presentation |
| FastAPI | analytics service layer |

### 📈 KPIs & Metrics
- Cross-team alignment on route and fleet economics improved
- Decision prep time for economics reviews reduced
- Visibility into tradeoffs between cost and access increased
- Dashboard refresh SLA: **under 20 minutes**

### ⚠️ Risks & Mitigations
| Risk | Mitigation |
|------|------------|
| Dashboard overload for leadership users | curated executive view |
| Metric inconsistency between teams | shared metric dictionary |
| Cost-centric interpretation overwhelms mission metrics | explicit access and equity views |
| Stale economics data | scheduled refresh and alerts |

### ✅ Conclusion
The fleet economics dashboard gave Bimride a unified operational-financial view, helping leadership and operations teams make more balanced decisions about scale, fairness, and sustainability.

---

## 🚧 Challenges Faced
- Economics metrics required careful balancing between financial efficiency and nonprofit access goals.
- Vehicle productivity analysis needed demand-aware normalization to avoid unfair comparisons.
- Subsidy discussions were sensitive because some low-efficiency routes had high social value.
- Deadhead analytics depended heavily on high-quality GPS and route-state classification.
- Dashboard design had to serve both operational analysts and leadership without oversimplifying tradeoffs.

---

## 🏁 Conclusion
Week 4 of February made Bimride substantially stronger in **fleet economics, efficiency analysis, and financially grounded operational planning**.  
By combining utilization intelligence, earnings balance, subsidy efficiency, deadhead reduction, route economics, vehicle productivity, and unified reporting, the platform gained a more disciplined view of how to scale mobility access across Barbados without losing fairness or mission alignment.
