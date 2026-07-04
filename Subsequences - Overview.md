# Subsequences - Overview

A **subsequence** is a set of elements from an array/string that keeps the same **relative order** but does **not** need to be contiguous (contrast with subarrays/substrings — see [[Subarrays and Substrings - Recognizing Patterns]]).

Example: for `[1, 2, 3, 4]`, valid subsequences include `[1, 3]`, `[4]`, `[]`, `[2, 3]` — but **not** `[3, 2]` (wrong order), `[5]` (not in original), or `[4, 1]` (wrong order).

## Difficulty
Subsequence problems are generally harder than subarray/substring problems. This topic gets revisited more deeply later in the course — **dynamic programming** solves a lot of subsequence problems.

## Common pattern so far: two pointers
Given the patterns covered up to this point, **two pointers** (specifically the two-iterables method — see [[Two Pointers - Two Iterables Method]]) is the most common technique associated with subsequences, particularly when two input arrays/strings are given (e.g. "Is Subsequence," covered in that note).

**Not applicable here:** prefix sums and sliding windows — both represent subarrays/substrings specifically (contiguous), so they don't apply to subsequence problems.

## Subsequence vs. subset — when order doesn't matter
If a subsequence problem doesn't actually care about order (e.g. it just wants the sum of the subsequence's elements), it can be treated the same as a [[Subsets - Overview|subset]] problem instead — which opens up techniques not available for order-sensitive subsequences, like sorting the input first.

#dsa #algorithms #arrays #strings #subsequences

Related: [[Subarrays and Substrings - Recognizing Patterns]], [[Subsets - Overview]], [[Two Pointers - Two Iterables Method]]
