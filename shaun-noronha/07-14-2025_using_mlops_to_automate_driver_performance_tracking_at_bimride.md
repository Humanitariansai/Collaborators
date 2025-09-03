# Using MLOps to Automate Driver Performance Tracking at Bimride

**Date:** 07-14-2025  
**Author:** Shaun Noronha

---

## 🚀 Introduction

In this technical document, we explore the application of **Using MLOps to Automate Driver Performance Tracking at Bimride** to improve Bimride’s intelligent transportation system in Barbados. This deep dive addresses how cutting-edge concepts in AI, MLOps, and Data Structures & Algorithms (DSA) can create a smarter, more reliable taxi network.

---

## ⚙️ Architecture Overview

---

## 🧠 Algorithms Used

### Example: Dynamic Pricing with Heaps

```python
import heapq

def dynamic_fare(base_fare, surge_factors):
    max_heap = [-x for x in surge_factors]
    heapq.heapify(max_heap)
    return base_fare * -heapq.heappop(max_heap)
```

---

## 🔁 MLOps Workflow Example

```yaml
# .github/workflows/train-model.yml
name: Train Model

on:
  push:
    paths:
      - 'data/**'
      - 'models/**'

jobs:
  train:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run training
        run: |
          python train_model.py
      - name: Track with DVC
        run: |
          dvc add data/
          dvc push
```

---

## 🔍 Real-World Scenario

**Use Case**: Bimride wants to forecast **ride demand** across Bridgetown using weather, time, and location data.

**Solution**: Train an XGBoost model using historical rides + external weather API data. Serve model through FastAPI for the Bimride app.

---

## 📊 Tools and Technologies

| Component            | Tool/Tech               |
|----------------------|-------------------------|
| Model Training       | PyTorch, Scikit-learn   |
| Deployment           | FastAPI + Docker        |
| Pipeline Orchestration | GitHub Actions, DVC   |
| Visualization        | Grafana + Prometheus    |
| Storage              | Delta Lake + Azure Blob |

---

## ✅ Conclusion

The integration of **Using ML**
