# Energy-Aware Routing for Electric Vehicles

**Date:** 08-30-2025  
**Author:** Shaun Noronha

---

## 🚀 Introduction

Energy constraints change routing: an EV must arrive with safe reserve and may require a charging stop. We adapt shortest-path to respect battery limits and charger availability.

---

## ⚙️ Architecture Overview


```
[Road Graph + Elevation] + [Chargers] + [SoC] -> [Energy-Constrained Dijkstra] -> [Route + Stops]
```
Notes:
- Slope-adjusted energy model; avoid steep climbs when marginal.
- Charger status pulled every 5 minutes; routes recomputed if station goes offline.


---

## 🧠 Algorithms Used

```python
import heapq, math

def dijkstra_energy(graph, start, goal, kwh, eff_km_per_kwh=6.0, reserve=0.5):
    # graph: {node: [(nbr, dist_km, slope)]}
    pq = [(0, start, kwh)]  # (cost, node, remaining_kwh)
    seen = set()
    while pq:
        cost, node, rem = heapq.heappop(pq)
        if (node, round(rem,2)) in seen: 
            continue
        seen.add((node, round(rem,2)))
        if node == goal and rem >= reserve: 
            return cost
        for nbr, dist, slope in graph.get(node, []):
            # simple slope factor
            energy = dist/eff_km_per_kwh * (1 + 0.3*max(0,slope))
            if rem - energy >= 0:
                heapq.heappush(pq, (cost+dist, nbr, rem-energy))
    return math.inf
```

---

## 🔁 MLOps Workflow Example

```yaml
name: ev-routing-nightly
on:
  schedule:
    - cron: "0 1 * * *"
jobs:
  refresh-elevation-chargers-train:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Update elevation tiles
        run: python data/elevation_sync.py --region barbados
      - name: Sync charger status
        run: python data/chargers_sync.py --provider all
      - name: Validate energy model
        run: python models/validate_energy.py --mae-threshold 0.12
```

---

## 🔍 Real-World Scenario

A taxi in **Harrison’s Cave** at 35% SoC gets routed via a reliable charger, arriving at the destination with 12% reserve despite hills.

---

## 📊 Tools and Technologies


| Component                | Tool/Tech                          |
|--------------------------|------------------------------------|
| Routing                  | OSRM / Valhalla + custom energy    |
| Data                     | SRTM elevation + charger feeds     |
| Serving                  | gRPC microservice                  |
| Caching                  | Redis                               |
| Infra                    | AKS + Spot nodes for batch         |


---

## ✅ Conclusion

This work on **Energy-Aware Routing for Electric Vehicles** is tailored to Bimride’s Barbados context and serves as a concrete, auditable progress artifact.
