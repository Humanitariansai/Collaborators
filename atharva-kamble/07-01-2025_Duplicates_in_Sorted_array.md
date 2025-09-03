# 🧠 Remove Duplicates from Sorted Array – In-Depth Study Report

## 🚩 Problem Statement

Given an integer array `nums` **sorted in non-decreasing order**, remove the duplicates **in-place** such that each unique element appears only once. The relative order of the elements should be kept the same.

Do not allocate extra space for another array — you must modify the input array **in-place** and return the new length.

---

## ✅ Final Solution (Python)

```python
class Solution:
    def removeDuplicates(self, nums):
        if not nums:
            return 0

        i = 0  # slow pointer for unique elements

        for j in range(1, len(nums)):
            if nums[j] != nums[i]:
                i += 1
                nums[i] = nums[j]

        return i + 1
```

---

## 🧰 Data Structure

### Array with Two Pointers

- The array is modified in-place using a two-pointer technique.
- `i` tracks the last unique element’s position.
- `j` scans through the array from start to finish, comparing with `i`.

---

## ⚙️ Time and Space Complexity

| Metric | Value       |
|--------|-------------|
| Time   | O(n)        |
| Space  | O(1)        |

- **Time:** We make a single pass through the array using two pointers.
- **Space:** No extra array or data structure is used; modification is in-place.

---

## 🧼 Clean Code Practices Applied

- Clear pointer naming (`i`, `j`) based on roles.
- Guard clause (`if not nums`) handles edge cases early.
- Loop is concise and readable.
- Constant space algorithm without clutter.

---

## ⚠️ Challenges Faced and Learnings

### 1. Understanding In-Place Modification
One challenge was realizing that the goal isn’t to return a new array, but to overwrite the input array such that only the first `k` elements are unique.

### 2. Two-Pointer Mechanics
Keeping `i` fixed while `j` searches ahead helps eliminate duplicates while preserving order — a core trick for in-place algorithms.

### 3. Off-by-One Edge Cases
Properly returning `i + 1` instead of `i` avoids common off-by-one errors when counting final unique elements.

---

## 🚗 Relevance to BimRide and Ride-Hailing Applications

This problem and its solution are relevant to real-world systems like **BimRide** in the following ways:

### 1. Deduplicating Driver or Rider Lists
When syncing data from multiple sources, you might receive repeated entries (e.g., same driver showing twice). A two-pointer rewrite like this efficiently cleans the data.

### 2. Streamlining Sorted Logs or Telemetry Data
Ride-tracking systems may generate sorted but duplicate telemetry points. Efficient in-place cleanup helps reduce storage and processing costs.

### 3. Memory-Constrained Mobile Environments
For mobile apps or on-device SDKs (like driver apps), working with in-place array operations improves memory efficiency and responsiveness.

### 4. Sorting and Cleanup of Location Pings
If rider pickup or driver location pings are sorted by time or position, duplicate readings can be removed using this exact logic before map rendering.

---

## 🔚 Conclusion

The **Remove Duplicates from Sorted Array** problem illustrates a classic and powerful use of the **two-pointer** technique for in-place array updates.

It teaches:
- How to optimize for space without sacrificing clarity.
- How to iterate cleanly through sorted data.
- How to prepare systems (like BimRide) for real-world data cleansing and deduplication workflows.

It’s a foundational algorithm for any backend system dealing with **sorted input**, **data deduplication**, or **performance-sensitive environments**.
