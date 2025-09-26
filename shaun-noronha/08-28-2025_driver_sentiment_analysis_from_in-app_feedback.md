# Driver Sentiment Analysis from In-App Feedback

**Date:** 08-28-2025  
**Author:** Shaun Noronha

---

## 🚀 Introduction

Understanding driver sentiment helps Bimride improve policies and reduce churn. We build a labeled corpus from in‑app feedback and fine‑tune a small transformer.

---

## ⚙️ Architecture Overview


```
[Feedback Text] -> [PII Scrubber] -> [Labeling (Human + Rules)] -> [Finetune DistilBERT]
                                                         \----> [Lexicon baseline]
Serving: REST API returns sentiment + key phrases; dashboard tracks trends by parish.
```
Considerations:
- Opt-in for feedback usage.
- Anonymize and aggregate before analytics.


---

## 🧠 Algorithms Used

```python
# Pseudo inference using a transformer-like output
import numpy as np

def softmax(x):
    e = np.exp(x - np.max(x)); return e/e.sum()

logits = np.array([1.2, -0.3, 0.1])  # [positive, negative, neutral]
probs = softmax(logits)
label = ["positive","negative","neutral"][int(np.argmax(probs))]
print({"label": label, "probs": probs.round(3).tolist()})
```

---

## 🔁 MLOps Workflow Example

```yaml
name: sentiment-train
on:
  schedule:
    - cron: "30 1 * * *"   # daily
jobs:
  train-eval-promote:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Install
        run: pip install -r nlp/requirements.txt
      - name: Train
        run: python nlp/train_sentiment.py --model distilbert-base-uncased --epochs 3
      - name: Evaluate
        run: python nlp/eval.py --f1-threshold 0.82
      - name: Package & push
        run: python nlp/package.py && dvc add models/ && dvc push
```

---

## 🔍 Real-World Scenario

Drivers around **Grantley Adams International Airport (BGI)** report long pickup waits during rain. The dashboard lights up with negative scores, prompting temporary incentives for drivers to reposition.

---

## 📊 Tools and Technologies


| Component                | Tool/Tech                          |
|--------------------------|------------------------------------|
| NLP                      | DistilBERT / spaCy                 |
| Labeling                 | Prodigy + rule-based seed labels   |
| Serving                  | FastAPI + ONNX Runtime             |
| Storage                  | Delta Lake                         |
| Dashboards               | Grafana + Grafana Alerting         |


---

## ✅ Conclusion

This work on **Driver Sentiment Analysis from In-App Feedback** is tailored to Bimride’s Barbados context and serves as a concrete, auditable progress artifact.
