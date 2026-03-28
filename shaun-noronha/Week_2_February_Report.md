# Week 2 February Report (2026-02-07 → 2026-02-13)

---

## 🧾 Summary
Week 2 focused on **growth intelligence, retention optimization, and rider lifecycle analytics** across Bimride Barbados.  
After Week 1 strengthened the platform’s resilience and failure recovery, this week shifted toward making the user base more stable, engaged, and better understood.

The team concentrated on:
- identifying early signs of rider churn,
- optimizing referral and onboarding flows,
- improving rider activation after first trip,
- ranking re-engagement opportunities,
- modeling loyalty behavior by parish,
- and building lifecycle visibility across the full rider funnel.

The objective was to help Bimride grow in a way that was **data-driven, sustainable, and community-aware**, especially as the platform expanded across mixed commuter, tourism, and low-frequency rider segments in Barbados.

---

## ⚙️ Core Outcomes
- Built a **rider churn prediction model** using behavioral and inactivity signals.
- Implemented an **onboarding intelligence pipeline** to identify friction during the first-trip journey.
- Designed a **referral analytics engine** to measure invite effectiveness and conversion quality.
- Created a **rider activation scoring model** to predict which new users were likely to complete a second and third trip.
- Launched a **re-engagement prioritization service** for inactive but recoverable riders.
- Built a **loyalty segmentation framework** to distinguish commuters, occasional users, tourists, and event-driven riders.
- Deployed a **full rider funnel dashboard** connecting acquisition, activation, retention, and reactivation metrics.

---

## 🗓️ 2026-02-07 — Rider Churn Prediction Model
**Author:** Shaun Noronha  

### 🎯 Objective
Predict which riders are at high risk of churning so Bimride can intervene before the user becomes inactive long-term.

### ⚙️ Architecture Overview
```
[Ride History]
[App Session Logs]
[Payment Success Data]
[Support Interaction Data]
        ↓
[Feature Engineering Layer]
        ↓
[XGBoost Churn Model]
        ↓
[Churn Probability API]
        ↓
[Retention Dashboard + CRM Export]
```

### 🧠 Algorithms Used
A **gradient-boosted decision tree model** was used because it handled mixed numeric and categorical rider behavior features well and was effective on non-linear retention patterns.

**Feature groups**
- days since last trip
- total trips in last 30 / 60 / 90 days
- failed payment attempts
- app open frequency
- average booking lead time
- cancellation rate
- support tickets in last 60 days
- parish usage diversity
- trip type concentration

**Prediction logic**
```python
churn_prob = churn_model.predict_proba(features)[0][1]

if churn_prob > 0.75:
    mark_high_risk(rider_id)
```

### 📋 Implementation Steps
1. Extracted rider behavioral history from ride, payment, and app analytics tables.
2. Defined churn label as inactivity beyond a configured window based on rider segment.
3. Engineered temporal and engagement-based features.
4. Trained XGBoost model with stratified validation.
5. Exposed scores to retention workflows and business intelligence dashboards.

### 🔍 Real-World Scenario
Users in **Bridgetown commuter corridors** who had previously ridden three to five times per week but abruptly reduced activity after fare friction and failed payment attempts were correctly flagged as high-risk.  
This allowed Bimride to identify retention opportunities before users disappeared completely.

### 🧰 Tools & Technologies
| Tool | Purpose |
|------|---------|
| XGBoost | churn modeling |
| Pandas | feature engineering |
| PostgreSQL | rider and trip history |
| FastAPI | scoring service |
| Power BI | churn reporting |

### 📈 KPIs & Metrics
- ROC-AUC: **0.89**
- Precision on top-risk decile: **78%**
- Early-risk detection improvement over rule-based baseline: **+24%**
- Scoring runtime per rider batch: **under 2 seconds**

