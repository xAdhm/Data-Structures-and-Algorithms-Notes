# Prefix Sum - Space Optimization

Shows that the *concept* of a prefix sum doesn't always require actually building the array — sometimes it can be replicated with a single running variable, cutting space from O(n) to O(1).

## Problem: 2270. Number of Ways to Split Array
Given `nums`, find the number of ways to split it into a left section and right section such that the left section's sum ≥ the right section's sum. The right section must have at least one number.

## Brute force — O(n²)
For each split index `i`: iterate `0` to `i` for the left sum, iterate `i+1` to end for the right sum.

## Prefix sum approach — O(n)
Build a prefix sum first, then for each index `i`, get the left and right section sums in O(1) each (same idea as [[Prefix Sum - Range Sum Queries Example]]).

## Do we need the actual array?
In this problem, `prefix` is only ever accessed **incrementally** — `prefix[i]` as `i` increases by 1 each iteration. That means the full array isn't necessary:

- **Left section:** initialize `leftSection = 0`, and add `nums[i]` to it each iteration as `i` advances — computed on the fly, no array needed.
- **Right section:** by definition, it's everything *not* in the left section. Pre-compute `total` = sum of the entire array once, then `rightSection = total - leftSection`.

This is still fundamentally a prefix sum — `leftSection` at each step *is* the value that `prefix[i]` would have held — just computed with a single integer instead of stored in an array.

**Result:** space complexity improves from O(n) (storing the full prefix array) down to **O(1)**, while keeping O(n) time.

## Takeaway
Whenever prefix values are only accessed in incrementing order (never jumped to or re-accessed out of sequence), consider whether a running variable can replace the full prefix array to save space.

#dsa #algorithms #prefix-sum #arrays

Related: [[Prefix Sum - Overview]], [[Prefix Sum - Range Sum Queries Example]]
