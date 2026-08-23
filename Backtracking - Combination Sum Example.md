# Backtracking - Combination Sum Example

## Problem: 39. Combination Sum
Given distinct positive integers `candidates` and `target`, return all unique combinations summing to `target`. **Each number may be reused unlimited times.**

## Building on Combinations
Reuses the [[Backtracking - Combinations Example|starting-index technique]] to avoid duplicates like `[2,2,3]` vs `[2,3,2]`. **Key difference:** since elements *can* repeat, when adding element at index `i`, the next call passes `i` (not `i + 1`, as in earlier examples where reuse wasn't allowed) — allowing the same element to be chosen again in the next recursive step.

## Tracking the running sum
Pass an integer `curr` alongside `path`, representing the sum of everything in `path` so far. **Why track it separately instead of recomputing from `path` each time:** avoids repeatedly summing the whole list at every node — a small but meaningful efficiency win, especially since it's easy to update incrementally as elements are added/removed.

**Pruning:** since all candidates are positive, once `curr + num > target`, that branch can never recover — skip it entirely rather than recursing into a guaranteed-dead path (see [[Backtracking - Overview|pruning]]).

## Base case
`curr == target` → valid combination found, save `path` and return. **Not every leaf is a valid answer** — a leaf could also occur where `curr < target` but every remaining candidate would push it over (in which case the loop simply finds no valid `num` to add, and the function naturally returns without ever hitting the `curr == target` condition).

## Code
```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        def backtrack(path, start, curr):
            if curr == target:
                ans.append(path[:])
                return

            for i in range(start, len(candidates)):
                num = candidates[i]
                if curr + num <= target:
                    path.append(num)
                    backtrack(path, i, curr + num)
                    path.pop()

        ans = []
        backtrack([], 0, 0)
        return ans
```

## Complexity
Let `n = len(candidates)`, `T = target`, `M = min(candidates)`. Maximum recursion depth ≈ `T / M` (repeatedly using the smallest candidate until hitting `target`). Each node can have up to `n` children → **O(n^(T/M)) time**. **Space: O(T/M)** for `path` and the recursion stack (excluding output).

#dsa #algorithms #backtracking #recursion

Related: [[Backtracking - Combinations Example]], [[Backtracking - Overview]]
