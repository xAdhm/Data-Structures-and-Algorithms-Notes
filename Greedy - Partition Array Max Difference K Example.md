# Greedy - Partition Array Max Difference K Example

## Problem: 2294. Partition Array Such That Maximum Difference Is K
Given `nums` and `k`, split into subsequences where each subsequence's max and min are within `k` of each other. Find the minimum number of subsequences needed.

Example: `nums = [3, 6, 1, 2, 5]`, `k = 2` → answer `2` (groups `[3,1,2]` and `[6,5]`).

## Subsequence, but order doesn't matter → treat as subset
Recall [[Subsequences - Overview|subsequences]] preserve relative order, while [[Subsets - Overview|subsets]] don't. Here, only the **max and min** of each group matter — order within a group is irrelevant. So this problem is effectively about **subsets**, not true subsequences, which means (per [[Subsets - Overview]]) **sorting the input is safe** — nothing about the "subsequence" framing is lost by reordering, since only max/min values matter, not positions.

## Establishing the greedy strategy
Start with the smallest remaining number `x`. Should the group include every element in range `[x, x+k]`? **Yes.** Suppose you excluded some element within that range (say `x + k - 1`) — the next group would then have to start at an even smaller number than it otherwise would have, which only **shrinks** the range available to future groups. Excluding anything reachable from `x` never helps and can only hurt.

**Confirming via case analysis:** whether you include just `x`, `x` and one more, or `x` and two more (up to the `k` boundary), the answer increments by exactly `1` in every case — so you might as well take the case that leaves the *smallest* remaining problem (i.e., take as many as possible), since a smaller remaining problem can only help minimize future groups. (This isn't a full formal proof, but is a sufficient explanation for an interview — same caveat repeated throughout the [[Greedy Algorithms - Overview|greedy chapter]].)

## Approach
Sort ascending. Track `x` = the start of the current group. Walk through the array — while an element is within `x + k`, it joins the current group implicitly; once an element exceeds `x + k`, start a new group (`x` = that element, increment answer).

## Code
```python
class Solution:
    def partitionArray(self, nums: List[int], k: int) -> int:
        nums.sort()
        ans = 1
        x = nums[0]

        for i in range(1, len(nums)):
            if nums[i] - x > k:
                x = nums[i]
                ans += 1

        return ans
```

## Complexity
**O(n log n) time** — dominated by the sort. **Space:** depends on the sorting algorithm, same as [[Greedy - Destroying Asteroids Example]].

#dsa #algorithms #greedy

Related: [[Greedy Algorithms - Overview]], [[Subsets - Overview]], [[Subsequences - Overview]]
