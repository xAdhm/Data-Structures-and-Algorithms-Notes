# Hashing - Nice Subarrays (Odd Count) Example

Second worked example applying [[Hashing - Subarray Sum Equals K (Exact Constraint Pattern)]] — demonstrates that the pattern generalizes beyond literal sums to **any** exact-value constraint metric.

## Problem: 1248. Count Number of Nice Subarrays
Given an array of positive integers `nums` and integer `k`, find the number of subarrays containing exactly `k` odd numbers.

Example: `nums = [1, 1, 2, 1, 1]`, `k = 3` → answer is 2.

## Adapting the pattern
In [[Hashing - Subarray Sum Equals K Example]], the constraint metric was **sum**, and `curr` tracked prefix sum. Here, the constraint metric is **count of odd numbers**, so `curr` instead tracks the running count of odd numbers seen so far (the "prefix odd count").

Everything else about the pattern works identically: if `curr - k` has been seen before, the subarray between that point and the current index has exactly `k` odd numbers (`curr - (curr - k) = k`).

**Detecting odd numbers:** `x % 2 == 1` if `x` is odd, else `0`. So each step does `curr += num % 2` instead of `curr += num`.

## Code
```python
from collections import defaultdict

class Solution:
    def numberOfSubarrays(self, nums: List[int], k: int) -> int:
        counts = defaultdict(int)
        counts[0] = 1
        ans = curr = 0

        for num in nums:
            curr += num % 2
            ans += counts[curr - k]
            counts[curr] += 1

        return ans
```

Compare directly to the Subarray Sum Equals K code — the only difference is `curr += num % 2` instead of `curr += num`. Same template, different constraint metric. (Not every problem in this pattern will be *this* close in code, but they'll all follow the same structural shape.)

## Complexity
**O(n) time and O(n) space** — identical reasoning to [[Hashing - Subarray Sum Equals K Example]].

#dsa #algorithms #hashing #hash-map #prefix-sum #counting

Related: [[Hashing - Subarray Sum Equals K (Exact Constraint Pattern)]], [[Hashing - Subarray Sum Equals K Example]]
