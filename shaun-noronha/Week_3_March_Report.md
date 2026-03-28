# Week 3 March Report (2026-03-21 → 2026-03-27)

---

## 🧾 Summary
Week 3 of March focused on **predictive public operations, emergency coordination, and disruption-aware mobility response** across Barbados.  
After Week 1 built stronger compliance infrastructure and Week 2 expanded interoperability with partner systems, this week shifted toward preparing Bimride to operate more effectively during public disruptions, weather-linked traffic instability, emergency routing needs, and city-scale service interruptions.

The team concentrated on:
- disruption prediction,
- emergency route prioritization,
- shelter and hospital corridor readiness,
- telecom-aware mobility risk signals,
- public alert synchronization,
- evacuation-support dispatch logic,
- and city-scale mobility response dashboards.

The objective was to ensure Bimride could support resilient, socially responsible transportation not only under normal commercial demand, but also during periods of public strain where reliability, prioritization, and coordination matter more than pure efficiency.

---

## ⚙️ Core Outcomes
- Built a **disruption prediction model** for traffic and mobility interruptions.
- Implemented an **emergency route prioritization engine** for critical corridors.
- Created a **medical and shelter corridor readiness workflow** for high-priority access zones.
- Added a **telecom-aware mobility degradation monitor** for communications-sensitive service planning.
- Integrated a **public alert synchronization feed** into mobility operations.
- Developed an **evacuation-support dispatch logic layer** for controlled routing priority under emergency conditions.
- Published a **city-scale response dashboard** for operations and leadership coordination.

---

## 🗓️ 2026-03-21 — Disruption Prediction Model
**Author:** Shaun Noronha  

### 🎯 Objective
Predict likely mobility disruptions before they fully materialize by combining traffic, weather, incident, and public-event signals.

### ⚙️ Architecture Overview
```
[Traffic Feed]
[Weather Feed]
[Incident Reports]
[Event Feed]
        ↓
[Feature Engineering Layer]
        ↓
[Disruption Prediction Model]
        ↓
[Zone Disruption Risk Scores]
        ↓
[Operations Dashboard + Alert Layer]
```

### 🧠 Algorithms Used
The disruption model used a **gradient-boosted tree classifier** to estimate the probability that a zone would experience service degradation within a future prediction window.

**Key features**
- congestion trend delta
- rainfall intensity
- road incident flags
- event density
- historical disruption rate
- time-of-day and day-of-week
- nearby zone spillover intensity

**Prediction logic**
```python
risk_prob = disruption_model.predict_proba(zone_features)[0][1]

if risk_prob > 0.70:
    flag_zone_for_preemptive_action(zone_id)
```

### 📋 Implementation Steps
1. Merged historical mobility degradation incidents with weather and congestion signals.
2. Built zone-level disruption labels for supervised learning.
3. Engineered rolling features for demand pressure, event influence, and route stress.
4. Trained and validated the classifier on prior disruption windows.
5. Published disruption risk scores by zone to operations systems.

### 🔍 Real-World Scenario
Unexpected rainfall and congestion buildup in **Bridgetown and surrounding approach corridors** often created cascading delays that were only recognized after service quality had already degraded.  
The model began surfacing high-risk windows earlier, giving operations more time to shift fleet posture.

### 🧰 Tools & Technologies
| Tool | Purpose |
|------|---------|
| XGBoost | disruption modeling |
| Pandas | feature engineering |
| PostgreSQL | zone event history |
| FastAPI | risk scoring API |
| Power BI | disruption dashboard |

### 📈 KPIs & Metrics
- Disruption lead-time improvement: **up 18%**
- Early-zone warning quality improved over threshold-only rules
- Alertable risk windows became operationally visible sooner
- Better preemptive fleet positioning in pilot zones

### ⚠️ Risks & Mitigations
| Risk | Mitigation |
|------|------------|
| False alerts in high-variance zones | risk smoothing across rolling intervals |
| Event-heavy areas over-trigger model | event normalization features |
| Weather data lag | fallback cached weather windows |
| Model drift during seasonal pattern shifts | periodic retraining |

### ✅ Conclusion
The disruption model gave Bimride earlier warning signals for mobility instability and improved its ability to act before service breakdown became visible to riders.

---

## 🗓️ 2026-03-22 — Emergency Route Prioritization Engine
**Author:** Shaun Noronha  

### 🎯 Objective
Rank critical road corridors during emergency or disruption scenarios so routing and dispatch decisions can protect access to essential destinations.

### ⚙️ Architecture Overview
```
[Road Network]
[Hospital / Shelter / Hub Locations]
[Traffic Conditions]
[Risk Signals]
        ↓
[Priority Corridor Scorer]
        ↓
[Critical Route Ranking]
        ↓
[Dispatch + Routing Overrides]
```

