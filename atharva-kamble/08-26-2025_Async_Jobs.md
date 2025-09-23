# Async Jobs and Queue Architecture

🎯 **Purpose:** Define the architecture and practices for BimRide's asynchronous job system including job types, idempotency, retries with backoff, dead letter handling, scheduled jobs, and exactly-once delivery goals.

---

## Why Async Jobs Matter

Ride-hailing platforms like BimRide process events that are time sensitive and high volume. Async jobs ensure heavy or background tasks do not block rider or driver interactions. Examples include:

* Payment capture after ride completion  
* Trip receipt generation and email sending  
* Driver incentive calculations  
* Location heatmap updates  

A queue system ensures durability, retries, and scale-out consumption with workers.

---

## Job Types

### 1. **Immediate Jobs**  
Triggered right after a user action (e.g., ride booking). Needs near real-time processing.

### 2. **Deferred Jobs**  
Executed after a delay (e.g., charge cancellation fee after 5 minutes if driver unconfirmed).

### 3. **Batch Jobs**  
Aggregate results over a time window (e.g., incentive payouts once a week).

### 4. **Scheduled Jobs**  
Cron-like tasks such as cleaning up expired promo codes or archiving old logs.

---

## Idempotency

Idempotency is critical to prevent duplicate effects from retries.

* **Idempotency Key**: A unique key tied to a logical operation, e.g., `ride_id + operation_type`.  
* **Deduplication Table**: Track completed jobs in Redis or database.  
* **Worker Check**: If key exists, skip re-execution.  

```python
def process_payment(ride_id, amount, idempotency_key):
    if redis.exists(idempotency_key):
        return "Already processed"
    charge_card(ride_id, amount)
    redis.set(idempotency_key, "done", ex=86400)
```

## Retry Strategy with Backoff

Retries must avoid overloading downstream services.

* **Exponential Backoff with Jitter**: Spread out retry spikes.
* **Retry Count Limit**: Prevent infinite loops.
* **Context Aware Retries**: Payment retries may differ from email retries.

```yaml
retry_policy:
  max_retries: 5
  backoff_strategy: exponential_jitter
  initial_delay: 2s
  max_delay: 5m
```

## Dead Letter Handling

Jobs that fail permanently move to a Dead Letter Queue (DLQ).

* Tagged with failure reason and metadata.
* Reviewed manually or with automated scripts.
* DLQ metrics are critical health signals.

```sql
SELECT job_id, error_message, failed_at 
FROM dead_letter_jobs 
WHERE created_at > NOW() - INTERVAL '24 HOURS';
```

## Scheduled Jobs

Use distributed cron (e.g., Quartz, Celery Beat, or Kubernetes CronJobs).

* Ensure leader election or coordination to avoid double execution.
* Log execution history for audits.

**Example:**
* Promo expiry cleanup every midnight
* Driver ranking refresh every hour

## Exactly-Once Delivery Goals

True exactly-once is difficult in distributed systems. BimRide targets effectively-once delivery via:

* Idempotency keys
* Atomic commits with outbox pattern
* Deduplication in workers
* Auditable state transitions

## Queue and Worker Design

### Core Components

* **Producer**: API or service creating the job event.
* **Broker**: Kafka, RabbitMQ, or Redis Streams to persist jobs.
* **Worker Pool**: Consumers executing jobs in parallel.
* **Monitoring**: Metrics for lag, retries, DLQs.

### Scaling

* Horizontal scaling of workers by job type.
* Separate critical vs. non-critical queues.
* Priority queues for rider-driver matching vs. background emails.

### Observability

* **Metrics**: Queue depth, processing latency, retry counts.
* **Tracing**: Job ID traced across producer, broker, and worker.
* **Alerts**: DLQ growth > threshold, lag time above SLA.

## Business Impact

* Reliable execution of payments, refunds, and trip updates
* Improved rider-driver experience due to non-blocking workflows
* Operational confidence with audit trails and dead letter visibility
* Cost efficiency by isolating background processing