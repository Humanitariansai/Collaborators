## A/B Testing and Statistical Hypothesis Testing in Ride-Hailing

---

## 1. Introduction

In this article, we explore **A/B Testing**, a statistical methodology widely used to compare two or more strategies or configurations. It is especially effective in **pricing**, **user interface**, and **driver incentives** within BimRide.

---

## 2. Problem Statement

How can BimRide determine whether a new dynamic pricing model or incentive scheme results in better performance compared to the current model?

A/B testing helps validate decisions by splitting users/drivers into two groups:
- **Group A**: Control (existing system)
- **Group B**: Test (new strategy)

Performance is measured using KPIs like:
- Ride completion rate
- Driver retention
- Average revenue per ride

---

## 3. A/B Testing Methodology

### 3.1 Design

- **Randomization**: Split sample into two statistically equivalent groups
- **Metric Selection**: Identify key success indicators (KPIs)
- **Duration**: Ensure a long-enough test to reduce noise
- **Confidence**: Typically aim for a 95% confidence level

### 3.2 Statistical Hypothesis Testing

- **Null Hypothesis (H₀)**: No difference between groups
- **Alternative Hypothesis (H₁)**: Test group performs better

Use **t-tests** or **z-tests** for comparison depending on sample size and variance.

---

## 4. Challenges Faced

### 4.1 Sample Bias
- **Problem**: Biased allocation skews results.
- **Solution**: Use stratified randomization across regions, time-of-day, and user types.

### 4.2 Insufficient Sample Size
- **Problem**: Small sample leads to underpowered tests.
- **Solution**: Conduct **power analysis** to estimate minimum size.

### 4.3 Interference Between Groups
- **Problem**: Drivers might operate in both A and B zones.
- **Solution**: Use geo-fencing or user tagging to avoid contamination.

---

## 5. Implementation in Python

### 5.1 Sample Code

```python
import pandas as pd
from scipy import stats

# Load sample A/B test results
data = pd.read_csv("ab_test_rides.csv")
group_a = data[data['group'] == 'A']['revenue']
group_b = data[data['group'] == 'B']['revenue']

# Perform t-test
t_stat, p_value = stats.ttest_ind(group_a, group_b, equal_var=False)

print(f"T-statistic: {t_stat:.4f}")
print(f"P-value: {p_value:.4f}")

if p_value < 0.05:
    print("Result is statistically significant. Accept H₁.")
else:
    print("No significant difference. Fail to reject H₀.")
```