### 🧠 Algorithms Used
This engine used a weighted corridor prioritization model.

**Priority score**
```python
priority_score = (
    0.30 * essential_access_weight +
    0.25 * travel_viability +
    0.20 * congestion_resilience +
    0.15 * public_need_score +
    0.10 * fallback_route_depth
)
```

Corridors serving hospitals, shelters, and emergency hubs received higher essential-access weights than ordinary commercial routes.

### 📋 Implementation Steps
1. Defined essential destination classes such as hospitals, shelters, transport hubs, and public service nodes.
2. Mapped road network corridors to critical destinations.
3. Calculated route viability and resilience metrics under stress conditions.
4. Ranked corridors dynamically using disruption-aware inputs.
5. Exposed priority rankings to dispatch and ops interfaces.

### 🔍 Real-World Scenario
Under simulated mobility stress affecting **hospital access corridors out of Bridgetown**, the engine elevated routes that preserved continuity toward essential services even when commercially busier roads were under pressure.

### 🧰 Tools & Technologies
| Tool | Purpose |
|------|---------|
| PostGIS | corridor geometry and routing context |
| Python | prioritization scoring |
| FastAPI | route priority API |
| Power BI | corridor visibility dashboard |

### 📈 KPIs & Metrics
- Critical corridor visibility improved
- Faster prioritization of essential routes during simulated disruption
- Better separation of commercial vs essential route value
- Dispatch coordination improved for service continuity planning

### ⚠️ Risks & Mitigations
| Risk | Mitigation |
|------|------------|
| Priority score oversimplifies local road realities | route drilldowns and manual override |
| Essential route list incomplete | maintained destination registry |
| Over-prioritization harms general service balance | emergency-mode scope gating |
| Route viability changes too quickly | frequent refresh windows |

### ✅ Conclusion
The route prioritization engine gave Bimride a principled way to distinguish critical access corridors from ordinary network demand during emergencies.

---

## 🗓️ 2026-03-23 — Medical and Shelter Corridor Readiness Workflow
**Author:** Shaun Noronha  

### 🎯 Objective
Track whether mobility support around hospitals, clinics, shelters, and high-priority public locations is operationally ready before and during disruptions.

### ⚙️ Architecture Overview
```
[Facility Registry]
[Fleet Position]
[Route Priority Scores]
[Traffic Viability]
        ↓
[Readiness Assessment Engine]
        ↓
[Facility Corridor Readiness States]
        ↓
[Ops Dashboard]
```

### 🧠 Algorithms Used
A composite readiness score was used.

```python
readiness_score = (
    0.30 * fleet_coverage +
    0.25 * route_viability +
    0.20 * dispatch_responsiveness +
    0.15 * congestion_tolerance +
    0.10 * fallback_access
)
```

### 📋 Implementation Steps
1. Built a registry of critical facilities and associated access corridors.
2. Linked those facilities to nearby supply, route viability, and congestion indicators.
3. Calculated readiness score at regular intervals.
4. Flagged facilities with yellow or red readiness state.
5. Added readiness views for operations and leadership response.

### 🔍 Real-World Scenario
Access continuity to **medical corridors and shelter-relevant routes in Bridgetown and surrounding zones** was tracked more explicitly rather than assumed from general fleet activity.  
This prevented blind spots where citywide service looked stable but critical access readiness was weaker.

### 🧰 Tools & Technologies
| Tool | Purpose |
|------|---------|
| PostgreSQL | facility registry |
| Python | readiness scoring |
| FastAPI | readiness service |
| Power BI | facility readiness dashboard |

### 📈 KPIs & Metrics
- Better visibility into essential mobility readiness
- Faster identification of weak service coverage near critical facilities
- Improved planning alignment between fleet position and public-need zones
- Readiness state now measurable instead of assumed

### ⚠️ Risks & Mitigations
| Risk | Mitigation |
|------|------------|
| Registry misses one critical facility | maintained validation process |
| Fleet presence overstates true readiness | combine with route viability |
| Readiness score too coarse | sub-score drilldown panels |
| Facility needs change during incidents | manual override state support |

### ✅ Conclusion
This workflow made high-priority public access measurable and helped Bimride treat essential corridors as an operational category of their own.

---

## 🗓️ 2026-03-24 — Telecom-Aware Mobility Degradation Monitor
**Author:** Shaun Noronha  

### 🎯 Objective
Incorporate telecom degradation signals into mobility operations planning because app connectivity, driver communications, and dispatch updates can fail even when road conditions remain usable.

