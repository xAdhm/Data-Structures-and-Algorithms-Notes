# Dynamic Programming - Solving Questions With Brainpower Example

## Problem: 2140. Solving Questions With Brainpower
Process `questions[i] = [points_i, brainpower_i]` in order. Solving question `i` earns `points_i` but locks out the next `brainpower_i` questions. Skipping moves to the next question with no penalty. Maximize total points.

## Recognizing the DP signal
Asks for a **maximum score**, and each question forces a genuine **take-or-skip decision** that directly constrains which future questions are even available — the same [[Dynamic Programming - When to Use It|two DP characteristics]] as [[Dynamic Programming - House Robber Example|House Robber]].

## Part 1 — function and state
`dp(i)` = maximum score achievable starting from question `i` onward.

**Do we need a separate "questions remaining to skip" counter as state?** Not necessary — same as [[Dynamic Programming - House Robber Example|House Robber's `prev` boolean]], this information gets folded directly into the recurrence relation instead.

## Part 2 — recurrence relation
At question `i`, two choices:
- **Solve it:** gain `questions[i][0]` points, but the next `questions[i][1]` questions become unsolvable — the next available question is at index `j = i + questions[i][1] + 1`. Total: `questions[i][0] + dp(j)`.
- **Skip it:** move to the very next question: `dp(i + 1)`.

`dp(i) = max(questions[i][0] + dp(j), dp(i + 1))`, where `j = i + questions[i][1] + 1`

## Part 3 — base case
Since this problem moves **forward** through the array (opposite of House Robber's backward-looking recurrence — see [[Dynamic Programming - House Robber Example]]'s "note on direction"), the base case sits at the **end**: once `i >= len(questions)`, the exam is over — no more points possible.

`dp(i) = 0`, when `i >= n`

## Top-down code
```python
class Solution:
    def mostPoints(self, questions: List[List[int]]) -> int:
        @cache
        def dp(i):
            if i >= len(questions):
                return 0

            j = i + questions[i][1] + 1
            return max(questions[i][0] + dp(j), dp(i + 1))

        return dp(0)
```

## Bottom-up code
```python
class Solution:
    def mostPoints(self, questions: List[List[int]]) -> int:
        n = len(questions)
        dp = [0] * (n + 1) # n + 1 to avoid out of bounds

        for i in range(n - 1, -1, -1):
            j = i + questions[i][1] + 1
            # need to make sure we don't go out of bounds
            dp[i] = max(questions[i][0] + dp[min(j, n)], dp[i + 1])

        return dp[0]
```

**Why the loop runs backward (`range(n-1, -1, -1)`):** since `dp(i)` depends on `dp(i+1)` and `dp(j)` where `j > i`, every value the recurrence needs must already be computed — meaning higher indices need to be filled in *before* lower ones, the mirror image of [[Dynamic Programming - Longest Increasing Subsequence Example|LIS's forward-iterating loop]].

**Why `dp` is sized `n + 1`, and `min(j, n)` is used:** `j` can legitimately land past the end of the array (skipping locks out more questions than remain) — padding the array with one extra slot (always `0`, representing "exam over") and clamping `j` to that slot avoids an out-of-bounds access while correctly contributing `0` points for an overshoot.

## Complexity
**O(n) time** — `n` states, O(1) work per state (looking up `dp[j]`/`dp[i+1]` and comparing). **Space: O(n)** for the `dp` array/memo — **cannot** be reduced to O(1) the way House Robber's could, since the recurrence relation is **not static**: `j` depends on `questions[i][1]`, which varies arbitrarily per index, rather than always looking back a fixed number of states.

#dsa #algorithms #dynamic-programming

Related: [[Dynamic Programming - Framework]], [[Dynamic Programming - House Robber Example]], [[Dynamic Programming - Longest Increasing Subsequence Example]]
