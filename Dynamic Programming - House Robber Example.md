# Dynamic Programming - House Robber Example

## Problem: 198. House Robber
Rob houses along a street (`nums[i]` = money in house `i`), but can't rob two **adjacent** houses (triggers the alarm). Maximize total money robbed.

Already introduced as the motivating example for [[Dynamic Programming - When to Use It]] — this note covers the actual DP construction, applying the [[Dynamic Programming - Framework|3-part framework]].

## Part 1 — function and state
`dp(i)` returns the maximum money robbable considering houses `0` through `i` (inclusive) — the standard "index represents everything up to here" convention (see [[Dynamic Programming - State]]).

**Do we need a `prev` boolean (was the previous house robbed)?** Not necessary — that information can be folded directly into the recurrence relation instead of being an explicit state variable.

## Part 2 — recurrence relation
At house `i`, two choices:
- **Rob it:** gain `nums[i]`, but can't have robbed house `i-1` — meaning the best score leading up to this point must have come from **2 houses back**: `dp(i-2) + nums[i]`.
- **Skip it:** gain nothing new, but can carry forward whatever the best score was up through the previous house: `dp(i-1)`.

Take the max of the two options:

`dp(i) = max(dp(i - 1), dp(i - 2) + nums[i])`

## Part 3 — base cases
- One house: might as well rob it → `dp(0) = nums[0]`
- Two houses: can only rob one → `dp(1) = max(nums[0], nums[1])`

**Why two base cases are needed:** without explicitly handling `dp(1)`, computing it via the recurrence would require `dp(-1)`, which doesn't exist.

## Top-down code
```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        def dp(i):
            # Base cases
            if i == 0:
                return nums[0]
            if i == 1:
                return max(nums[0], nums[1])

            if i in memo:
                return memo[i]

            # Recurrence relation
            memo[i] = max(dp(i - 1), dp(i - 2) + nums[i])
            return memo[i]

        memo = {}
        return dp(len(nums) - 1)
```

**Python shortcut:** `functools.cache` automatically memoizes a function — just decorate it, no manual hash map needed:
```python
from functools import cache

class Solution:
    def rob(self, nums: List[int]) -> int:
        @cache
        def dp(i):
            if i == 0:
                return nums[0]
            if i == 1:
                return max(nums[0], nums[1])
            return max(dp(i - 1), dp(i - 2) + nums[i])
        return dp(len(nums) - 1)
```

## Bottom-up code
```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        # To avoid out of bounds error from setting base case
        if len(nums) == 1:
            return nums[0]

        n = len(nums)
        dp = [0] * n

        # Base cases
        dp[0] = nums[0]
        dp[1] = max(nums[0], nums[1])

        for i in range(2, n):
            # Recurrence relation
            dp[i] = max(dp[i - 1], dp[i - 2] + nums[i])

        return dp[n - 1]
```

## Improving space to O(1)
At state `i`, only the **previous two** states are ever needed — everything further back becomes irrelevant once passed. This optimization is possible whenever the recurrence relation is **static** (always looks at a fixed, small number of prior states, regardless of input) — see [[Dynamic Programming - Complexity]].

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        if len(nums) == 1:
            return nums[0]

        n = len(nums)
        # Base cases
        back_two = nums[0]
        back_one = max(nums[0], nums[1])

        for i in range(2, n):
            # back_two becomes back_one, and back_one gets updated
            back_one, back_two = max(back_one, back_two + nums[i]), back_one
        return back_one
```

**Important caveat:** this O(1) space trick only works for **bottom-up**. The top-down recursive call stack itself uses O(n) space regardless — that overhead can't be avoided even if the hash map were removed, since the stack depth is tied to `n`.

## A note on direction (dp(i) can point either way)
Everything above defines `dp(i)` as "the answer considering elements **0 through i**" — extremely common, and the more intuitive choice here. But `dp` could instead be defined as "the answer considering elements **from i to the end**" — a perfectly valid alternative, just less intuitive for this particular problem.

**Under this flipped definition:** the answer to the original problem becomes `dp(0)` (not `dp(n-1)`); base cases move to `dp(n-1)` and `dp(n-2)`; and the recurrence relation looks **forward** (`i+1`, `i+2`) instead of backward.

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        def dp(i):
            # Base cases
            if i == len(nums) - 1:
                return nums[-1]
            if i == len(nums) - 2:
                return max(nums[-1], nums[-2])
            if i in memo:
                return memo[i]
            # Recurrence relation
            memo[i] = max(dp(i + 1), dp(i + 2) + nums[i])
            return memo[i]
        memo = {}
        return dp(0)
```

**Takeaway:** the definition of `dp` is entirely up to the problem solver — as long as base cases and the recurrence relation are made consistent with whatever definition is chosen, either direction works. This particular problem doesn't benefit from the flipped direction, but other problems sometimes do.

## Complexity
**O(n) time** (each state computed once, O(1) work per state), **O(n) space** for top-down (memo) or standard bottom-up (array) — improvable to **O(1) space** in bottom-up specifically, per above.

#dsa #algorithms #dynamic-programming

Related: [[Dynamic Programming - Framework]], [[Dynamic Programming - When to Use It]], [[Dynamic Programming - Longest Increasing Subsequence Example]]