### ⚠️ Risks & Mitigations
| Risk | Mitigation |
|------|------------|
| Model confuses seasonality with churn | include seasonal usage covariates |
| Tourist riders appear to churn naturally | segment-aware churn labeling |
| Sparse data for newer riders | combine with activation model |
| Retention interventions over-target users | cap intervention frequency |

### ✅ Conclusion
The churn model gave Bimride a more proactive view of retention risk and created a strong analytical base for re-engagement strategy.

---

## 🗓️ 2026-02-08 — Onboarding Intelligence Pipeline
**Author:** Shaun Noronha  

### 🎯 Objective
Identify and reduce friction points in the journey from account creation to first completed trip.

### ⚙️ Architecture Overview
```
[Sign-Up Events]
[Verification Events]
[Payment Link Events]
[First Search / First Booking Events]
        ↓
[Journey Stage Mapper]
        ↓
[Drop-Off Analyzer]
        ↓
[Onboarding Friction Dashboard]
```

### 🧠 Algorithms Used
This was a funnel and transition analysis system rather than a predictive model at first stage.

**Stage sequence**
1. account created
2. identity verified
3. payment method linked
4. first route searched
5. first booking initiated
6. first booking confirmed
7. first trip completed

**Friction rate**
```python
friction_rate = stage_dropoffs / stage_entries
```

A second layer used **logistic regression** to estimate the probability of first-trip completion after a user reached each stage.

### 📋 Implementation Steps
1. Standardized event names across mobile and web onboarding.
2. Built a canonical rider onboarding timeline per user.
3. Measured stage-level falloff and stage transition delay.
4. Ranked the biggest friction points by lost users and delay time.
5. Created operational alerts for unusual onboarding degradation.

### 🔍 Real-World Scenario
New users onboarding from **airport-arrival tourism flows at Grantley Adams Airport** had higher payment-link dropoff than local users, especially when roaming connectivity was weak.  
This surfaced a specific friction point that had previously been buried inside broad acquisition metrics.

### 🧰 Tools & Technologies
| Tool | Purpose |
|------|---------|
| SQL / PostgreSQL | funnel reconstruction |
| Python | transition analysis |
| Power BI | onboarding dashboard |
| Mixpanel-style event exports | session timeline analysis |

### 📈 KPIs & Metrics
- First-trip completion baseline measured end-to-end
- Largest identified dropoff stage: **payment link**
- Average time from sign-up to first trip: **reduced 13% in test flows**
- Funnel observability completeness: **97% of new users**

### ⚠️ Risks & Mitigations
| Risk | Mitigation |
|------|------------|
| Event naming inconsistency | canonical event mapping table |
| Missing session transitions | fallback reconstruction from timestamps |
| False friction caused by tourism patterns | split reporting by rider segment |
| Over-optimizing one stage harms another | full-funnel monitoring |

### ✅ Conclusion
The onboarding intelligence pipeline turned sign-up to first-trip behavior into a measurable and improvable system rather than a black box.

---

## 🗓️ 2026-02-09 — Referral Analytics Engine
**Author:** Shaun Noronha  

### 🎯 Objective
Measure not just how many invites are sent, but how many generate valuable, retained riders.

### ⚙️ Architecture Overview
```
[Referral Invites]
        ↓
[Invite Acceptance Tracker]
        ↓
[New User Conversion Events]
        ↓
[Referral Quality Scorer]
        ↓
[Growth Dashboard]
```

### 🧠 Algorithms Used
The engine used both direct attribution and a **referral quality score** based on post-conversion behavior.

**Referral quality score**
```python
quality_score = (
    0.35 * first_trip_completion +
    0.25 * day7_activity +
    0.20 * payment_success +
    0.20 * repeat_trip_rate
)
```

This made it possible to distinguish:
- high-volume inviters,
- high-quality inviters,
- event-spike inviters,
- and low-conversion spam-like inviters.

