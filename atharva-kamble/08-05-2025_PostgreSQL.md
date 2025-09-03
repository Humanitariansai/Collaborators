# 🚖 Day 2 — PostgreSQL Schema & Query Optimization for Ride-Hailing APIs

## 🎯 Goal
Design a normalized and indexed PostgreSQL schema for the ride-hailing backend, optimized for:
- **Spatial queries** (finding nearby drivers)
- **Trip lifecycle updates**
- **High-volume inserts** from trip events
- **Low-latency reads** for live tracking and history

---

## 🗃️ Core Database Schemas

### 1. `users` Table
Stores both riders and drivers (role-based field for separation).

```sql
CREATE TABLE users (
    user_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    full_name TEXT NOT NULL,
    email TEXT UNIQUE NOT NULL,
    phone TEXT UNIQUE NOT NULL,
    role TEXT CHECK (role IN ('rider', 'driver')),
    rating NUMERIC(2,1) DEFAULT 5.0,
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);
CREATE INDEX idx_users_role ON users(role);
```

## 2. `driver_locations` Table

Holds driver’s last known location (updated every 3–5 seconds in active trips).

```sql
CREATE TABLE driver_locations (
    driver_id UUID PRIMARY KEY REFERENCES users(user_id),
    location GEOGRAPHY(Point, 4326) NOT NULL,
    last_updated TIMESTAMP DEFAULT NOW()
);
CREATE INDEX idx_driver_locations_geo ON driver_locations USING GIST(location);
```

## 3. `trips` Table

Main record for trip lifecycle.

```sql
CREATE TABLE trips (
    trip_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    rider_id UUID REFERENCES users(user_id),
    driver_id UUID REFERENCES users(user_id),
    status TEXT CHECK (status IN ('requested','driver_pending','accepted','at_pickup','en_route','completed','canceled')),
    pickup_loc GEOGRAPHY(Point, 4326),
    dropoff_loc GEOGRAPHY(Point, 4326),
    estimated_fare NUMERIC(10,2),
    final_fare NUMERIC(10,2),
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);
CREATE INDEX idx_trips_status ON trips(status);
CREATE INDEX idx_trips_rider_id ON trips(rider_id);
CREATE INDEX idx_trips_driver_id ON trips(driver_id);
```

## 4. `trip_events` Table

```sql
CREATE TABLE trip_events (
    event_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    trip_id UUID REFERENCES trips(trip_id),
    event_type TEXT,
    event_payload JSONB,
    created_at TIMESTAMP DEFAULT NOW()
);
CREATE INDEX idx_trip_events_trip_id_created_at ON trip_events(trip_id, created_at DESC);
```

## Spatial Query Example

```sql
SELECT driver_id, ST_Distance(location, ST_SetSRID(ST_MakePoint($1, $2), 4326)) AS distance
FROM driver_locations
WHERE ST_DWithin(location, ST_SetSRID(ST_MakePoint($1, $2), 4326), 3000)
ORDER BY distance ASC
LIMIT 10;
```

## 📌 Indexes Used
- **GIST** on `driver_locations.location` for fast geo lookups.

---

## ⚡ Query Optimization Tactics

| Area           | Strategy |
|----------------|----------|
| Trip lookups   | Composite indexes on `(status, created_at)` and `(rider_id, created_at)` |
| Event writes   | Use `UNLOGGED` tables for temp events if persistence not critical |
| Driver matching| PostGIS + `LIMIT` to avoid scanning all drivers |
| Hot reads      | Cache active trips in Redis (TTL: 10–15 s) |
| Bulk inserts   | Use `COPY` or batch inserts for historical loads |

---

## 🔒 Data Integrity & Safety
- Foreign keys for **trip ↔ user** consistency  
- **ENUM/Check** constraints to prevent illegal states  
- Periodic archival of completed trips into `trips_archive` for smaller active dataset  

---

## 📌 Deliverables for Day 2
✅ Core schema for `users`, `driver_locations`, `trips`, and `trip_events`  
✅ Spatial indexes for geo queries  
✅ Composite indexes for common filters  
✅ Example driver proximity query  
✅ Performance tactics documented  
