# Dynamic Programming - Longest Increasing Subsequence Example

## Problem: 300. Longest Increasing Subsequence (LIS)
Given `nums`, return the length of the longest **strictly increasing** [[Subsequences - Overview|subsequence]].

## Recognizing the DP signal
Asks for a **maximum length** (first [[Dynamic Programming - When to Use It|DP characteristic]]), and choosing to include an element **constrains future choices** — e.g. with `nums = [1,2,5,3,4]`, taking the `5` increases length now but blocks taking `3` and `4` later (second characteristic).

## Part 1 — function and state
`dp(i)` = length of the LIS that **ends with** the `i`th element specifically (not just "considering elements up to `i`" — a subtly different, more useful framing for this problem).

## Part 2 — recurrence relation
For index `i`, only earlier elements `j < i` with `nums[j] < nums[i]` can be extended by `nums[i]` (must stay strictly increasing). For any such valid `j`, appending `nums[i]` to the subsequence ending at `j` gives length `dp(j) + 1`. Take the best among all valid `j`:

`dp(i) = max(dp(j) + 1) for all j in [0, i) where nums[i] > nums[j]`

**Worked trace:** at index 7 (value 5), checking index 5 (value 4, `dp[5] = 3`, meaning some increasing subsequence of length 3 ends there) — since `5 > 4`, appending gives length `4`. The actual *contents* of that subsequence don't matter, only its length.

## Part 3 — base case
Every single element is trivially an increasing subsequence of length `1` on its own.

## Final answer
Since `dp(i)` only captures subsequences **ending exactly at `i`**, the overall answer is the **maximum across all `dp(i)`** — not simply `dp(n-1)`, since the true LIS might end anywhere in the array.

## Top-down code
```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        @cache
        def dp(i):
            ans = 1 # Base case
            # Recurrence relation
            for j in range(i):
                if nums[i] > nums[j]:
                    ans = max(ans, dp(j) + 1)

            return ans
        return max(dp(i) for i in range(len(nums)))
```

## Bottom-up code
```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        dp = [1] * len(nums)
        for i in range(len(nums)):
            for j in range(i):
                if nums[i] > nums[j]:
                    dp[i] = max(dp[i], dp[j] + 1)
        return max(dp)
```

`dp[i]` computations naturally proceed left-to-right, so by the time index `i` is reached, every `dp[j]` for `j < i` has already been correctly computed — same ordering guarantee that made [[Dynamic Programming - House Robber Example|House Robber]]'s bottom-up loop work.

## Complexity
The nested loop makes this **O(n²) time** — work per state is **linear** (O(n)) here, not constant, unlike the earlier examples, and there are `n` states → O(n) × O(n) = O(n²). **Space: O(n)** for the `dp` array/memo — **cannot** be reduced the way [[Dynamic Programming - House Robber Example|House Robber's space was]], because the recurrence relation here is **not static**: it depends on *all* previous indices, not a fixed small number of them.

#dsa #algorithms #dynamic-programming

Related: [[Dynamic Programming - Framework]], [[Subsequences - Overview]], [[Dynamic Programming - House Robber Example]]
