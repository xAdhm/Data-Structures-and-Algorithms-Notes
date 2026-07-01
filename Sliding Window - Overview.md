# Sliding Window - Overview

Sliding window is another common technique for array/string problems — like [[Two Pointers - Overview]], it works identically for arrays and strings (both just need to be iterables). In fact, a sliding window is implemented *using* two pointers.

## Subarrays (aka "windows")
A **subarray** is a contiguous section of an array — elements must be adjacent and in original order. For `[1, 2, 3, 4]`:
- Length 1: `[1]`, `[2]`, `[3]`, `[4]`
- Length 2: `[1,2]`, `[2,3]`, `[3,4]`
- Length 3: `[1,2,3]`, `[2,3,4]`
- Length 4: `[1,2,3,4]`

A subarray is defined by two indices: the **left bound** (start) and **right bound** (end). In sliding window context, a subarray is also called a **window**.

For strings, the equivalent term is **substring**.

## "Valid" subarrays
Many array problems revolve around finding "valid" subarrays. Validity is defined by two parts:
1. **Constraint metric** — an attribute of the subarray (e.g. sum, number of unique elements, frequency of a specific element)
2. **Numeric restriction** on that metric (e.g. "sum ≤ 10")

A subarray is valid if its constraint metric satisfies the restriction.

## The core idea
Maintain two variables, `left` and `right`, marking the window's bounds. Start with `left = right = 0` (window = just the first element).
- **Expand** the window by incrementing `right` ("adding" a new element)
- If adding an element makes the window invalid, **shrink** it by incrementing `left` ("removing" the left-most element) until valid again
- The window's size fluctuates, but it always slides rightward overall until it reaches the end of the input

### Worked walkthrough
`nums = [3, 2, 1, 3, 1, 1]`, find the longest subarray with sum ≤ 5.
- Start: window = `[3]`
- Expand to `[3, 2, 1]` → sum = 6 > 5 → invalid
- Shrink from the left → `[2, 1]` → sum = 3 → valid again

**Why it's safe to permanently discard the removed `3`:** since all elements are positive, sum only grows as the window grows. `[3, 2, 1]` was already too big, and any window that still includes that `3` must also include everything between it and the current right bound (by the definition of a contiguous subarray) — so it can never shrink back to validity while keeping the `3`. It can be safely forgotten for the rest of the algorithm.

## When to think "sliding window"
Whenever a problem talks about "valid" subarrays **and** asks you to find them — think sliding window. Common variants:
- Find the *best* valid subarray (e.g. longest) — see [[Sliding Window - Dynamic Window Size]]
- Find the *number* of valid subarrays — see [[Sliding Window - Counting Valid Subarrays]]
- Fixed-length window problems — see [[Sliding Window - Fixed Window Size]]

#dsa #algorithms #sliding-window #arrays #strings

Related: [[Two Pointers - Overview]], [[Sliding Window - Dynamic Window Size]], [[Sliding Window - Counting Valid Subarrays]], [[Sliding Window - Fixed Window Size]], [[Sliding Window - Why It's Efficient]]
