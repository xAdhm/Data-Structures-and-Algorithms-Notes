# Backtracking - Combinations Example

## Problem: 77. Combinations
Given integers `n` and `k`, return all combinations of `k` numbers chosen from the range `[1, n]` (any order).

Example: `n = 4, k = 2` → `[[2,4],[3,4],[2,3],[1,2],[1,3],[1,4]]`

## Reframing: this is Subsets, restricted to length k
Combinations disallow duplicates the same way subsets do (`[1,2]` and `[2,1]` are the same) — so this problem is really just "all subsets of `[1, n]` with length exactly `k`," reusing [[Backtracking - Subsets Example|the exact same algorithm]] with two adjustments:

1. **New base case:** `len(curr) == k` — no need to keep extending past the target length, since longer combinations aren't wanted.
2. **Answer nodes are leaves again** (like [[Backtracking - Permutations Example|Permutations]]), not every node — add `curr` to the answer only when the base case is hit, not on every call.

## No need to materialize a range array
Since the "input" here is just the numbers `1` to `n` (not a given array), there's no need to actually build a `[1, 2, ..., n]` list — the `for` loop's own iteration variable can directly represent each candidate number, saving the space that would otherwise go toward storing that array.

## The `i` argument, reused
Same [[Backtracking - Subsets Example|starting-index technique]]: `i` tracks where to start considering numbers from at each node, preventing duplicate/out-of-order combinations. Start at `i = 1` (smallest valid number); when adding `num`, pass `num + 1` to the next call.

## Code
```python
class Solution:
    def combine(self, n: int, k: int) -> List[List[int]]:
        def backtrack(curr, i):
            if len(curr) == k:
                ans.append(curr[:])
                return

            for num in range(i, n + 1):
                curr.append(num)
                backtrack(curr, num + 1)
                curr.pop()

        ans = []
        backtrack([], 1)
        return ans
```

## Complexity
Genuinely difficult to derive exactly — the article gives it as **O(k · n! / ((n-k)! · k!))**. A reasonable **upper-bound approximation**, sufficient for interview purposes: the first call's loop runs `n` times, the next runs up to `n-1` times, and so on — suggesting O(n!) — but since the max recursion depth is `k` (not `n`), the "factorial multiplication" only goes down to `n - k`, not all the way to `1`. This gives roughly `n! / (n-k)!` total calls. Each combination found also costs O(k) to copy → **≈ O(k · n! / (n-k)!)**. An interviewer should accept an approximation reasoned through this way, as long as the thought process is explained (same caveat as [[Backtracking - Permutations Example]]).

**Space: O(k)** for `curr` and the recursion call stack.

## The bigger pattern across all three examples
Permutations, Subsets, and Combinations share nearly identical code shape — the differences are all in **which nodes count as answers** (leaves only vs. every node) and **how children are generated** (whole input vs. starting-index restricted). Model the problem as a tree first, then figure out what each node's children should be — the actual backtracking mechanics (modify → recurse → undo) stay the same across all three.

#dsa #algorithms #backtracking #recursion

Related: [[Backtracking - Overview]], [[Backtracking - Subsets Example]], [[Backtracking - Permutations Example]]
