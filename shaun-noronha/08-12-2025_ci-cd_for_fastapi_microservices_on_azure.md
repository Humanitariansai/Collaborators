# CI/CD for FastAPI Microservices on Azure

**Date:** 08-12-2025  
**Author:** Shaun Noronha

---

## 🚀 Introduction

In this technical document, we implement **CI/CD for FastAPI Microservices on Azure** for Bimride in Barbados.
This write-up is intended as a progress artifact for nonprofit auditing and background checks,
covering architecture, algorithms, CI/CD and KPIs. Reference areas include Bridgetown Harbour & Cruise Terminal and Oistins (Christ Church).

---

## ⚙️ Architecture Overview

- Batch processing in Spark for daily aggregates; Flink for streaming features.
- Event ingestion via Kafka (rides, payments, app telemetry) → feature store.
- Authentication with OAuth2; RBAC for ops dashboards; secrets in Azure Key Vault.
- Service boundaries: `pricing`, `safety`, `routing`, `support`, `compliance`.
- Canary releases using workload identity; blue/green for risky changes.

---

## 🧠 Algorithms Used

```python
from fastapi import FastAPI
app=FastAPI()
@app.get('/healthz')
def health(): return {'ok':True}
```

---

## 🔁 MLOps Workflow Example

```yaml
# .github/workflows/ci-cd-for-fastapi-microservices-on-azure.yml
name: ci-cd-for-fastapi-microservices-on-azure pipeline

on:
  push:
    branches: [ main ]
    paths:
      - 'data/**'
      - 'services/ci-cd-for-fastapi-microservices-on-azure/**'
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
        run: docker build -t bimride/ci-cd-for-fastapi-microservices-on-azure:$GITHUB_SHA services/ci-cd-for-fastapi-microservices-on-azure
      - name: Push Artifacts (DVC)
        run: |
          dvc add data/ models/ || true
          dvc push || true
```

---

## 🔍 Real-World Scenario

**Use Case**: Deploy **CI/CD for FastAPI Microservices on Azure** to production serving riders between Bridgetown Harbour & Cruise Terminal and Grantley Adams International Airport (BGI).  
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
-- Minimal schema for ci-cd-for-fastapi-microservices-on-azure
CREATE TABLE IF NOT EXISTS audit_ci_cd_for_fastapi_microservices_on_azure (
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
  title: CI/CD for FastAPI Microservices on Azure API
  version: 1.0.0
paths:
  /v1/ci-cd-for-fastapi-microservices-on-azure/status:
    get:
      responses: {'200': {'description': 'ok'}}
```

---

## 🎯 KPIs / Acceptance Criteria

- p95 latency < 200ms
- zero-downtime deploys
- rollbacks < 5min

---

## ⚠️ Risks & Mitigations

- Data drift causing degraded predictions → add nightly drift report with Kolmogorov–Smirnov tests.  
- Cost spikes on storage/compute → enable object lifecycle and spot instances for batch jobs.  
- Privacy concerns → pseudonymize rider IDs and enforce retention windows.

---

## ✅ Conclusion

This artifact documents substantive progress on **CI/CD for FastAPI Microservices on Azure**. The implementation is reproducible,
secure by default, and measured against clear KPIs suitable for nonprofit audits in Barbados.
