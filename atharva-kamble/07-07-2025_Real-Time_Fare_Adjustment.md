# Real-Time Fare Adjustment Using Sliding Window Average

**LeetCode Tie-In**: Sliding Window Maximum / Moving Average
**Bimride Use**: Dynamic pricing based on live demand or surge zones

---

## 🚩 Problem Statement

In a real-world ride-hailing application like Bimride, surge pricing is often applied when there's a spike in rider demand or a shortage of available drivers.

To prevent sudden spikes and drops in fare, the system must calculate a **real-time moving average** of recent ride prices or demand values over a fixed time window. This helps determine when to apply surge pricing.

This scenario matches the classic **sliding window average** problem from LeetCode, where we compute the average of the last `k` entries in a continuous stream.

---

## ✅ Final Solution (Python)

```python
from collections import deque
from typing import List

class MovingAverage:
    def __init__(self, size: int):
        self.window = deque()
        self.max_size = size
        self.sum = 0

    def next(self, val: int) -> float:
        self.window.append(val)
        self.sum += val

        if len(self.window) > self.max_size:
            removed = self.window.popleft()
            self.sum -= removed

        return self.sum / len(self.window)

# Example: Moving Average Fare Calculation
fare_avg = MovingAverage(3)
print(fare_avg.next(10))  # 10.0
print(fare_avg.next(20))  # 15.0
print(fare_avg.next(30))  # 20.0
print(fare_avg.next(40))  # 30.0 (oldest value 10 removed)
```

---

## 🧰 Data Structure

* **Deque (collections.deque)**: Efficient O(1) insertions/removals from both ends.
* **Running Sum**: Maintains current sum of the elements inside the window.

---

## ⚙️ Time and Space Complexity

| Metric | Value                             |
| ------ | --------------------------------- |
| Time   | O(1) per operation                |
| Space  | O(k) where k = size of the window |

Efficient for streaming use cases where new values arrive every second or minute.

---

## 🧼 Clean Code Practices

* Used `deque` for constant-time pop/append
* Maintains a `sum` variable for fast average computation
* Clear separation of initialization and logic

---

## 🧠 Why This Matters for Bimride

This technique enables:

1. **Surge Pricing Decisions**:

   * Use the moving average of trip volume or wait time to decide when surge multipliers apply.

2. **Smoothing Outliers**:

   * Averages over time reduce the effect of sudden high or low trip fares.

3. **Demand Prediction**:

   * Feed these averages into a time-series model or dashboard to prepare for upcoming spikes.

4. **Real-Time Dashboards**:

   * Use moving average fare across cities/zones for pricing insights.

---

## 📊 Visual Interpretation (Conceptual)

If trip demand over 10 minutes = `[4, 8, 6, 7, 10, 12]`, and window = 3:

The sliding window averages would be:

```
(4+8+6)/3 = 6.0
(8+6+7)/3 = 7.0
(6+7+10)/3 = 7.67
(7+10+12)/3 = 9.67
```

---

## 🔄 Real-World Extensions

* Use weighted averages (give more weight to recent fares)
* Pair this logic with a pricing API and demand metrics
* Extend to rolling median or quantile calculations for more robust surge triggers
* Visualize live fare windows on operational dashboards

---

## 🚗 Relevance to Bimride

| Use Case                 | Sliding Window Role                                 |
| ------------------------ | --------------------------------------------------- |
| Dynamic fare calculation | Compute smoothed fare to reduce jitter              |
| Live demand mapping      | Track average rides per minute/hour                 |
| Wait-time alerting       | Raise alerts if avg wait crosses threshold          |
| Resource allocation      | Adjust driver distribution based on rolling average |

This creates a system where pricing, driver distribution, and rider communication remain responsive and stable.

---

## 🔚 Conclusion

Sliding window average is a core technique for **stream processing** in real-time applications. For Bimride, it ensures:

* Accurate surge pricing
* Fair fare adjustments
* Smooth user experiences
* Demand-aware driver coordination

By learning from the Moving Average LeetCode problem, we can translate a simple data structure into a **dynamic pricing microservice** that powers a smarter ride-hailing backend.