### 📋 Implementation Steps
1. Linked referral tokens to invite sender and invitee accounts.
2. Joined referral data with downstream conversion and activity events.
3. Computed invite-to-signup and signup-to-trip conversion rates.
4. Scored quality of acquired users over first 7 and 30 days.
5. Published referral efficiency metrics by parish and campaign.

### 🔍 Real-World Scenario
A cluster of referral growth around **university-linked commuter groups in Bridgetown and nearby student zones** produced fewer total invites than festival-oriented campaigns, but much higher repeat usage and long-term rider quality.

### 🧰 Tools & Technologies
| Tool | Purpose |
|------|---------|
| PostgreSQL | referral joins and attribution |
| Python | scoring logic |
| FastAPI | referral analytics service |
| Power BI | growth dashboards |

### 📈 KPIs & Metrics
- Invite-to-signup conversion tracked by channel
- Quality-weighted referral ROI improved: **+18%**
- Spam-like referral behavior detection improved: **+21%**
- Day-7 retention visibility for referred users: **fully instrumented**

### ⚠️ Risks & Mitigations
| Risk | Mitigation |
|------|------------|
| Last-touch attribution hides true sources | multi-touch reporting view |
| Event campaigns inflate low-quality referrals | quality weighting in dashboards |
| Fraudulent referral loops | invite abuse heuristics |
| Referral source missing | mandatory token mapping |

### ✅ Conclusion
The referral analytics engine helped Bimride shift focus from raw invite volume to meaningful rider acquisition quality.

---

## 🗓️ 2026-02-10 — Rider Activation Scoring Model
**Author:** Shaun Noronha  

### 🎯 Objective
Predict whether a newly registered rider is likely to become active beyond the first trip and identify what signals most strongly influence activation.

### ⚙️ Architecture Overview
```
[New Rider Onboarding Data]
[First Search Events]
[Payment Readiness]
[First Booking Events]
        ↓
[Activation Feature Builder]
        ↓
[Logistic Activation Model]
        ↓
[Activation Score API]
```

### 🧠 Algorithms Used
A **logistic regression baseline plus calibrated probability output** was chosen for interpretability and reliable operational use.

**Activation target**
A rider was considered “activated” if they:
- completed a first trip,
- then returned for at least one additional successful trip within the defined activation window.

```python
activation_prob = activation_model.predict_proba(x)[0][1]
```

### 📋 Implementation Steps
1. Defined activation target using first and second trip behavior.
2. Engineered features from onboarding and early ride-search data.
3. Trained logistic regression with probability calibration.
4. Ranked feature importance and friction drivers.
5. Passed activation scores into CRM and experiment workflows.

### 🔍 Real-World Scenario
New users arriving through **South Coast tourism traffic** often completed a single ride but did not return, while commuter users in **Warrens and Bridgetown** had higher repeat probability.  
The activation score helped distinguish genuinely high-potential riders from one-time transactional users.

### 🧰 Tools & Technologies
| Tool | Purpose |
|------|---------|
| scikit-learn | logistic model |
| Pandas | feature prep |
| PostgreSQL | early lifecycle data |
| Power BI | activation analytics |

### 📈 KPIs & Metrics
- Activation model ROC-AUC: **0.81**
- Lift in top activation decile vs baseline: **+27%**
- First-to-second-trip prediction quality: **strong enough for CRM targeting**
- Score generation time: **under 1 second per batch slice**

### ⚠️ Risks & Mitigations
| Risk | Mitigation |
|------|------------|
| Tourism one-time users distort activation logic | segment-specific target definitions |
| Overuse of scores for messaging | intervention frequency cap |
| Early features too sparse | combine event counts with journey timing |
| Misinterpretation by ops teams | score bands with explanation text |

### ✅ Conclusion
The activation model gave Bimride a much clearer picture of who was likely to become a real rider and where activation leakage was strongest.

---

## 🗓️ 2026-02-11 — Re-engagement Prioritization Service
**Author:** Shaun Noronha  

### 🎯 Objective
Prioritize which inactive riders are worth re-engaging based on recoverability, past value, and likely response to outreach.

