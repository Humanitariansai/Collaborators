# Voice-Enabled Booking for Bimride Riders

**Date:** 08-26-2025  
**Author:** Shaun Noronha

---

## 🚀 Introduction

Hands-free booking improves accessibility for seniors and helps tourists who are unfamiliar with the app. We combine VAD, ASR, and intent parsing to create reliable **voice-enabled booking**.

---

## ⚙️ Architecture Overview


```
[Microphone] -> [VAD] -> [ASR] -> [Intent Parser] -> [Booking API]
                      ^                          \-> [Disambiguation prompts]
               [Noise Suppression]
```
Highlights:
- Offline fallback ASR keeps basic functionality during network outages.
- Domain-specific grammar reduces ambiguity for places like Oistins and Bathsheba.


---

## 🧠 Algorithms Used

```python
# Simple voice intent extraction (toy example)
def parse_intent(text):
    text = text.lower()
    if "book" in text and "to" in text:
        # naive parse: everything after 'to' is destination
        dest = text.split("to",1)[1].strip()
        return {"intent":"book_ride","destination":dest}
    return {"intent":"unknown"}

print(parse_intent("Please book a ride to Oistins Fish Fry"))
```

---

## 🔁 MLOps Workflow Example

```yaml
name: voice-booking-ci
on:
  push:
    paths:
      - 'voice/**'
      - 'nlu/**'
jobs:
  tests-and-export:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Install
        run: pip install -r voice/requirements.txt
      - name: Unit tests (NLU + VAD)
        run: pytest -q
      - name: Evaluate ASR accuracy (WER)
        run: python voice/eval_asr.py --dataset data/barbados_accent.json
      - name: Export intents model
        run: python nlu/export.py --format onnx
```

---

## 🔍 Real-World Scenario

A rider in **Grantley Adams International Airport (BGI)** says, “Book a ride to Miami Beach at 7 pm.” The system confirms the pickup time and destination via voice and posts the booking.

---

## 📊 Tools and Technologies


| Component                | Tool/Tech                         |
|--------------------------|-----------------------------------|
| ASR                      | Vosk / Wav2Vec2                   |
| NLU                      | spaCy / fastText / Transformers   |
| VAD & Noise Suppression  | WebRTC VAD, RNNoise               |
| Serving                  | FastAPI + WebSocket               |
| Testing                  | PyTest + audio fixtures           |


---

## ✅ Conclusion

This work on **Voice-Enabled Booking for Bimride Riders** is tailored to Bimride’s Barbados context and serves as a concrete, auditable progress artifact.
