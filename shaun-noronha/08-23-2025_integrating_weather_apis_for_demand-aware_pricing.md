# Integrating Weather APIs for Demand-Aware Pricing

**Date:** 08-23-2025  
**Author:** Shaun Noronha

---

## 🚀 Introduction

Bimride pricing responds to real-world conditions. Rain bands crossing the Atlantic often trigger sharp demand spikes in Barbados. By integrating **hourly forecasts** and **nowcasts** into the pricing engine, we can pre-position drivers and smooth surge.

---

## ⚙️ Architecture Overview


```
[Mobile App] --telemetry--> [Ingress API]
                         \-> [Weather ETL] -> [Feature Store]
[Pricing Service] <------ features -------- [Demand Model]
[Driver App] <----------- surge factors ---- [Pricing Service]
```
Key design points:
- Feature Store keeps hourly weather features (precip_mm, wind_kph, humidity, lightning_alert).
- Pricing service clamps surge to avoid price shocks; cache prevents API overuse.


---

## 🧠 Algorithms Used

```python
import math

def surge_factor(hour, precip_mm, wind_kph, temp_c, event_score):
    # Cyclical time features for hour-of-day
    hsin, hcos = math.sin(2*math.pi*hour/24), math.cos(2*math.pi*hour/24)
    # Linear model calibrated offline
    surge = 1.0 + 0.02*precip_mm + 0.005*wind_kph - 0.003*max(temp_c-30,0) + 0.15*event_score             + 0.05*hsin + 0.03*hcos
    return max(1.0, min(2.5, round(surge, 2)))
```

---

## 🔁 MLOps Workflow Example

```yaml
name: weather-pricing-train
on:
  schedule:
    - cron: "0 * * * *"   # hourly refresh of features
  workflow_dispatch:
jobs:
  features-train-eval:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Install
        run: pip install -r requirements.txt
      - name: Fetch weather & build features
        run: python pipelines/weather_features.py --region "Barbados"
      - name: Retrain demand model
        run: python models/train_weather_pricing.py --hours 168
      - name: Backtest & threshold check
        run: python models/backtest.py --metric rmse --limit 0.12
      - name: Publish surge policy
        run: python deploy/publish_policy.py --env prod
```

---

## 🔍 Real-World Scenario

During a sudden downpour near **Grantley Adams International Airport (BGI)**, the model predicts a 22% demand surge. The policy raises surge to 1.25, notifies idle drivers to move toward rainy zones, and caps prices to avoid rider churn.

---

## 📊 Tools and Technologies


| Component                | Tool/Tech                         |
|--------------------------|-----------------------------------|
| Weather Data             | Meteomatics/NOAA API, local cache |
| Feature Store            | Feast + Delta Lake                |
| Models                   | LightGBM, StatsModels             |
| Serving                  | FastAPI, Redis (feature cache)    |
| Orchestration            | GitHub Actions + DVC              |
| Monitoring               | Prometheus + Grafana              |


---

## ✅ Conclusion

This work on **Integrating Weather APIs for Demand-Aware Pricing** is tailored to Bimride’s Barbados context and serves as a concrete, auditable progress artifact.
