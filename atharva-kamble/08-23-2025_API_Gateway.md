# API Gateway Rate Limiting And Throttling

**Owner:** Platform Engineering  
**Purpose:** Protect BimRide services from overload and abuse while keeping honest traffic fast and predictable.

## Core ideas
* Rate limit controls how many requests a subject can make in a time window  
* Throttling shapes bursty traffic into a smooth flow  
* Subjects can be user, device, driver, api key, city, or ip  
* Policies live in config and can be changed without a deploy

## Minimal architecture

### Control plane
* Policy store with versioned limits and quotas  
* Admin view for edits, approvals, and audit

### Data plane
* API gateway sidecar on every edge node  
* Redis or Dynamo style store for counters and tokens  
* Metrics pipeline for near real time visibility

### Consistency
* Use eventual consistency for counters with small drift tolerance  
* Use sticky hashing for subjects so most requests hit the same shard

## Policy model

```json
{
  "policy_key": "rider_public_api",
  "subjects": ["rider_id", "ip"],
  "limits": [
    { "name": "per_minute", "window_seconds": 60, "allow": 120 },
    { "name": "per_second_burst", "window_seconds": 1, "allow": 10 }
  ],
  "penalty": { "cooldown_seconds": 30 }
}
```

### City override example

```json
{
  "policy_key": "rider_public_api_bb_bgi",
  "inherits": "rider_public_api",
  "limits": [
    { "name": "per_minute", "window_seconds": 60, "allow": 90 }
  ]
}
```

## Algorithms

### Fixed window
Simple counter per window. Easy and fast. Can allow spikes at the boundary.

### Sliding window
Counts recent requests over a moving window. Better fairness. Slightly higher cost.

### Token bucket
Bucket fills at a set rate up to a max. Each request consumes one token. Allows short bursts while keeping a steady average.

Rate R tokens per second with bucket size B

```
Tokens at time t equals min(B, tokens_at_t0 + R × delta_t)
Allow if tokens greater than or equal to one else reject
```

## Token bucket with Redis

### Keys
```
tb:{policy}:{subject}:tokens
tb:{policy}:{subject}:ts
```

### Lua atomics

```lua
local key_tokens = KEYS[1]
local key_ts = KEYS[2]
local now = tonumber(ARGV[1])
local rate = tonumber(ARGV[2])
local burst = tonumber(ARGV[3])

local tokens = tonumber(redis.call("GET", key_tokens) or burst)
local ts = tonumber(redis.call("GET", key_ts) or now)
local delta = math.max(0, now - ts)
local refill = delta * rate
tokens = math.min(burst, tokens + refill)

local allowed = 0
if tokens >= 1 then
  tokens = tokens - 1
  allowed = 1
end

redis.call("SET", key_tokens, tokens)
redis.call("SET", key_ts, now)
return {allowed, tokens}
```

### Gateway call in Python

```python
def allow(subject, policy, now, rate, burst, r):
    res = r.eval(lua_token_bucket, 2,
                 f"tb:{policy}:{subject}:tokens",
                 f"tb:{policy}:{subject}:ts",
                 now, rate, burst)
    allowed, tokens = int(res[0]), float(res[1])
    return allowed == 1, tokens
```

## Enforcement flow

1. Normalize request identity into a subject tuple such as rider id plus ip
2. Select policy using route tag and city
3. Evaluate fast path in memory cache for very hot subjects
4. Fallback to Redis script for atomic update
5. If allowed then forward to upstream
6. If not allowed then return 429 with Retry After

### Standard 429 body

```json
{ "error": "rate_limited", "retry_after_seconds": 30 }
```

## Quotas and fairness
* Per user quotas to protect riders
* Per driver quotas to protect drivers
* Per ip quotas to slow scrapers
* Per city overrides for special events
* Soft limit with warning header before a hard block

### Response headers

```yaml
X-RateLimit-Limit: 120
X-RateLimit-Remaining: 23
X-RateLimit-Reset: 39
```

## Abuse controls
* Shadow mode to observe hit rates before turning on blocks
* Block lists for known bad keys and ips
* Anomaly alerts when a subject hits many routes at once
* Slow path captcha for public endpoints when abuse spikes

## Observability

### Metrics per policy and per city
* Allow rate and block rate
* P99 latency at the gateway
* Redis call time and error rate
* Keyspace size and eviction rate

### Logs
* Sampled allow and block events with subject hash and route tag

### Alerts
* Block rate jump above a set band
* Redis latency above budget
* Memory pressure on edge nodes

## Failure modes and safe defaults
* **Store outage** → allow with a tiny local bucket for a short window
* **Policy store outage** → freeze to last good config
* **Hotkey subject** → protect with local LRU to avoid store meltdown

## Testing and rollout
* Unit tests for edge cases like window boundary and burst refill
* Load test with recorded traffic shape
* Shadow mode with metrics only
* Ramp by city and route set
* Post ramp review of false positive rate and customer impact

## Simple checklist
1. Define policy and subject
2. Add headers for visibility
3. Set alerts
4. Shadow for a day
5. Ramp to five then twenty then fifty then full
6. Review and adjust limits0