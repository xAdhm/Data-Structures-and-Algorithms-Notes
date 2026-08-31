# Dynamic Programming - Minimum Path Sum Example

## Problem: 64. Minimum Path Sum
`m x n` grid of non-negative numbers. Find a top-left → bottom-right path (down/right moves only) that **minimizes** the sum of visited numbers.

Same setup as [[Dynamic Programming - Unique Paths Example]] — matrix, top-left start, bottom-right target, down/right only — but optimizing a **sum** instead of counting paths.

## Part 1 — function and state
`dp(row, col)` = minimum path sum to reach `(row, col)` from `(0, 0)`. Answer: `dp(m-1, n-1)`.

## Part 2 — recurrence relation
Arriving at `(row, col)` means coming from above or from the left — take whichever predecessor had the **smaller** running sum, then add the current cell's value:

`dp(row, col) = grid[row][col] + min(dp(row - 1, col), dp(row, col - 1))` (staying in bounds)

## Part 3 — base case
`dp(0, 0) = grid[0][0]` — the path sum starting (and, so far, ending) at the origin.

## Top-down code
```python
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        @cache
        def dp(row, col):
            if row + col == 0:
                return grid[row][col]

            ans = float("inf")
            if row > 0:
                ans = min(ans, dp(row - 1, col))
            if col > 0:
                ans = min(ans, dp(row, col - 1))

            return grid[row][col] + ans

        m = len(grid)
        n = len(grid[0])
        return dp(m - 1, n - 1)
```

## Bottom-up code
```python
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        m = len(grid)
        n = len(grid[0])
        dp = [[0] * n for _ in range(m)]
        dp[0][0] = grid[0][0]

        for row in range(m):
            for col in range(n):
                if row + col == 0:
                    continue

                ans = float("inf")
                if row > 0:
                    ans = min(ans, dp[row - 1][col])
                if col > 0:
                    ans = min(ans, dp[row][col - 1])

                dp[row][col] = grid[row][col] + ans

        return dp[m - 1][n - 1]
```

## Space optimization: O(n)
Same reasoning as [[Dynamic Programming - Unique Paths Example|Unique Paths]] — the recurrence only ever looks at "row above, same column" and "same row, previous column," so a single running row suffices:

```python
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        m = len(grid)
        n = len(grid[0])
        dp = [float("inf")] * n
        dp[0] = 0
        for row in range(m):
            next_row = [0] * n
            for col in range(n):
                next_row[col] = dp[col]
                if col > 0:
                    next_row[col] = min(next_row[col], next_row[col - 1])

                next_row[col] += grid[row][col]
            dp = next_row
        return dp[n - 1]
```

## Complexity
Identical profile to [[Dynamic Programming - Unique Paths Example]]: **O(m·n) time**, **O(m·n) space** with the full table, improvable to **O(n)** with the row-by-row optimization.

## Chapter closing note
This wraps up the core Dynamic Programming chapter. DP isn't as universally common in interviews as some other topics, but the [[Dynamic Programming - Framework|3-part framework]] (function/state, recurrence relation, base cases) is the main tool worth internalizing — it turns even unfamiliar-looking problems into a systematic construction process.

#dsa #algorithms #dynamic-programming #graphs

Related: [[Dynamic Programming - Unique Paths Example]], [[Dynamic Programming - Framework]]
