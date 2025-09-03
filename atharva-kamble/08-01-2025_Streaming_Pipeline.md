# 📅 Day 3: Backend Streaming Pipeline & Real-Time Display Layer

## 🎯 Objective
Design a scalable and low-latency backend streaming system that ingests, processes, and displays real-time location updates for riders and drivers. This layer ensures smooth trip tracking and accurate live maps.

---

## 📦 Core Components

### 1. **Ingestion Gateway**
- Accepts location updates from driver apps via WebSocket, MQTT, or HTTPS
- Validates, timestamps, and normalizes incoming data
- Temporarily buffers updates if downstream services are busy

### 2. **Stream Processing Engine**
- Technologies: **Apache Kafka**, **Redis Streams**, **Apache Flink**, **Spark Streaming**
- Responsibilities:
  - Deduplicate location points
  - Smooth path using Kalman filters
  - Detect trip phase changes (pickup, en route, dropoff)
  - Join location data with trip metadata (IDs, user roles)

### 3. **Real-Time Database**
- Stores the latest location for each driver/rider
- Tech options:
  - **Redis** (fast, in-memory store)
  - **Firebase Realtime DB** or **Firestore**
  - **ScyllaDB** or **Cassandra** for scalable writes

### 4. **Location Query API**
- Allows frontend apps to:
  - Fetch live location for a given trip
  - Poll for updates or subscribe via WebSocket
  - Access trip history if authorized

---

## 🗺️ Real-Time Display Architecture

```text
[Driver App] --> [WebSocket/MQTT] --> [Ingestion Layer] --> [Kafka/Flink] --> [Redis Store] --> [Location API] --> [Rider App Map]
```

### Trip Routing and Polling Strategy

- **Trip IDs** are used to route updates to only relevant clients.
- **Fallback for polling** via REST if WebSocket disconnects.

---

## ⚙️ Performance Targets

| Metric              | Target                        |
|---------------------|-------------------------------|
| Ingestion latency   | < 200 ms                      |
| End-to-end delay    | < 500 ms (device to device)   |
| Update frequency    | 1 per 3–5 seconds (realistic) |
| Uptime SLA          | 99.99%                        |

---

## 🛡️ Security & Access Control

- All updates secured via **TLS**.
- Authenticated via **JWT tokens**.
- Riders can only access the trip they’re on.
- **Trip data expires** after TTL (e.g., 30 minutes post-trip).
- **Real-time channel tokens** rotate periodically for safety.

---

## 🧠 Design Challenges

| Challenge               | Mitigation Strategy                                    |
|------------------------|--------------------------------------------------------|
| High-frequency writes   | Use Redis with TTL and batching                       |
| WebSocket scalability   | Shard connections by user ID or geo-hash              |
| Multi-device sync       | Centralize user sessions; resolve conflicts on server |
| Partial data loss       | Buffer & retry failed updates                         |
| Geo-spatial indexing    | Use QuadTrees or RedisGeo to filter nearby drivers    |

---

## 🌍 Real-World Extensions

- **Location Heatmaps**: Store anonymized pings to visualize demand over time.
- **Route Playback**: Enable trip replays for customer support or disputes.
- **Multi-party Visibility**: Allow real-time tracking for third parties (e.g. family).
- **Region-based Sharding**: Divide processing clusters by country or zone.
- **Replay Pipelines**: Store Kafka topics for 24–48 hrs to replay missed updates.

---

## 🚗 Relevance to Bimride

| Feature / Use Case        | Backend Streaming Role                                  |
|---------------------------|---------------------------------------------------------|
| Live trip tracking        | Display accurate real-time location updates             |
| Driver ETA estimates      | Predict and show dynamic arrival time to riders         |
| Shared ride coordination  | Update all riders with live driver location             |
| Safety response tracking  | Monitor driver path in real-time for safety escalations |

---

## 📌 Deliverables for Day 3

- ✅ Designed Kafka-based location stream processing architecture
- ✅ Chose appropriate databases for high-speed writes and real-time reads
- ✅ Mapped API routes and update protocols for live display
- ✅ Outlined latency benchmarks and access control rules
- ✅ Identified geo-distributed and replay-safe extensions
