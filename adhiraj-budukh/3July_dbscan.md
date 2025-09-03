## DBSCAN (Density-Based Spatial Clustering of Applications with Noise)

## 1. Introduction

As a follow-up to our K-Means clustering article, we now explore **DBSCAN**, a density-based clustering algorithm ideal for detecting spatial patterns in ride-hailing data without requiring the number of clusters `k` in advance. This approach is particularly useful in cities where demand zones are irregular and constantly shifting.

---

## 2. Problem Statement

How can BimRide identify dynamic pickup clusters in high-density zones like downtown or near event venues, where:
- The number of clusters is unknown
- Cluster shapes are irregular
- Outliers or noise (rare requests) exist

---

## 3. Algorithm Overview: DBSCAN

### 3.1 Core Concepts

DBSCAN groups points that are closely packed together (high density) and marks isolated points (low density) as outliers.

Key parameters:
- `eps`: Maximum distance between two points to be in the same cluster
- `min_samples`: Minimum number of points to form a dense region

### 3.2 How It Works

1. Choose a point at random.
2. Find all points within `eps`.
3. If the number of neighbors ≥ `min_samples`, a cluster is formed.
4. Expand the cluster by recursively applying steps 2–3 to neighbors.
5. Label remaining points as noise.

---

## 4. Challenges Faced

### 4.1 Parameter Sensitivity
- **Problem**: Inappropriate `eps` or `min_samples` leads to poor clusters.
- **Solution**: Use **k-distance graph** to find optimal `eps`.

### 4.2 Performance with Large Datasets
- **Problem**: DBSCAN’s complexity is O(n²) in naive form.
- **Solution**: Use optimized implementations (e.g., `scikit-learn`) with KD-Trees or Ball Trees.

### 4.3 Inconsistent Cluster Sizes
- **Problem**: DBSCAN may split large areas or merge small ones.
- **Solution**: Use **HDBSCAN** for hierarchical density clustering.

---

## 5. Implementation in Python

### 5.1 Dataset
Simulated ride request data from various zones in BimRide (lat, lon, timestamps)

### 5.2 Sample Code

```python
from sklearn.cluster import DBSCAN
import pandas as pd
import matplotlib.pyplot as plt
from geopy.distance import great_circle
from sklearn.preprocessing import StandardScaler

# Load dataset
data = pd.read_csv("bimride_requests.csv")
coords = data[['latitude', 'longitude']]
coords_scaled = StandardScaler().fit_transform(coords)

# Apply DBSCAN
db = DBSCAN(eps=0.3, min_samples=10).fit(coords_scaled)
data['cluster'] = db.labels_

# Visualize
plt.scatter(data['longitude'], data['latitude'], c=data['cluster'], cmap='tab10')
plt.title("DBSCAN Ride Demand Clusters")
plt.xlabel("Longitude")
plt.ylabel("Latitude")
plt.show()
```