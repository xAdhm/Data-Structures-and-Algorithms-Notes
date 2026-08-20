# Backtracking - Subsets Example

## Problem: 78. Subsets
Given unique integers `nums`, return all subsets (any order, no duplicates).

Example: `nums = [1,2,3]` → `[[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]`

## Key differences from Permutations
Compared to [[Backtracking - Permutations Example]]:
- **Length varies** — a subset can be any length, not fixed at `n`.
- **Order doesn't matter** — `[1,2]` and `[2,1]` are the *same* subset (this is the [[Subsets - Overview|subset, not subsequence]] distinction from the arrays chapter).

## Avoiding duplicates: the "starting index" technique
Since order doesn't matter, iterating over the *entire* input at every node (like Permutations did) would generate the same subset multiple times in different orders — e.g. both `[1,2]` and `[2,1]` would appear. **Fix:** pass an integer `i` into `backtrack` representing "only consider elements from this index onward." When adding element at index `j`, the next call only considers indices `> j` (pass `j + 1`) — this guarantees every subset is built in strictly increasing index order, so each unique combination is only ever generated once.

**This is a very common general technique** for avoiding duplicates in backtracking: an integer argument tracking the starting point for iteration at each node.

## Every node is an answer, not just leaves
Unlike Permutations (where only leaf nodes — length `n` — were valid answers), a subset of **any** length is valid — including the empty subset (the root itself). So `curr` gets added to the answer **at the start of every call**, not just at a base case.

## Code
```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        def backtrack(curr, i):
            if i > len(nums):
                return
            ans.append(curr[:])
            for j in range(i, len(nums)):
                curr.append(nums[j])
                backtrack(curr, j + 1)
                curr.pop()
        ans = []
        backtrack([], 0)
        return ans
```

**Note:** the `i > len(nums)` base case is technically unreachable in practice (the loop bound `range(i, len(nums))` naturally prevents `i` from ever exceeding `len(nums)` through a recursive call) — included for clarity/safety rather than because it's ever actually triggered.

## Complexity
There are **2ⁿ** total subsets (`n = len(nums)`) — each element is independently either included or excluded. Think of the algorithm as a [[Binary Trees - DFS Overview|DFS]] over a tree with 2ⁿ nodes; at each node, copying `curr` costs O(n) → **O(n · 2ⁿ) time**. **Space: O(n)** for `curr` and the recursion call stack.

#dsa #algorithms #backtracking #recursion

Related: [[Backtracking - Overview]], [[Backtracking - Permutations Example]], [[Backtracking - Combinations Example]], [[Subsets - Overview]]
