# Backtracking - Permutations Example

## Problem: 46. Permutations
Given distinct integers `nums`, return all possible permutations (any order).

Example: `nums = [1,2,3]` → `[[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]`

## Modeling as a tree
Build each permutation with `backtrack(curr)`, where `curr` = the permutation being built so far. **Base case:** `len(curr) == len(nums)` — a complete permutation, add it to the answer and return (base cases are the **leaf nodes** of the [[Backtracking - Overview|backtracking tree]]).

To generate every permutation, every element needs a turn in the first position, and for each of those, every *remaining* element needs a turn in the second position, and so on — so each call to `backtrack` **loops over the entire input**, adding whichever number isn't already used (`num not in curr`) to avoid duplicate elements within a single permutation.

## Code
```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        def backtrack(curr):
            if len(curr) == len(nums):
                ans.append(curr[:])
                return

            for num in nums:
                if num not in curr:
                    curr.append(num)
                    backtrack(curr)
                    curr.pop()

        ans = []
        backtrack([])
        return ans
```

**Why `curr[:]` (a copy) instead of `curr` directly:** `curr` is a single mutable list being repeatedly modified and un-modified throughout the whole recursion — appending the live reference would mean every entry in `ans` points to the *same* list, which keeps changing. A shallow copy freezes the current state at the moment of appending.

**The `curr.pop()` after the recursive call is the actual "backtracking" step** — undoing the modification made just before recursing, moving back "up" the tree to try the next sibling option, per [[Backtracking - Overview]].

## Complexity
Let `n = len(nums)`. The root call makes `n` calls; each of those makes `n-1` (avoiding duplicates); each of those makes `n-2`; and so on — roughly **O(n!)** total calls. Each call loops over `n` elements, and the `num not in curr` check itself costs O(n) → each call costs ~O(n²). Combined estimate: **O(n² · n!)** (or **O(n · n!)** if `curr`'s membership check were optimized with a separate hash set for O(1) lookups instead of O(n) list scanning).

**Note:** the *true* time complexity is more intricate and requires more advanced math to derive exactly — but presenting this level of reasoning (call-count estimate × per-call cost) is a perfectly acceptable level of rigor for an interview. This difficulty in exact analysis is typical for backtracking problems generally.

#dsa #algorithms #backtracking #recursion

Related: [[Backtracking - Overview]], [[Backtracking - Subsets Example]]