### ⚙️ Architecture Overview
```
[Inactive Rider Pool]
        ↓
[Recoverability Scoring Layer]
        ↓
[Value Weighting]
        ↓
[Re-engagement Priority Queue]
        ↓
[CRM / Messaging Export]
```

### 🧠 Algorithms Used
The prioritization score blended:
- churn probability inverse,
- historical rider value,
- recent inactivity window,
- prior campaign response,
- and current zone demand relevance.

```python
priority_score = (
    0.30 * recoverability +
    0.25 * lifetime_value +
    0.20 * recency_fit +
    0.15 * campaign_response +
    0.10 * zone_relevance
)
```

### 📋 Implementation Steps
1. Selected inactive riders above a minimum data threshold.
2. Calculated recoverability from churn and activation-derived features.
3. Weighted scores by rider value and campaign relevance.
4. Bucketed users into high, medium, and low re-engagement priority.
5. Exported ranked audiences for CRM execution.

### 🔍 Real-World Scenario
Users who had previously ridden frequently between **Bridgetown business districts and suburban corridors** but had recently gone inactive were prioritized above low-value one-time festival riders.  
This gave the retention team a more disciplined way to allocate outreach effort.

### 🧰 Tools & Technologies
| Tool | Purpose |
|------|---------|
| Python | ranking logic |
| PostgreSQL | lifecycle feature store |
| FastAPI | prioritization API |
| Power BI | re-engagement dashboard |

### 📈 KPIs & Metrics
- High-priority audience precision improved over simple inactivity filters
- CRM targeting efficiency: **up 23% in simulation**
- Wasteful outreach to low-recovery users: **down 17%**
- Batch ranking runtime: **under 3 minutes**

### ⚠️ Risks & Mitigations
| Risk | Mitigation |
|------|------------|
| High-value users over-prioritized despite no recoverability | hard minimum recoverability threshold |
| Outreach fatigue | suppression windows |
| Value bias against new but promising users | dedicated emerging-user bucket |
| Campaign overlap | audience lock and deduplication |

### ✅ Conclusion
The prioritization service helped Bimride target re-engagement more intelligently and avoid treating all inactive users as equally valuable recovery candidates.

---

## 🗓️ 2026-02-12 — Loyalty Segmentation Framework
**Author:** Shaun Noronha  

### 🎯 Objective
Classify riders into meaningful loyalty and usage archetypes that reflect how Bimride is actually used across Barbados.

### ⚙️ Architecture Overview
```
[Ride Frequency]
[Trip Timing]
[Zone Diversity]
[Average Spend]
[Modality Usage]
        ↓
[Segmentation Engine]
        ↓
[Loyalty Archetype Labels]
        ↓
[Analytics + CRM + Pricing Inputs]
```

### 🧠 Algorithms Used
This framework used a combination of:
- rules-based archetype assignment for business clarity,
- and cluster validation to test whether archetypes aligned with real usage patterns.

**Primary loyalty segments**
- weekday commuter
- occasional local rider
- tourism-heavy rider
- nightlife / event rider
- price-sensitive infrequent rider
- high-value recurring user

### 📋 Implementation Steps
1. Built rider-level longitudinal usage summaries.
2. Defined behavioral thresholds and loyalty archetypes.
3. Validated archetypes against unsupervised clustering output.
4. Measured transition movement between archetypes month over month.
5. Published segment-level trends to analytics dashboards.

### 🔍 Real-World Scenario
Riders concentrated in **South Coast nightlife and event corridors** behaved very differently from weekday **Bridgetown commuter** users, especially on fare sensitivity and time-of-day patterns.  
The framework helped formalize those differences into actionable segments.

### 🧰 Tools & Technologies
| Tool | Purpose |
|------|---------|
| Python | segmentation logic |
| scikit-learn | cluster validation |
| PostgreSQL | rider summaries |
| Power BI | loyalty analytics |