### ⚙️ Architecture Overview
```
[App Connectivity Metrics]
[Driver Sync Failure Rates]
[Message Delivery Health]
        ↓
[Telecom Degradation Monitor]
        ↓
[Communications Risk Score]
        ↓
[Ops Alerting + Routing Guidance Adjustments]
```

### 🧠 Algorithms Used
The monitor produced a communications-risk score.

```python
comms_risk = (
    0.40 * sync_failure_rate +
    0.30 * message_delivery_delay +
    0.20 * offline_session_ratio +
    0.10 * reconnect_time
)
```

### 📋 Implementation Steps
1. Aggregated app, driver, and sync-transport connectivity signals.
2. Built zone-level communications degradation indicators.
3. Scored telecom risk by area and time window.
4. Flagged zones where service quality might degrade despite usable roads.
5. Fed risk output into dispatch and operational awareness tools.

### 🔍 Real-World Scenario
In **East Coast and lower-signal corridors**, transport operations could become unreliable because of sync failure rather than direct road failure.  
The monitor surfaced these zones as communications-sensitive so planning could adapt earlier.

### 🧰 Tools & Technologies
| Tool | Purpose |
|------|---------|
| Python | telecom risk logic |
| PostgreSQL | sync and delivery history |
| Grafana | communications monitoring |
| FastAPI | risk scoring endpoint |

### 📈 KPIs & Metrics
- Communications-related service risk became visible
- Better separation between road disruption and connectivity disruption
- Earlier flagging of sync-fragile zones
- Improved degraded-mode planning for low-signal areas

### ⚠️ Risks & Mitigations
| Risk | Mitigation |
|------|------------|
| Connectivity data noisy | smoothing over rolling windows |
| Localized outages misread as systemic | zone-level scoring |
| Overreaction to small sync delays | alert thresholds with dampening |
| Telecom health not linked to mobility planning | integration with ops dashboards |

### ✅ Conclusion
The telecom-aware monitor broadened Bimride’s operational understanding by recognizing that communications fragility can be just as important as road fragility during disruptions.

---

## 🗓️ 2026-03-25 — Public Alert Synchronization Feed
**Author:** Shaun Noronha  

### 🎯 Objective
Synchronize mobility operations with public alerts and advisories so routing, pickup guidance, and dispatch logic can adapt to external warnings.

### ⚙️ Architecture Overview
```
[Public Alerts]
[Road Advisories]
[Weather Warnings]
[Venue Notices]
        ↓
[Alert Normalization Layer]
        ↓
[Mobility Impact Mapper]
        ↓
[Shared Alert Feed]
        ↓
[Ops and Routing Systems]
```

### 🧠 Algorithms Used
This was a normalization and impact-mapping pipeline.

**Impact mapping**
```python
if alert_type == "flood_risk":
    affected_mode = "routing_and_pickups"
elif alert_type == "crowd_restriction":
    affected_mode = "pickup_and_staging"
```

### 📋 Implementation Steps
1. Ingested public alerts from approved sources.
2. Standardized alert schema and severity bands.
3. Mapped alert types to transport system implications.
4. Tagged affected zones and time windows.
5. Published the synchronized alert feed internally.

### 🔍 Real-World Scenario
A public advisory impacting **South Coast event and transport corridors** was synchronized quickly into route and pickup operations instead of being noticed too late through manual monitoring alone.

### 🧰 Tools & Technologies
| Tool | Purpose |
|------|---------|
| Python | alert normalization |
| PostgreSQL | alert feed storage |
| FastAPI | alert delivery API |
| Power BI | public alert visibility |

### 📈 KPIs & Metrics
- Better alignment between public warnings and mobility response
- Reduced lag between public advisory release and ops visibility
- Alert applicability to transport workflows improved
- Fewer manual monitoring gaps

### ⚠️ Risks & Mitigations
| Risk | Mitigation |
|------|------------|
| Alert source inconsistency | source-priority rules |
| Advisory too broad for routing action | impact classification layer |
| Duplicate alerts clutter workflow | deduplication and merging |
| Expired alerts persist too long | strict TTL enforcement |

### ✅ Conclusion
The synchronized alert feed made Bimride more responsive to public conditions and reduced operational lag in interpreting external warnings.

---

## 🗓️ 2026-03-26 — Evacuation-Support Dispatch Logic Layer
**Author:** Shaun Noronha  

### 🎯 Objective
Create a dispatch mode that can prioritize protected movement, essential pickups, and controlled routing during emergency-support conditions.

### ⚙️ Architecture Overview
```
[Emergency Dispatch Requests]
[Priority Corridor Rankings]
[Facility Readiness States]
        ↓
[Emergency Dispatch Policy Layer]
        ↓
[Protected Dispatch Assignment]
        ↓
[Ops Control Surface]
```

