# Dynamic Programming - Framework

A systematic 3-part framework for building any [[Dynamic Programming - Overview|DP]] algorithm — works for beginners and general-purpose, top-down first.

**Running example:** Min Cost Climbing Stairs — given `cost[i]` for step `i`, you can climb 1 or 2 steps at a time after paying that step's cost, and can start at step 0 or step 1. Find the minimum cost to reach the top (past the last index).

## Part 1 — A function (or data structure) that computes the answer for any given state
Two decisions needed:
1. **What does the function return?** Here: `dp(state)` returns the **minimum cost** to climb the stairs for a given state.
2. **What arguments (state variables) does it need?** Only one is relevant here: an index `i` along the input.

**How to reason about state variables:** imagine the problem as a real-life scenario — what information do you need to *fully* describe it? You need to know which step you're on (`i`). You don't need, say, "the color of your socks" — that's technically a different scenario but doesn't affect anything relevant to the cost. This is the litmus test for [[Dynamic Programming - State|deciding what belongs in the state]].

So: `dp(i)` = minimum cost to climb the stairs **up to and including step `i`** — the same "index represents everything up to this point" convention flagged in [[Dynamic Programming - State]].

## Part 2 — A recurrence relation to transition between states
Usually **the hardest part** of building a DP algorithm.

**Reasoning it out:** to reach step 100, you must have arrived from either step 99 or step 98 (since you can only move 1 or 2 steps at a time). So:

`dp(100) = min(dp(99) + cost[99], dp(98) + cost[98])`

Generalized:

`dp(i) = min(dp(i - 1) + cost[i - 1], dp(i - 2) + cost[i - 2])`

This is the problem's **recurrence relation** — same concept as Fibonacci's `F(n) = F(n-1) + F(n-2)` from [[Dynamic Programming - Overview]].

## Part 3 — Base cases
The recurrence relation alone is useless — computing `dp(100)` needs `dp(99)` and `dp(98)`, which need `dp(98)`/`dp(97)` and `dp(97)`/`dp(96)`, and so on forever without a stopping point.

Since the problem allows starting at step 0 *or* step 1 for free: `dp(0) = dp(1) = 0`. With these anchors, `dp(2)` becomes computable, then `dp(3)`, and so on up to the target. Figuring out base cases is usually straightforward — mainly requires reading the problem statement carefully.

## Top-down implementation
```python
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        # 1. A function that returns the answer
        def dp(i):
            if i <= 1:
                # 3. Base cases
                return 0

            if i in memo:
                return memo[i]

            # 2. Recurrence relation
            memo[i] = min(dp(i - 1) + cost[i - 1], dp(i - 2) + cost[i - 2])
            return memo[i]

        memo = {}
        return dp(len(cost))
```

Memoizing (per [[Dynamic Programming - Overview]]) drops this from O(2ⁿ) to **O(n)**, where `n = len(cost)`.

## Converting top-down → bottom-up (general method)
1. Implement the top-down approach first.
2. Initialize a `dp` array sized to match the state variables (e.g. a problem with state `(i, k)` needs a 2D array of size `len(nums) × k`) — so `dp(4, 6)` in top-down becomes `dp[4][6]` in bottom-up.
3. Set base cases directly in the array (often just array-initialization defaults, like `0` here).
4. Write `for` loop(s) over the state variables — nested loops if multiple state variables — iterating from the base cases up toward the target.
5. Each iteration of the innermost loop = one top-down function call for that state. Copy the top-down logic in, replacing `dp(...)` calls with `dp[...]` array accesses.
6. Return `dp[...]` (the target state) instead of calling `dp(...)`.

## Bottom-up implementation
```python
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        n = len(cost)
        # Step 2
        dp = [0] * (n + 1)

        # Step 3: Base cases are implicitly defined as they are 0
        # Step 4
        for i in range(2, n + 1):
            # Step 5
            dp[i] = min(dp[i - 1] + cost[i - 1], dp[i - 2] + cost[i - 2])

        # Step 6
        return dp[n]
```

Directly mirrors the top-down version — same recurrence relation, same base cases, just restructured as iteration over an array instead of memoized recursive calls (see [[Dynamic Programming - Top-Down vs Bottom-Up]]).

#dsa #algorithms #dynamic-programming

Related: [[Dynamic Programming - Overview]], [[Dynamic Programming - State]], [[Dynamic Programming - Top-Down vs Bottom-Up]]
