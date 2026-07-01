# Sliding Window - Counting Valid Subarrays

When a problem asks for the **number** of valid subarrays (rather than the longest one), sliding window still applies — plus one extra math trick.

## The trick
Given a current valid window `(left, right)`, how many valid windows *end* at index `right`?

Answer: every window `(left, right)`, `(left+1, right)`, `(left+2, right)`, ..., `(right, right)` — i.e., fix the right bound and choose any left bound from `left` to `right` inclusive.

**Number of valid windows ending at `right` = size of the current window = `right - left + 1`.**

So instead of updating the answer with `max(...)` (as in the longest-subarray case, see [[Sliding Window - Dynamic Window Size]]), you **add** `right - left + 1` to a running count each time the window is valid.

## Example: 713. Subarray Product Less Than K
Given positive integers `nums` and integer `k`, count subarrays where the product of all elements is strictly less than `k`.

Example: `nums = [10, 5, 2, 6]`, `k = 100` → answer is 8:
`[10], [5], [2], [6], [10,5], [5,2], [2,6], [5,2,6]`

Walkthrough: at index 2, the product becomes too large, so remove the leftmost `10`. Window is now valid with length 2 → **2** valid subarrays end at this index (`[2]` and `[5,2]`).

Edge case: if `k <= 1`, no subarray can ever be valid (all elements are positive integers, so any single-element product is ≥ 1) — return 0 immediately.

**Complexity:** O(n) time (amortized O(1) per iteration), O(1) space.

#dsa #algorithms #sliding-window #arrays

Related: [[Sliding Window - Overview]], [[Sliding Window - Dynamic Window Size]]
