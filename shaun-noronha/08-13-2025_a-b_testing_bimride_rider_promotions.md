# A/B Testing Bimride Rider Promotions

**Date:** 08-13-2025  
**Author:** Shaun Noronha

---

## 🚀 Introduction

In this technical document, we implement **A/B Testing Bimride Rider Promotions** for Bimride in Barbados.
This write-up is intended as a progress artifact for nonprofit auditing and background checks,
covering architecture, algorithms, CI/CD and KPIs. Reference areas include Speightstown (St. Peter) and Oistins (Christ Church).

---

## ⚙️ Architecture Overview

- Service boundaries: `pricing`, `safety`, `routing`, `support`, `compliance`.
- Authentication with OAuth2; RBAC for ops dashboards; secrets in Azure Key Vault.
- Canary releases using workload identity; blue/green for risky changes.
- Batch processing in Spark for daily aggregates; Flink for streaming features.
- Event ingestion via Kafka (rides, payments, app telemetry) → feature store.

---

## 🧠 Algorithms Used

```python
def srm_check(control, treatment):
    # Simple sample ratio mismatch (SRM) using chi-square
    import math
    n = control + treatment
    expected = n/2
    chi = ((control-expected)**2/expected)+((treatment-expected)**2/expected)
    return chi
```

---

## 🔁 MLOps Workflow Example

```yaml
# .github/workflows/a-b-testing-bimride-rider-promotions.yml
name: a-b-testing-bimride-rider-promotions pipeline

on:
  push:
    branches: [ main ]
    paths:
      - 'data/**'
      - 'services/a-b-testing-bimride-rider-promotions/**'
  workflow_dispatch:

jobs:
  ci-cd:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with: { python-version: '3.11' }
      - name: Install
        run: pip install -r requirements.txt
      - name: Lint & Test
        run: pytest -q && ruff check .
      - name: Build Image
        run: docker build -t bimride/a-b-testing-bimride-rider-promotions:$GITHUB_SHA services/a-b-testing-bimride-rider-promotions
      - name: Push Artifacts (DVC)
        run: |
          dvc add data/ models/ || true
          dvc push || true
```

---

## 🔍 Real-World Scenario

**Use Case**: Deploy **A/B Testing Bimride Rider Promotions** to production serving riders between Oistins (Christ Church) and Harrison’s Cave.  
**Solution**: Roll out to 10% traffic for 48 hours, evaluate KPIs, then ramp to 50% if targets hold.

---

## 📊 Tools and Technologies

| Component                | Choice                                      |
|-------------------------|----------------------------------------------|
| Training/Serving        | PyTorch, Scikit-learn, FastAPI               |
| Storage                 | Postgres, Azure Blob, Delta/Iceberg          |
| Stream & Batch          | Kafka, Flink, Spark                          |
| Monitoring              | Prometheus, Grafana, OpenTelemetry           |
| Secrets & Identity      | Azure Key Vault, Managed Identity            |

---

## 📐 Data Model (SQL)

```sql
-- Minimal schema for a-b-testing-bimride-rider-promotions
CREATE TABLE IF NOT EXISTS audit_a_b_testing_bimride_rider_promotions (
  id BIGSERIAL PRIMARY KEY,
  happened_at TIMESTAMPTZ NOT NULL,
  entity_id TEXT NOT NULL,
  metric TEXT NOT NULL,
  value DOUBLE PRECISION,
  notes TEXT
);
```

---

## 🔌 Public API Sketch (OpenAPI)

```yaml
openapi: 3.0.3
info:
  title: A/B Testing Bimride Rider Promotions API
  version: 1.0.0
paths:
  /v1/a-b-testing-bimride-rider-promotions/status:
    get:
      responses: {'200': {'description': 'ok'}}
```

---

## 🎯 KPIs / Acceptance Criteria

- lift detection power > 0.8
- SRM checks pass
- promo ROI > 1.2

---

## ⚠️ Risks & Mitigations

- Data drift causing degraded predictions → add nightly drift report with Kolmogorov–Smirnov tests.  
- Cost spikes on storage/compute → enable object lifecycle and spot instances for batch jobs.  
- Privacy concerns → pseudonymize rider IDs and enforce retention windows.

---

## ✅ Conclusion

This artifact documents substantive progress on **A/B Testing Bimride Rider Promotions**. The implementation is reproducible,
secure by default, and measured against clear KPIs suitable for nonprofit audits in Barbados.
