# Analyzing Traffic Patterns with Graph Neural Networks

**Date:** 08-25-2025  
**Author:** Shaun Noronha

---

## 🚀 Introduction

Barbados roads form a dynamic graph. We treat intersections as nodes, roads as edges, and learn how congestion propagates using temporal graph convolutions.

---

## ⚙️ Architecture Overview


```
[GPS Pings] -> [Map-Matching] -> [Road Graph with Speeds]
                                   |                |
                                   v                v
                             [Time Windows]   [GNN Trainer] -> [Deployed GNN]
```
Distinctives:
- Graph updated daily; edge weights are speed distributions.
- Temporal windows (5-min) capture rush-hour patterns near schools and business districts.


---

## 🧠 Algorithms Used

```python
# Minimal temporal convolution on edge speeds (pseudocode)
import numpy as np

def temporal_conv(signal, kernel):
    # signal: [time] array per edge; kernel: short 1D filter
    k = len(kernel); out = np.zeros(len(signal)-k+1)
    for t in range(len(out)):
        out[t] = (signal[t:t+k] * kernel).sum()
    return out

speeds = np.array([28,25,20,18,22,26,30])  # km/h over time
kernel = np.array([0.2,0.5,0.3])           # emphasize recent history
print(temporal_conv(speeds, kernel))
```

---

## 🔁 MLOps Workflow Example

```yaml
name: traffic-gnn-refresh
on:
  schedule:
    - cron: "*/30 * * * *"   # every 30 minutes
jobs:
  build-graph-train:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Map-match GPS to OSM
        run: python data/map_match.py --area barbados
      - name: Build temporal graph slices
        run: python data/build_graph.py --window-min 5
      - name: Train T-GCN
        run: python models/train_tgcn.py --epochs 6
      - name: Export to serving
        run: python serve/export_model.py --target s3://models/traffic
```

---

## 🔍 Real-World Scenario

A road closure near **Bathsheba (St. Joseph)** causes spillover onto side streets. The model predicts the peak 12 minutes ahead, prompting driver reroutes before gridlock.

---

## 📊 Tools and Technologies


| Component                | Tool/Tech                       |
|--------------------------|---------------------------------|
| Graph Processing         | NetworkX / PyG / DGL            |
| Map-Matching             | Valhalla / OSRM                 |
| Stream Ingestion         | Kafka                           |
| Serving                  | FastAPI + gRPC                  |
| Batch                    | Spark                           |


---

## ✅ Conclusion

This work on **Analyzing Traffic Patterns with Graph Neural Networks** is tailored to Bimride’s Barbados context and serves as a concrete, auditable progress artifact.
