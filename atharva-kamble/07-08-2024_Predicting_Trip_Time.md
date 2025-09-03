# Predicting Trip Time Using Linear Regression

**Concept**: Supervised Learning – Linear Regression
**Bimride Use**: Accurate ETA (Estimated Time of Arrival) prediction based on trip distance, pickup time, and traffic indicators

---

## 🚩 Problem Statement

Riders expect reliable arrival estimates when booking rides. Poor ETA predictions lead to dissatisfaction and operational inefficiencies.

Using a simple machine learning technique like **Linear Regression**, Bimride can create a lightweight model to predict trip duration based on historical ride data. This provides a real-time ETA at booking and improves routing, driver dispatch, and rider experience.

---

## ✅ Final Code (Python using scikit-learn)

```python
import pandas as pd
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_absolute_error, r2_score

# Sample mock dataset (trip features)
data = {
    'distance_km': [2.5, 7.0, 3.3, 5.0, 8.8, 10.2],
    'pickup_hour': [8, 14, 17, 9, 18, 20],
    'traffic_level': [2, 3, 4, 1, 4, 5],  # 1=Low, 5=High
    'trip_duration_min': [10, 25, 20, 12, 35, 40]
}

# Convert to DataFrame
trip_df = pd.DataFrame(data)

# Define features and target
X = trip_df[['distance_km', 'pickup_hour', 'traffic_level']]
y = trip_df['trip_duration_min']

# Train-test split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Build model
model = LinearRegression()
model.fit(X_train, y_train)

# Predict
y_pred = model.predict(X_test)

# Evaluation
print("MAE:", mean_absolute_error(y_test, y_pred))
print("R2 Score:", r2_score(y_test, y_pred))
```

---

## 🧰 Features and Data Engineering

* `distance_km`: Distance between pickup and drop (in kilometers)
* `pickup_hour`: Extracted from timestamp (captures rush hours)
* `traffic_level`: Proxy for congestion; optionally from an API

Can be expanded with:

* Weather info (rain = slower travel)
* Road closures or events
* Day of week / weekend flag

---

## ⚙️ Model Evaluation

| Metric   | Description                         |
| -------- | ----------------------------------- |
| MAE      | Average absolute error in minutes   |
| R² Score | How well model explains variability |

For real deployment:

* Use larger datasets (thousands of rides)
* Periodically retrain with fresh data
* Monitor model drift during peak vs off-peak hours

---

## 📊 Visual Example (Regression Line)

Plotting predicted vs actual trip durations:

```
     |      /
     |     /       * actual
trip |    /-------- predicted
 time|
     |_____________________
         distance (km) →
```

---

## 🚗 Relevance to Bimride

| Use Case              | Impact of Prediction            |
| --------------------- | ------------------------------- |
| Rider app ETA display | Improves trust and planning     |
| Driver dispatching    | Better route selection          |
| Pool ride batching    | More accurate merging of trips  |
| Surge pricing models  | Traffic-adjusted time component |

By applying even a basic regression model, Bimride can provide **smart ETAs** that outperform static rules or average speeds.

---

## 🔄 Real-World Extensions

* Use **XGBoost** or **Random Forests** for non-linear relationships
* Integrate real-time traffic APIs (Google, HERE)
* Build a microservice that takes pickup/drop coords and returns ETA
* Retrain nightly with new trip data

---

## 🔚 Conclusion

Trip duration prediction is a foundational element of any ride-hailing app. Linear Regression provides a simple but effective baseline that Bimride can build upon.

It enables:

* More accurate ETAs
* Better rider communication
* Efficient resource management
* Smarter dispatching systems

With just a few features, we can dramatically improve both rider and driver satisfaction.
