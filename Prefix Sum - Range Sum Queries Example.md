# Prefix Sum - Range Sum Queries Example

Demonstrates the core use case from [[Prefix Sum - Overview]]: answering many "sum of subarray" queries efficiently.

## Problem
Given `nums`, an array `queries` where `queries[i] = [x, y]`, and an integer `limit`, return a boolean array — `true` for each query if the sum of the subarray from `x` to `y` is less than `limit`, else `false`.

Example: `nums = [1, 6, 3, 2, 7, 2]`, `queries = [[0,3], [2,5], [2,4]]`, `limit = 13`
Subarray sums: `[12, 14, 12]` → answer: `[true, false, true]`

## Approach
1. Build the prefix sum array once — O(n)
2. For each query `[x, y]`, compute the subarray sum in O(1) using `prefix[y] - prefix[x - 1]`
3. Compare against `limit` to answer that query

## Complexity comparison
- **Without prefix sum:** each query costs O(n) in the worst case → with `m = queries.length`, total is **O(n·m)**
- **With prefix sum:** O(n) to build + O(1) per query → total is **O(n + m)**

This is a substantial improvement whenever there are many queries. Space cost: O(n) to store the prefix sum array.

#dsa #algorithms #prefix-sum #arrays

Related: [[Prefix Sum - Overview]], [[Prefix Sum - Space Optimization]]
