# Partnership Analytics with Local Businesses

**Date:** 08-31-2025  
**Author:** Shaun Noronha

---

## 🚀 Introduction

Partnerships with hotels, restaurants, and tour operators drive growth. We quantify partner performance and optimize commissions transparently.

---

## ⚙️ Architecture Overview


```
[Referral Clicks] + [Ride Logs] -> [Attribution Model] -> [Partner Scorecard API]
                                          |
                                          v
                                   [Commission Engine]
```
- Multi-touch attribution splits credit when riders browse multiple partners.
- Outlier detection flags suspicious referral spikes.


---

## 🧠 Algorithms Used

```python
import pandas as pd

def partner_kpi(df):
    # df columns: partner, rides, revenue, commission_rate
    df = df.copy()
    df["net"] = df["revenue"] - df["revenue"]*df["commission_rate"]
    grouped = df.groupby("partner").agg(rides=("rides","sum"),
                                        revenue=("revenue","sum"),
                                        net=("net","sum")).reset_index()
    grouped["roi"] = (grouped["net"] / grouped["revenue"]).round(3)
    return grouped.sort_values("roi", ascending=False)

sample = pd.DataFrame({
    "partner":["Hotel A","Tour B","Restaurant C","Hotel A"],
    "rides":[120,80,60,95],
    "revenue":[3600,2400,900,2800],
    "commission_rate":[0.18,0.20,0.12,0.18]
})
print(partner_kpi(sample))
```

---

## 🔁 MLOps Workflow Example

```yaml
name: partner-analytics-monthly
on:
  schedule:
    - cron: "0 3 1 * *" # 1st of each month
jobs:
  aggregate-scorecard:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Install
        run: pip install -r analytics/requirements.txt
      - name: Build attribution model
        run: python analytics/attribution.py --lookback 7d
      - name: Publish partner scorecards
        run: python analytics/publish.py --dest s3://bimride/partners
```

---

## 🔍 Real-World Scenario

In **Holetown (St. James)**, a boutique hotel drives high-value rides with minimal discounts. The scorecard recommends a small commission bump and co-marketing through Bimride ads.

---

## 📊 Tools and Technologies


| Component                | Tool/Tech                          |
|--------------------------|------------------------------------|
| Analytics                | Pandas + DuckDB                    |
| Warehousing              | Delta Lake + Azure Blob            |
| Dashboards               | Metabase / Power BI                |
| Serving                  | FastAPI + PostgREST                |
| Alerts                   | Grafana + email/webhooks           |


---

## ✅ Conclusion

This work on **Partnership Analytics with Local Businesses** is tailored to Bimride’s Barbados context and serves as a concrete, auditable progress artifact.
