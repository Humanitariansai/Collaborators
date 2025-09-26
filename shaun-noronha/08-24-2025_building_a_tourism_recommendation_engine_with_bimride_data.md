# Building a Tourism Recommendation Engine with Bimride Data

**Date:** 08-24-2025  
**Author:** Shaun Noronha

---

## 🚀 Introduction

Bimride can act as a **tour guide** by recommending attractions that match rider tastes. We blend collaborative filtering with POI embeddings (beach, food, culture) and context (cruise day, weather).

---

## ⚙️ Architecture Overview


```
[Ride Events] -> [Sessionization] -> [User-POI Matrix] -> [MF/Embeddings] -> [Re-ranker]
                                       ^                                    |
[POI Catalog, Reviews, Tags] ----------|------------------------------------+
```
Notes:
- Re-ranker boosts diversity and distance-aware novelty to reduce echo-chambers.
- Cold-start handled by popularity within 5km + weather-aware beach multipliers.


---

## 🧠 Algorithms Used

```python
import numpy as np

def softmax(x): 
    ex = np.exp(x - np.max(x))
    return ex / ex.sum()

def rerank(base_scores, distance_km, category_penalty):
    # Encourage diverse categories and penalize far POIs
    s = base_scores - 0.1*distance_km - 0.2*category_penalty
    return softmax(s)

base = np.array([3.2, 2.1, 1.4, 2.7])
dist = np.array([1.0, 8.2, 4.3, 2.0])
catp = np.array([0.0, 1.0, 0.0, 0.5])  # penalize repeated categories
print(rerank(base, dist, catp))
```

---

## 🔁 MLOps Workflow Example

```yaml
name: tourism-recsys-train
on:
  schedule:
    - cron: "0 2 * * 1"   # weekly
  workflow_dispatch:
jobs:
  train-eval-export:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Install
        run: pip install -r requirements.txt
      - name: Build user-POI interactions
        run: python data/build_interactions.py --window 90d
      - name: Train MF + POI embeddings
        run: python models/train_recsys.py --k 64 --epochs 15
      - name: Evaluate (CTR@5, NDCG)
        run: python models/evaluate_recsys.py --min_ndcg 0.28
      - name: Export top-k index
        run: python serve/export_ann.py --k 200
```

---

## 🔍 Real-World Scenario

On a cruise day at **Grantley Adams International Airport (BGI)**, visitors who liked Carlisle Bay yesterday see varied recommendations: Bathsheba (scenic), Oistins (food), and Harrison’s Cave (indoor option if rainy).

---

## 📊 Tools and Technologies


| Component                | Tool/Tech                                |
|--------------------------|------------------------------------------|
| Modeling                 | Implicit MF, SentenceTransformers        |
| Vector Index             | FAISS / ScaNN                            |
| Data Pipeline            | Spark + Delta Tables                     |
| Serving                  | FastAPI + ANN service                    |
| Offline Eval             | MLflow + custom CTR dashboard            |
| Orchestration            | GitHub Actions + DVC                     |


---

## ✅ Conclusion

This work on **Building a Tourism Recommendation Engine with Bimride Data** is tailored to Bimride’s Barbados context and serves as a concrete, auditable progress artifact.
