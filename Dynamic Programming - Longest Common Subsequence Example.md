# Dynamic Programming - Longest Common Subsequence Example

First example of a **multi-dimensional** DP problem — using more than one state variable.

## Problem: 1143. Longest Common Subsequence
Given `text1` and `text2`, return the length of their longest common [[Subsequences - Overview|subsequence]] (LCS).

Example: `text1="abcde"`, `text2="ace"` → `3` (`"ace"` is shared).

## Recognizing the DP signal
Asks for the **longest** of something, and deciding whether to use a given letter affects which future letters remain usable — same [[Dynamic Programming - When to Use It|two characteristics]] as every prior example.

## Part 1 — function and state
Two index variables needed — one per string. `dp(i, j)` = length of the LCS considering `text1` starting at index `i` and `text2` starting at index `j`.

## Part 2 — recurrence relation
Two cases at any `(i, j)`:
- **`text1[i] == text2[j]`:** found a matching character — always worth taking, since a match can never increase length by more than 1 at any step, so there's no benefit to skipping an available match. Advance both indices: `dp(i, j) = 1 + dp(i + 1, j + 1)`.
- **`text1[i] != text2[j]`:** no match here — try advancing **either** string individually and take the better result: `dp(i, j) = max(dp(i + 1, j), dp(i, j + 1))`.

## Part 3 — base case
If either string is exhausted (`i == len(text1)` or `j == len(text2)`), no characters remain to match → return `0`.

## Top-down code
```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        @cache
        def dp(i, j):
            if i == len(text1) or j == len(text2):
                return 0

            if text1[i] == text2[j]:
                return 1 + dp(i + 1, j + 1)

            return max(dp(i + 1, j), dp(i, j + 1))

        return dp(0, 0)
```

## Bottom-up code
```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        n = len(text1)
        m = len(text2)
        dp = [[0] * (m + 1) for _ in range(n + 1)]

        for i in range(n - 1, -1, -1):
            for j in range(m - 1, -1, -1):
                if text1[i] == text2[j]:
                    dp[i][j] = 1 + dp[i + 1][j + 1]
                else:
                    dp[i][j] = max(dp[i + 1][j], dp[i][j + 1])

        return dp[0][0]
```

Both loops run **backward** since `dp[i][j]` depends on higher indices (`i+1`, `j+1`) — same forward-dependency logic as [[Dynamic Programming - Solving Questions With Brainpower Example|Brainpower's]] backward loop, just nested across two dimensions here.

## A note on direction (again)
As with [[Dynamic Programming - House Robber Example|House Robber]], the direction of `dp` is a free choice as long as base cases and the recurrence stay internally consistent. An equally valid alternative: `dp(i, j)` = LCS considering `text1[0..i]` and `text2[0..j]`, base case at `i == -1 or j == -1`, and the recurrence looking at `dp(i-1, j)`, `dp(i, j-1)`, `dp(i-1, j-1)` instead. Same algorithm, opposite direction.

## Complexity
`n = len(text1)`, `m = len(text2)`. O(1) work per state → **O(n · m) time and space** (state count = product of the two index ranges, per [[Dynamic Programming - Complexity]]).

#dsa #algorithms #dynamic-programming

Related: [[Dynamic Programming - Framework]], [[Dynamic Programming - Complexity]], [[Subsequences - Overview]]
