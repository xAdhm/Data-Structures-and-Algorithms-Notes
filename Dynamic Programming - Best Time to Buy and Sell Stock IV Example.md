# Dynamic Programming - Best Time to Buy and Sell Stock IV Example

Three state variables — the most complex example so far in terms of dimensionality.

## Problem: 188. Best Time to Buy and Sell Stock IV
Given `prices[i]` (stock price on day `i`) and integer `k`: hold at most one unit of stock at a time, maximize profit with **at most `k` transactions**.

## Recognizing the DP signal
Many interacting decisions — buy today? sell today? — each constraining what's possible next (can't buy while already holding; can't sell without holding; each buy/sell consumes a limited transaction) — a clear [[Dynamic Programming - When to Use It|DP fit]].

## Part 1 — function and state
Three state variables needed:
- `i` — current day (usual index variable)
- `holding` — boolean, are we currently holding stock?
- `remain` — how many transactions are left

`dp(i, holding, remain)` = max profit achievable from day `i` onward, given current holding status and remaining transaction budget. Answer to the problem: `dp(0, False, k)`.

## Part 2 — recurrence relation
At any state, always consider **skipping**: `dp(i + 1, holding, remain)` — move to the next day, nothing else changes.

Additionally:
- **If not holding:** can **buy** — pay `prices[i]`, become holding, transaction not yet complete (`remain` unchanged since a transaction is typically counted as a full buy+sell pair — the cost is paid now but the "transaction" itself completes on sell): `-prices[i] + dp(i + 1, True, remain)`.
- **If holding:** can **sell** — gain `prices[i]`, stop holding, and this completes one transaction: `prices[i] + dp(i + 1, False, remain - 1)`.

`dp(i, holding, remain) = max(skip, buy_or_sell_if_applicable)`

## Part 3 — base cases
`i == len(prices)` (ran out of days) or `remain == 0` (ran out of transactions) → return `0`, no more profit possible either way.

## Top-down code
```python
class Solution:
    def maxProfit(self, k: int, prices: List[int]) -> int:
        @cache
        def dp(i, holding, remain):
            if i == len(prices) or remain == 0:
                return 0

            ans = dp(i + 1, holding, remain)
            if holding:
                ans = max(ans, prices[i] + dp(i + 1, False, remain - 1))
            else:
                ans = max(ans, -prices[i] + dp(i + 1, True, remain))

            return ans

        return dp(0, False, k)
```

## Bottom-up code
```python
class Solution:
    def maxProfit(self, k: int, prices: List[int]) -> int:
        n = len(prices)
        dp = [[[0] * (k + 1) for _ in range(2)] for __ in range(n + 1)]
        for i in range(n - 1, -1, -1):
            for remain in range(1, k + 1):
                for holding in range(2):
                    ans = dp[i + 1][holding][remain]
                    if holding:
                        ans = max(ans, prices[i] + dp[i + 1][0][remain - 1])
                    else:
                        ans = max(ans, -prices[i] + dp[i + 1][1][remain])

                    dp[i][holding][remain] = ans

        return dp[0][0][k]
```

**Configuring nested loops correctly is genuinely tricky here** — the important guiding principle: iteration must start from the base cases and work toward the answer, so `i` iterates down from `n`, and `remain` iterates up from `1` (since `remain = 0` is itself a base case, already correctly `0` by array initialization). `holding` (0 or 1) can be looped in either order since it doesn't depend on itself.

## Complexity
Work per state is O(1). Number of states = product of each state variable's range: `n` (days) × `2` (holding, effectively constant) × `k` (remain) → **O(n · k) time and space**.

#dsa #algorithms #dynamic-programming

Related: [[Dynamic Programming - Longest Common Subsequence Example]], [[Dynamic Programming - Complexity]], [[Dynamic Programming - State]]
