# Hashing - Subarray Sum Equals K Example

Worked LeetCode example applying [[Hashing - Subarray Sum Equals K (Exact Constraint Pattern)]].

## Problem: 560. Subarray Sum Equals K
Given integer array `nums` and integer `k`, find the number of subarrays whose sum equals `k`.

Example: `nums = [1, 2, 1, 2, 1]`, `k = 3` → answer is 4 (`[1,2]` twice, `[2,1]` twice).

Prefix sums for this input: `[1, 3, 4, 6, 7]`. Differences equal to 3: `(4-1)`, `(6-3)`, `(7-4)` — only 3 found this way, but the answer is 4. **Why?** Because `counts[0] = 1` must be initialized for the empty prefix — without it, a subarray that itself sums to exactly `k` starting from index 0 wouldn't be counted (its needed `curr - k = 0` wouldn't exist in the map).

## Code
```python
from collections import defaultdict

class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        counts = defaultdict(int)
        counts[0] = 1
        ans = curr = 0

        for num in nums:
            curr += num
            ans += counts[curr - k]
            counts[curr] += 1

        return ans
```

## Why a hash map is needed, not just a set
Since `nums` can contain negative numbers (constraint: `-1000 <= nums[i] <= 1000`), `curr` doesn't strictly increase — the same prefix sum value can occur more than once, so frequency actually matters.

**Illustrating example:** `nums = [1, -1, 1, -1]`, `k = 0` → 4 valid subarrays: `[1,-1]` (twice), `[-1,1]` (once), and the whole array.
Prefix sums: `[1, 0, 1, 0]`. Because `counts[0]` starts at 1 (empty prefix) and gets incremented again after index 1 (`curr = 0` again), by the time you reach the final index, `counts[0] = 2` — meaning `ans += counts[curr - k]` at that point adds **2** to the answer at once, correctly capturing both subarrays ending there.

If all numbers were positive, `curr` would strictly increase, so no prefix sum could repeat — a set would suffice in that special case. But because non-positive numbers are allowed generally, a hash map (tracking frequency) is necessary.

## Complexity
**O(n) time and O(n) space**, where `n = len(nums)` — constant work per iteration; the hash map can grow to at most `n` distinct prefix sums.

#dsa #algorithms #hashing #hash-map #prefix-sum #counting

Related: [[Hashing - Subarray Sum Equals K (Exact Constraint Pattern)]], [[Hashing - Nice Subarrays (Odd Count) Example]]
