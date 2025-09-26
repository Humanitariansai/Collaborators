# Using Blockchain for Ride Payment Transparency

**Date:** 08-27-2025  
**Author:** Shaun Noronha

---

## 🚀 Introduction

Transparent payments reduce disputes and improve trust with regulators. We record ride hashes on-chain and store full details off-chain for privacy and scalability.

---

## ⚙️ Architecture Overview


```
[Ride Service] -> [Payment Service] -> [Hasher] -> [On-chain Tx Hash]
                                   \-> [Encrypted Off-chain Ledger]
Regulator UI -> verifies hash matches receipt; PII never touches chain.
```
Design choices:
- Sidechain with low fees; periodic checkpoints to mainnet.
- Hash includes fare, timestamps, vehicle id; no PII.


---

## 🧠 Algorithms Used

```python
import hashlib, json

def ride_hash(receipt: dict, salt="bimride"):
    # Keep PII out: only hashed metadata
    payload = {k: receipt[k] for k in ["fare","start_ts","end_ts","vehicle_id"]}
    blob = json.dumps(payload, sort_keys=True).encode()
    return hashlib.sha256((salt.encode()+blob)).hexdigest()

print(ride_hash({"fare":18.5,"start_ts":1693170000,"end_ts":1693171800,"vehicle_id":"BB-123"}))
```

---

## 🔁 MLOps Workflow Example

```yaml
name: solidity-ci
on:
  push:
    paths:
      - 'contracts/**'
jobs:
  build-test-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: 20
      - name: Install deps
        run: npm ci --prefix contracts
      - name: Compile + Test
        run: npm test --prefix contracts
      - name: Deploy to testnet
        run: npm run deploy:testnet --prefix contracts
```

---

## 🔍 Real-World Scenario

In **Harrison’s Cave**, a rider questions a fare. Support locates the ride receipt, verifies the on-chain hash, and the case closes without manual data digging.

---

## 📊 Tools and Technologies


| Component                | Tool/Tech                          |
|--------------------------|------------------------------------|
| Smart Contracts          | Solidity + Hardhat                 |
| Off-chain Storage        | Postgres (encrypted columns)       |
| Hashing                  | SHA-256 with salt                  |
| Explorer                 | Blockscout                         |
| CI/CD                    | Node + Hardhat tests               |


---

## ✅ Conclusion

This work on **Using Blockchain for Ride Payment Transparency** is tailored to Bimride’s Barbados context and serves as a concrete, auditable progress artifact.
