# 📅 Day 2: Mobile Location Polling & Battery Optimization

### 🎯 Objective
Design an efficient system for location tracking on mobile devices that balances GPS accuracy with minimal battery consumption.

---

## 📍 Tracking Strategy

### 🧭 Location Tracking Modes
- **Foreground Tracking**: High frequency, highest accuracy, used when ride is active.
- **Background Tracking**: Reduced frequency, optimized for battery, used when user is idle or app is minimized.
- **Trip-Aware Polling**: Dynamic polling interval. For example:
  - Near pickup: High-frequency updates.
  - Mid-trip: Medium-frequency updates.
  - Idle/waiting: Low-frequency updates.

---

## 🔋 Battery Optimization Techniques

| Technique                             | Benefit                                                |
|--------------------------------------|---------------------------------------------------------|
| **Geofencing**                       | Activates high-precision updates only near key trip points. |
| **Adaptive Polling**                 | Decreases GPS polling when speed or movement is low.    |
| **Motion Sensors (Accelerometer/Gyro)** | Prevents GPS polling if the phone hasn't moved.     |
| **OS-Specific APIs**                 | Uses native features like Android ActivityRecognition or iOS Significant Location Changes to reduce battery use. |
| **Batch Updates**                    | Buffers and sends location in grouped batches to reduce wake-ups. |

---

## 📲 Mobile Architecture & Flow

- **Native OS Features:**
  - `FusedLocationProviderClient` for Android
  - `CoreLocation` for iOS

- **Tracking States**:
  - Background / Foreground / Terminated

- **Data Transmission**:
  - Primary channel: WebSocket (or MQTT)
  - Fallback: HTTPS (REST API)

- **Offline Handling**:
  - SQLite or local JSON used for temporarily storing location data
  - Retry mechanism for automatic sync once connectivity is restored

---

## 🧪 Sample Polling Logic

```python
if app_state == "foreground" and trip_status == "in_progress":
    polling_interval = 2  # seconds
elif trip_status in ["waiting", "en_route"]:
    polling_interval = 5–10
elif app_state == "background":
    polling_interval = 30–60
elif motion_detected == False:
    polling_interval = None  # disable temporarily
```

## 🧰 Tools & Libraries

### React Native:
- `react-native-background-geolocation`
- `expo-location`

### Native Android/iOS:
- **Android**: `FusedLocationProvider`, `WorkManager`, `JobScheduler`
- **iOS**: `CLLocationManager`, `BGAppRefreshTask`, `CLVisit`

### Storage:
- `SQLite`, `AsyncStorage`, or `Room`

### Profiling:
- **Android**: Battery Historian  
- **iOS**: Instruments

---

## 🧠 Edge Case Handling

| Scenario                    | Strategy                                              |
|-----------------------------|-------------------------------------------------------|
| Phone loses GPS             | Use last known location + predictive movement         |
| User disables location access | Trigger fallback alert and prompt user permissions |
| Device offline              | Store locally and retry in background                 |
| App killed by OS            | Use native background task APIs                       |

---

## 📌 Deliverables for Day 2

- ✅ Foreground vs background mode-switching strategy implemented
- ✅ Adaptive polling with motion detection logic
- ✅ Energy profiling & benchmark targets defined
- ✅ Fallback mechanisms for offline and OS-level terminations
- ✅ Full mobile architecture designed for location syncing
