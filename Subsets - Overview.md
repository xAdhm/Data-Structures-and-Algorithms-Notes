# Subsets - Overview

A **subset** is any collection of elements from the original array/string. **Order doesn't matter**, and elements don't need to be contiguous or adjacent.

Example: for `[1, 2, 3, 4]`, valid subsets include `[3, 2]`, `[4, 1, 2]`, `[1]`.

Subsets containing the same elements are considered the same subset — `[1, 2, 4]` and `[4, 1, 2]` are the same subset (order is irrelevant), which is the key difference from [[Subsequences - Overview|subsequences]].

## Subset vs. subsequence
Since order doesn't matter for subsets, finding "does a subset with 3 consecutive numbers (like 1, 2, 3) exist" is easier than finding a *subsequence* with the same property — a subset only needs those 3 elements to exist somewhere in the array; a subsequence needs them in that exact relative order.

Example: `[3, 2, 1]` has **no subsequence** `1, 2, 3` (wrong order), but it **does** have a subset `{1, 2, 3}` (order irrelevant).

## Practical implication: sorting is allowed
Because order doesn't matter for subsets, you're free to **sort the input** as a first step — something you generally can't do for subsequence problems, where relative order is the whole point.

## Where this comes up
Subsets are explored in much more depth in the **backtracking** chapter later in the course. For now this is just the vocabulary/distinction to recognize.

#dsa #algorithms #arrays #strings #subsets

Related: [[Subsequences - Overview]], [[Subarrays and Substrings - Recognizing Patterns]]