### 🧠 Algorithms Used
This layer used a policy-constrained dispatch prioritization strategy.

```python
dispatch_priority = (
    0.35 * essential_request_weight +
    0.25 * corridor_priority +
    0.20 * vehicle_readiness +
    0.20 * response_time_score
)
```

### 📋 Implementation Steps
1. Defined dispatch classes for emergency-support contexts.
2. Linked dispatch weighting to corridor and facility readiness signals.
3. Added policy gates for controlled activation.
4. Built operator-visible emergency dispatch queues.
5. Logged all priority dispatch actions for later review.

### 🔍 Real-World Scenario
In a controlled emergency-support simulation affecting **shelter and medical access routes**, the dispatch logic elevated high-priority requests above ordinary commercial routing flows without disabling the rest of the system blindly.

### 🧰 Tools & Technologies
| Tool | Purpose |
|------|---------|
| Python | dispatch scoring logic |
| FastAPI | dispatch control layer |
| PostgreSQL | dispatch audit records |
| Power BI | emergency dispatch visibility |

### 📈 KPIs & Metrics
- Priority dispatch readiness improved
- Better separation between emergency and ordinary queue handling
- Dispatch reviewability preserved through audit logging
- Controlled activation logic reduced ambiguity in simulated response

### ⚠️ Risks & Mitigations
| Risk | Mitigation |
|------|------------|
| Emergency mode triggered too broadly | manual authorization gate |
| Priority scoring hides nuance | sub-score review |
| Commercial service starved unnecessarily | protected non-emergency minimum capacity |
| Staff confusion during mode shift | dashboard mode banner and workflow training |

### ✅ Conclusion
The evacuation-support dispatch layer gave Bimride a structured way to prioritize public-need mobility without abandoning accountability or control.

---

## 🗓️ 2026-03-27 — City-Scale Response Dashboard
**Author:** Shaun Noronha  

### 🎯 Objective
Create a unified dashboard for city-scale and island-scale mobility response during disruptions, public advisories, or emergency-support periods.

### ⚙️ Architecture Overview
```
[Disruption Risk Scores]
[Critical Corridor Priorities]
[Facility Readiness]
[Telecom Risk]
[Public Alerts]
[Emergency Dispatch Signals]
        ↓
[Response Intelligence Warehouse]
        ↓
[City-Scale Response Dashboard]
```

### 🧠 Algorithms Used
This was a synthesis layer that unified public-operations signals into a single operational control surface.

### 📋 Implementation Steps
1. Standardized response-oriented metrics across all sub-systems.
2. Created a shared warehouse for disruption and emergency-support views.
3. Built dashboard panels for operations, leadership, and response planning.
4. Added drilldowns by parish, corridor, and facility type.
5. Added freshness indicators and event timeline overlays.

### 🔍 Real-World Scenario
Leadership and operations teams tracking **Bridgetown, South Coast, airport-linked corridors, and essential access zones** could finally view public mobility readiness and disruption exposure in one place instead of across fragmented tools.

### 🧰 Tools & Technologies
| Tool | Purpose |
|------|---------|
| PostgreSQL | response warehouse |
| Python | metric synthesis |
| Power BI | dashboard presentation |
| FastAPI | reporting layer |

### 📈 KPIs & Metrics
- Better cross-team visibility during response planning
- Reduced delay in identifying multi-factor mobility risk
- More coordinated view of public access readiness
- Dashboard refresh SLA: **under 15 minutes**

### ⚠️ Risks & Mitigations
| Risk | Mitigation |
|------|------------|
| Too many signals overload ops teams | severity-based panel prioritization |
| Metrics interpreted differently by teams | shared definitions and labels |
| Stale dashboard creates false confidence | freshness status indicators |
| Public-operations mode confused with ordinary service mode | explicit dashboard state separation |

### ✅ Conclusion
The city-scale response dashboard unified disruption, readiness, communications, alerting, and dispatch signals into one operational view, making Bimride more capable as a public-responsibility mobility platform.

---

## 🚧 Challenges Faced
- Public disruption data varied in timeliness and quality.
- Essential-corridor logic required careful balancing against ordinary service needs.
- Telecom degradation introduced operational risk that did not always correlate with road conditions.
- Emergency-support dispatch policies needed strict governance to avoid overuse.
- Dashboard design had to present many signals without overwhelming operators.

---

## 🏁 Conclusion
Week 3 of March made Bimride significantly stronger in **public-operations readiness, disruption response, and emergency-support mobility planning**.  
By combining disruption prediction, critical corridor prioritization, facility readiness, telecom-aware risk signals, synchronized public alerts, emergency dispatch logic, and a city-scale response dashboard, the platform became more capable of serving Barbados not just as a transport service, but as a resilient public-mobility partner.