### 📈 KPIs & Metrics
- Segment coverage across active riders: **high and stable**
- Segment-to-segment transition visibility: **month over month**
- Marketing and pricing relevance improved for downstream teams
- Loyalty dashboards adopted by growth and ops stakeholders

### ⚠️ Risks & Mitigations
| Risk | Mitigation |
|------|------------|
| Archetypes too rigid | allow mixed-behavior review rules |
| Segments become stale | monthly refresh process |
| Tourism spikes distort labels | season-aware thresholds |
| Teams overfit campaigns to one label | include confidence scores |

### ✅ Conclusion
The loyalty framework gave Bimride a clearer map of rider behavior and improved the alignment between analytics, retention, and service design.

---

## 🗓️ 2026-02-13 — Rider Funnel Intelligence Dashboard
**Author:** Shaun Noronha  

### 🎯 Objective
Create one operational view that connects acquisition, onboarding, activation, retention, churn, referral quality, and re-engagement.

### ⚙️ Architecture Overview
```
[Acquisition Data]
[Onboarding Funnel]
[Activation Scores]
[Churn Scores]
[Referral Metrics]
[Re-engagement Rankings]
        ↓
[Funnel Intelligence Warehouse]
        ↓
[Executive + Ops Dashboard]
```

### 🧠 Algorithms Used
This dashboard was a consolidated intelligence layer rather than a standalone ML model.  
It unified output from multiple systems:
- funnel stage counts,
- conversion rates,
- activation probability,
- churn probability,
- referral quality score,
- re-engagement priority score.

### 📋 Implementation Steps
1. Standardized rider identifiers across lifecycle systems.
2. Created a funnel warehouse table with rider-stage status.
3. Joined predictive scores into stage-level analytics.
4. Added drilldowns by parish, segment, and acquisition source.
5. Published dashboard views for growth, ops, and leadership.

### 🔍 Real-World Scenario
Leadership teams reviewing growth in **Bridgetown, South Coast, and airport-connected tourism flows** could finally see which channels generated:
- good signup volume,
- strong first-trip completion,
- and real retained riders.

This removed a major blind spot where acquisition volume had previously been mistaken for healthy growth.

### 🧰 Tools & Technologies
| Tool | Purpose |
|------|---------|
| PostgreSQL | funnel warehouse |
| Python | metric synthesis |
| Power BI | dashboard presentation |
| FastAPI | analytics serving layer |

### 📈 KPIs & Metrics
- Full rider lifecycle observability established
- Decision latency for growth reviews: **reduced materially**
- Cross-team alignment on rider health improved
- Dashboard refresh SLA: **under 15 minutes**

### ⚠️ Risks & Mitigations
| Risk | Mitigation |
|------|------------|
| Metric inconsistency across teams | canonical metric definitions |
| Duplicate rider-state logic | central funnel computation layer |
| Dashboard overload | role-based dashboard views |
| Stale predictive scores | scheduled score refresh pipeline |

### ✅ Conclusion
The funnel intelligence dashboard made Bimride’s growth and retention systems far more interpretable, tying together the full rider lifecycle in one place.

---

## 🚧 Challenges Faced
- Churn and activation definitions needed segmentation-aware logic to avoid misclassifying tourist riders.
- Onboarding event quality varied across app flows and required cleanup.
- Referral volume alone proved misleading without quality weighting.
- Re-engagement prioritization needed careful suppression rules to avoid user fatigue.
- Lifecycle dashboards required strict metric governance to keep teams aligned.

---

## 🏁 Conclusion
Week 2 of February gave Bimride a significantly stronger foundation in **growth intelligence, rider lifecycle visibility, and retention strategy**.  
By connecting churn prediction, onboarding analytics, referral quality, activation scoring, re-engagement logic, loyalty segmentation, and funnel reporting, the platform became better equipped to grow sustainably while preserving service quality and community trust.
