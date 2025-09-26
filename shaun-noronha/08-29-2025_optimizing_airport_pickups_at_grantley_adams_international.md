# Optimizing Airport Pickups at Grantley Adams International

**Date:** 08-29-2025  
**Author:** Shaun Noronha

---

## 🚀 Introduction

Airport demand arrives in waves aligned to flight schedules. We create a pickup controller that balances fairness and minimal wait time.

---

## ⚙️ Architecture Overview


```
[Flight API] -> [Arrival Batches] -> [Pickup Controller] -> [Driver Queue]
                                                 |                 |
                                                 v                 v
                                            [Rider Queue] <-match-> [Assignment]
```
Mechanics:
- Drivers rotate through a virtual queue when inside airport geofence.
- Batch assignment before simultaneous landings reduces chaos at curbside.


---

## 🧠 Algorithms Used

```python
import heapq, time

def assign(flights, drivers, now_ts):
    # flights: [(eta_ts, flight_id)]
    # drivers: [(idle_ts, driver_id)]
    heapq.heapify(flights); heapq.heapify(drivers)
    match = []
    while flights and drivers and flights[0][0] <= now_ts + 15*60:
        eta, f = heapq.heappop(flights)
        idle, d = heapq.heappop(drivers)
        match.append((f, d))
    return match
```

---

## 🔁 MLOps Workflow Example

```yaml
name: airport-pickups-controller
on:
  push:
    paths:
      - 'airport/**'
jobs:
  build-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Lint & Test
        run: pytest -q
      - name: Build image
        run: docker build -t bimride/airport:$GITHUB_SHA airport/
      - name: Deploy
        run: python deploy/rollout.py --service airport --strategy canary
```

---

## 🔍 Real-World Scenario

At **Bridgetown**, two wide-bodies arrive 10 minutes apart. The controller forms two assignment batches to keep both riders and drivers flowing.

---

## 📊 Tools and Technologies


| Component                | Tool/Tech                          |
|--------------------------|------------------------------------|
| Flight Data              | Aviation API / ACARS feed          |
| Geofencing               | PostGIS + H3                       |
| Queueing                 | Redis Streams                      |
| Serving                  | FastAPI + Celery workers           |
| Infra                    | AKS + Horizontal Pod Autoscaler    |


---

## ✅ Conclusion

This work on **Optimizing Airport Pickups at Grantley Adams International** is tailored to Bimride’s Barbados context and serves as a concrete, auditable progress artifact.
