# Prefix Sum - Overview

A **prefix sum** is a technique for arrays (usually of numbers). Build an array `prefix` where `prefix[i]` = the sum of all elements from index 0 up to and including index `i`.

Example: `nums = [5, 2, 1, 6, 3, 8]` → `prefix = [5, 7, 8, 14, 17, 25]`

A subarray that starts at index 0 is called a **prefix** of the array — hence "prefix sum" represents the sum of each such prefix.

## Building it
```
Given an array nums,

prefix = [nums[0]]
for (int i = 1; i < nums.length; i++)
    prefix.append(nums[i] + prefix[prefix.length - 1])
```
Start with just the first element. Each subsequent entry = current element + the last value already in `prefix` (which represents the sum of everything before the current index). Cost: **O(n)** to build.

## Why it's useful: O(1) subarray sum queries
Once built, the sum of any subarray from index `i` to `j` (inclusive) can be found in **O(1)**:

`sum(i, j) = prefix[j] - prefix[i - 1]`

(or `prefix[j] - prefix[i] + nums[i]` if you want to avoid handling the out-of-bounds case when `i = 0`)

**Why this works:** `prefix[i - 1]` is the sum of everything *before* index `i`. Subtracting that from `prefix[j]` (sum of everything up to and including `j`) leaves exactly the sum of elements from `i` to `j`.

Visually: take the sum of everything up to the end of your target subarray, then subtract the sum of everything before it — what's left is the subarray itself.

## The trade-off
- Building the prefix sum: O(n) time, O(n) space (one-time cost)
- Every future subarray sum query: O(1)

This is a form of **pre-processing** — investing some upfront time/space to store pre-computed data, which then saves much more time during the main algorithm. Whenever a problem repeatedly needs subarray sums, prefix sum usually improves the time complexity by a factor of O(n).

#dsa #algorithms #prefix-sum #arrays

Related: [[Prefix Sum - Range Sum Queries Example]], [[Prefix Sum - Space Optimization]]
