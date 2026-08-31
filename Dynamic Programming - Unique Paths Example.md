# Dynamic Programming - Unique Paths Example

DP on a matrix is a common pattern — the matrix can be modeled as an [[Graphs - Input Formats|implicit grid graph]], exactly like the ones from the trees/graphs chapter, with each square as a node and edges between adjacent squares.

## Problem: 62. Unique Paths
`m x n` grid; a robot starts top-left, wants to reach bottom-right, moving only **down** or **right**. Return the number of distinct paths.

## Part 1 — function and state
`dp(row, col)` = number of unique paths to reach `(row, col)` from `(0, 0)`. Answer: `dp(m-1, n-1)`.

## Part 2 — recurrence relation
Since only down/right moves are allowed, arriving at `(row, col)` means coming from either directly **above** (`row-1, col`) or directly **left** (`row, col-1`). Total paths to `(row, col)` = sum of paths to each of those (every distinct path to either predecessor extends into a distinct path here):

`dp(row, col) = dp(row - 1, col) + dp(row, col - 1)` (staying in bounds)

## Part 3 — base case
`dp(0, 0) = 1` — exactly one "way" to be at the start: starting there.

## Top-down code
```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        @cache
        def dp(row, col):
            if row + col == 0:
                return 1 # Base case
            ways = 0
            if row > 0:
                ways += dp(row - 1, col)
            if col > 0:
                ways += dp(row, col - 1)

            return ways

        return dp(m - 1, n - 1)
```

## Bottom-up code
```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = [[0] * n for _ in range(m)]
        dp[0][0] = 1

        for row in range(m):
            for col in range(n):
                if row > 0:
                    dp[row][col] += dp[row - 1][col]
                if col > 0:
                    dp[row][col] += dp[row][col - 1]
        return dp[m - 1][n - 1]
```

## Space optimization: O(n)
The recurrence is **static** — always looks at exactly "previous row, same column" and "same row, previous column" — so the full 2D table isn't needed. Process **one row at a time**, keeping only the previous row in memory:

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = [0] * n
        dp[0] = 1

        for _ in range(m):
            next_row = [0] * n
            for col in range(n):
                next_row[col] += dp[col]
                if col > 0:
                    next_row[col] += next_row[col - 1]

            dp = next_row
        return dp[n - 1]
```
`dp[col]` (before overwriting) represents "value from the row above"; `next_row[col-1]` represents "value from the left in the current row" — both pieces the recurrence needs, without storing the entire grid.

## Complexity
**O(m·n) time** (O(1) work per state, `m·n` states). **Space: O(m·n)** with the full table, improvable to **O(n)** with the row-by-row optimization (same static-recurrence justification as [[Dynamic Programming - House Robber Example|House Robber's O(1) trick]], just one dimension instead of collapsing to a constant).

#dsa #algorithms #dynamic-programming #graphs

Related: [[Dynamic Programming - Framework]], [[Dynamic Programming - Minimum Path Sum Example]], [[Graphs - Input Formats]]
