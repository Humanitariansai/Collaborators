# 🧠 Roman to Integer – In-Depth Study Report

## 🚩 Problem Statement

Given a Roman numeral string `s`, convert it to its corresponding integer. Roman numerals follow specific rules, including subtractive combinations (e.g., `IV` = 4, `IX` = 9).

---

## ✅ Final Solution (Python)

```python
class Solution:
    def romanToInt(self, s: str) -> int:
        roman = {
            'I': 1, 'V': 5, 'X': 10, 'L': 50,
            'C': 100, 'D': 500, 'M': 1000
        }

        total = 0
        prev = 0

        for char in reversed(s):
            value = roman[char]
            if value < prev:
                total -= value
            else:
                total += value
                prev = value

        return total
```

---

## 🧰 Data Structure

### Dictionary (Hash Map)

- Used to map Roman characters to their integer values.
- Enables **O(1)** lookup for each character.

---

## ⚙️ Time and Space Complexity

| Metric | Value       |
|--------|-------------|
| Time   | O(n)        |
| Space  | O(1)        |

- **Time**: One pass through the string of length `n`.
- **Space**: Fixed size dictionary and variables, independent of input size.

---

## 🧼 Clean Code Practices Applied

- **Descriptive variable names**: `roman`, `value`, `prev`, `total`
- **Efficient iteration**: Reverse traversal avoids lookahead logic
- **Early conditional branching**: Simplifies the subtractive rule logic
- **No redundant loops or data structures**

---

## ⚠️ Challenges Faced and Learnings

### 1. Handling Subtractive Notation
Pairs like `IV`, `IX`, `XL`, etc. require subtracting smaller values before larger ones. By reversing the string and tracking the previous numeral, this logic becomes intuitive.

### 2. Avoiding String Mutation or Conversion
Instead of converting strings to lists or performing string slicing, simple character access and arithmetic improve performance and clarity.

### 3. Clean Reversal Logic
Reversing the string allows the code to detect "look-back" conditions instead of complex lookahead, simplifying edge case handling.

### 4. Preventing Incorrect Subtractions
Using `if value < prev` avoids mistakes when Roman numerals are incorrectly formatted or when processing the first character.

---

## 🚗 Relevance to BimRide and Ride-Hailing Applications

While Roman numerals themselves aren't common in ride-hailing, this algorithm teaches powerful **pattern-to-value conversion** logic that can apply in real-world scenarios like:

### 1. Promo Code Parsing
BimRide may support legacy or styled coupon codes (e.g., "XIV20") that mix Roman and Arabic numerals for branding. This algorithm can help convert them to usable numeric values during validation.

### 2. Pricing Tier Parsing
If pricing tiers or vehicle categories are represented by encoded strings, a similar approach can be used to decode, validate, and compare values.

### 3. Low-Resource Token Decoding
On embedded or offline systems with size constraints, encoding numbers in compact symbolic forms (like Roman-style) could be useful. Efficient parsing logic ensures real-time decoding.

### 4. Time Code Interpretation
In reporting or audit logs, non-standard time or shift notations could be mapped back to integers for further computation using similar mappings.

---

## 🔚 Conclusion

The **Roman to Integer** problem showcases how to efficiently parse symbolic data using dictionary mapping, reverse traversal, and conditional arithmetic. It reinforces fundamental parsing strategies and clean, efficient logic.

In systems like **BimRide**, this approach finds relevance in data decoding, promo logic, token interpretation, and user-friendly feature design.

The clean, one-pass solution demonstrates both **algorithmic clarity** and **real-world readiness**.

