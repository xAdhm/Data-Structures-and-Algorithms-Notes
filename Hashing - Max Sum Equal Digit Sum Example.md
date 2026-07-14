# Hashing - Max Sum Equal Digit Sum Example

## Problem: 2342. Max Sum of a Pair With Equal Sum of Digits
Given integer array `nums`, find `max(nums[i] + nums[j])` where `nums[i]` and `nums[j]` have the same digit sum. Return `-1` if no such pair exists.

## Same identifier trick as Group Anagrams
Directly parallels [[Hashing - Group Anagrams Example]]: there, strings were grouped by their sorted form (the identifier). Here, numbers are grouped by their **digit sum** (the identifier). Numbers sharing a digit sum go in the same group; within each group with ≥2 elements, we just need the top 2 values.

## Digit sum helper
```python
def get_digit_sum(num):
    digit_sum = 0
    while num:
        digit_sum += num % 10
        num //= 10

    return digit_sum
```

## Approach 1: store all numbers per digit-sum group, then sort
```python
from collections import defaultdict

class Solution:
    def maximumSum(self, nums: List[int]) -> int:
        def get_digit_sum(num):
            digit_sum = 0
            while num:
                digit_sum += num % 10
                num //= 10
            return digit_sum

        dic = defaultdict(list)
        for num in nums:
            digit_sum = get_digit_sum(num)
            dic[digit_sum].append(num)

        ans = -1
        for key in dic:
            curr = dic[key]
            if len(curr) > 1:
                curr.sort(reverse=True)
                ans = max(ans, curr[0] + curr[1])

        return ans
```

**Complexity:** sorting each group is wasteful — in the worst case (every number shares the same digit sum), this costs **O(n log n)**, where `n = len(nums)`.

## Approach 2 (optimized): only track the largest value seen per digit sum
Just like [[Hashing - Minimum Card Pickup Example]]'s optimization, we don't need the *whole group* — only the current maximum for each digit-sum key. When a new number arrives with a digit sum already seen, we immediately have a valid candidate pair (`current num + stored max`), and then update the stored max if needed.

```python
from collections import defaultdict

class Solution:
    def maximumSum(self, nums: List[int]) -> int:
        def get_digit_sum(num):
            digit_sum = 0
            while num:
                digit_sum += num % 10
                num //= 10
            return digit_sum

        dic = defaultdict(int)
        ans = -1
        for num in nums:
            digit_sum = get_digit_sum(num)
            if digit_sum in dic:
                ans = max(ans, num + dic[digit_sum])
            dic[digit_sum] = max(dic[digit_sum], num)
        return ans
```

**Complexity:** **O(n)** time — no sorting needed, single pass. Space also improves on average (each key stores a single integer instead of a growing list), same reasoning as the card-pickup optimization.

## Pattern takeaway
This is the same "identifier grouping" pattern as Group Anagrams, combined with the same "track only what you need (max/latest), not the full history" optimization from [[Hashing - Minimum Card Pickup Example]]. Recognizing when a hash map's *values* can shrink from a list to a single running value (max, count, most-recent-index, etc.) is a recurring space/time win.

#dsa #algorithms #hashing #hash-map

Related: [[Hashing - Group Anagrams Example]], [[Hashing - Minimum Card Pickup Example]]
