# Dynamic Programming - Maximum Value of K Coins From Piles Example

## Problem: 2218. Maximum Value of K Coins From Piles
`n` piles of coins, each pile an ordered list (top to bottom). Each move takes the top coin off any pile. Choose exactly `k` coins total to maximize their sum.

## Part 1 — function and state
Two state variables: `i` (current pile) and `remain` (moves/coins left to take). `dp(i, remain)` = max value achievable starting from pile `i` onward, with `remain` coins still to take.

## Part 2 — recurrence relation
At pile `i`, two broad choices:
- **Skip the pile entirely:** `dp(i + 1, remain)`.
- **Take some number of coins from the top of this pile** (0 up to as many as available or as many as `remain` allows) — for each possible count `j+1` taken (indices `0` through `j`), the gain is the prefix sum `sum(piles[i][:j+1])`, plus whatever's achievable from the next pile with the reduced budget: `dp(i + 1, remain - j - 1)`.

Track the running prefix sum incrementally with a variable `curr` while iterating `j`, rather than recomputing `sum(piles[i][:j+1])` from scratch each time (same efficiency idea as [[Backtracking - Combination Sum Example|Combination Sum's running `curr`]]).

`dp(i, remain) = max(skip, take)`, where `take` = the best result across all valid `j` from `0` to `min(remain, len(piles[i])) - 1`.

## Part 3 — base case
`i == len(piles)` (no piles left) or `remain == 0` (no more coins allowed) → `0`.

## Top-down code
```python
class Solution:
    def maxValueOfCoins(self, piles: List[List[int]], k: int) -> int:
        @cache
        def dp(i, remain):
            if i == len(piles) or remain == 0:
                return 0

            ans = dp(i + 1, remain) # skip this pile
            curr = 0
            for j in range(min(remain, len(piles[i]))):
                curr += piles[i][j]
                ans = max(ans, curr + dp(i + 1, remain - j - 1))

            return ans
        return dp(0, k)
```

## Bottom-up code
```python
class Solution:
    def maxValueOfCoins(self, piles: List[List[int]], k: int) -> int:
        n = len(piles)
        dp = [[0] * (k + 1) for _ in range(n + 1)]
        for i in range(n - 1, -1, -1):
            for remain in range(1, k + 1):
                dp[i][remain] = dp[i + 1][remain] # skip this pile
                curr = 0
                for j in range(min(remain, len(piles[i]))):
                    curr += piles[i][j]
                    dp[i][remain] = max(dp[i][remain], curr + dp[i + 1][remain - j - 1])
        return dp[0][k]
```

Iterates `i` backward from `n` and `remain` forward from `1`, same reasoning as [[Dynamic Programming - Best Time to Buy and Sell Stock IV Example|Buy and Sell Stock IV]]'s loop configuration.

## Complexity
Let `x` = average coins per pile. States: **O(n · k)** (pile index × remaining coins). Each state does a `for` loop up to `x` iterations → **O(n · k · x) time**. **Space: O(n · k)** for the `dp` table/memo.

## Closing thought on the chapter
Multi-dimensional DP problems can look intimidating, but the [[Dynamic Programming - Framework|same 3-part framework]] applies regardless of how many state variables are involved — carefully identifying state, recurrence, and base cases turns even a problem like this into a systematic construction rather than a guessing game.

#dsa #algorithms #dynamic-programming

Related: [[Dynamic Programming - Best Time to Buy and Sell Stock IV Example]], [[Dynamic Programming - Framework]], [[Dynamic Programming - Complexity]]
