# Hashing - Subarray Sum Equals K (Exact Constraint Pattern)

A pattern for counting subarrays that satisfy an **exact** constraint (e.g. "sum equals exactly k") — as opposed to the sliding-window-friendly constraints from [[Sliding Window - Overview]] (e.g. "sum ≤ k"), which rely on the property that if window `(left, right)` is valid, then every window `(i, right)` for `left < i ≤ right` is also valid. That property **doesn't hold** for exact-value constraints — an array could have negative numbers, so shrinking a window doesn't monotonically move you toward or away from validity the way it does for `≤ k` with all-positive inputs. This is why sliding window doesn't directly apply here — instead this pattern combines [[Prefix Sum - Overview|prefix sums]] with a hash map.

## The core idea
The sum of any subarray = the difference between two prefix sums. If a subarray from `j` to `i` has sum `k`:

`prefix(i) - prefix(j - 1) = k`, so `prefix(j - 1) = prefix(i) - k`

In other words: if the current running prefix sum is `curr`, and you've previously seen a prefix sum equal to `curr - k`, then there's a subarray ending at the current index with sum exactly `k`.

*(See the accompanying diagram: for `k = 3`, prefix sum up to `i` is `curr = 14`; a prefix sum of `11` seen earlier equals `curr - k`; the subarray between those two points — sum `3` — is the one being "found.")*

## Why a hash map, not a plain prefix sum array
We need to track **how often** each prefix sum has occurred, not just whether it occurred — if the input has negative numbers or zeroes, the same prefix sum value can repeat. Each repeat represents another valid starting point for a subarray ending at the current index. This is why `counts` maps `prefix sum → frequency`, rather than just being a set.

## Building the algorithm
1. Hash map `counts`, mapping prefix sum values → how many times each has occurred
2. **Initialize `counts[0] = 1`** — this accounts for the "empty prefix" (sum 0, before any elements). Necessary so that a subarray starting at index 0 (where there's no real "prefix before it") is still counted correctly.
3. Iterate through the input, maintaining `curr` = running prefix sum so far
4. At each index: **before** updating `counts` with the current prefix, add `counts[curr - k]` to the answer — this is the number of previously-seen prefixes that would make a valid subarray ending here
5. Then increment `counts[curr]` to record that this prefix sum has now occurred

## Why this mirrors Two Sum
Compare to [[Hashing - Checking for Existence]]'s Two Sum example: there, you lock in `num` and search for `target - num` (since `num + (target - num) = target`). Here, you lock in `curr` and search for `curr - k` (since `curr - (curr - k) = k`). Two Sum operates on raw array values directly; this pattern operates on **prefix sums** of the array instead.

## Worked mini-example
`nums = [0, 1, 2, 3, 4]`, `k = 5`, at index `i = 3`:
- `curr = 6` (prefix sum up to index 3: `0+1+2+3`)
- `counts` so far holds prefix sums `0, 1, 3` (seen at earlier indices)
- We want `curr - k = 6 - 5 = 1` → yes, `1` was seen before (prefix `[0, 1]`)
- Subtracting that earlier prefix from the current one: `[0,1,2,3] - [0,1] = [2,3]`, sum = 5 = k ✓ — the subarray found is `[2, 3]`

This pattern generalizes to any "exact value" subarray constraint — not just sums. See [[Hashing - Subarray Sum Equals K Example]] and [[Hashing - Nice Subarrays (Odd Count) Example]] for two worked LeetCode problems using this exact template.

#dsa #algorithms #hashing #hash-map #prefix-sum #counting

Related: [[Prefix Sum - Overview]], [[Hashing - Checking for Existence]], [[Subarrays and Substrings - Recognizing Patterns]]
