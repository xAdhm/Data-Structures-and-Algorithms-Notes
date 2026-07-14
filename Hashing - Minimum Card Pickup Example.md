# Hashing - Minimum Card Pickup Example

## Problem: 2260. Minimum Consecutive Cards to Pick Up
Given integer array `cards`, find the length of the shortest subarray containing at least one duplicate. Return `-1` if there are no duplicates.

(Solvable with sliding window too, but this note focuses on the hash-map-centric approach.)

## Reframing the problem
The shortest subarray containing a duplicate must have the **duplicate pair as its first and last elements** — any extra elements at the edges could be trimmed off for free without breaking the "contains a duplicate" property, so they'd never appear in the *shortest* answer.

This means the problem reduces to: **what is the shortest distance between any two occurrences of the same element?**

## Approach 1: store all indices per value
Iterate once, recording every index each value appears at in a hash map (`value → list of indices`, naturally sorted ascending since we iterate left to right). Then for each value with multiple occurrences, check adjacent pairs of indices (since the list is sorted, only adjacent pairs can be the minimum gap) to find the smallest distance.

```python
from collections import defaultdict

class Solution:
    def minimumCardPickup(self, cards: List[int]) -> int:
        dic = defaultdict(list)
        for i in range(len(cards)):
            dic[cards[i]].append(i)

        ans = float("inf")
        for key in dic:
            arr = dic[key]
            for i in range(len(arr) - 1):
                ans = min(ans, arr[i + 1] - arr[i] + 1)

        return ans if ans < float("inf") else -1
```

**Complexity:** despite the nested loop, this is still **O(n)** time — the inner loop's total iterations across the *entire* algorithm can't exceed `n`, since it's just iterating over all recorded indices exactly once, split across different keys (same amortized-analysis reasoning as [[Sliding Window - Why It's Efficient]]). Space: O(n) always, since every index gets stored.

## Approach 2 (optimized): only track the most recent index per value
You don't need the *entire* history of indices for each value — only the most recent one. As soon as you see a repeat, you can compute the gap immediately and then just overwrite the stored index with the current one.

```python
from collections import defaultdict

class Solution:
    def minimumCardPickup(self, cards: List[int]) -> int:
        dic = defaultdict(int)
        ans = float("inf")
        for i in range(len(cards)):
            if cards[i] in dic:
                ans = min(ans, i - dic[cards[i]] + 1)

            dic[cards[i]] = i
        return ans if ans < float("inf") else -1
```

**Complexity:** still O(n) time, but this version saves an entire extra pass (no separate loop needed to scan through stored indices afterward) and improves **average-case space**: instead of always storing every index (guaranteed O(n) space), it only ever stores one index per distinct value, so space is O(n) only in the worst case (e.g. no duplicates at all) rather than always.

## Pattern takeaway
Whenever a hash map's values are only ever needed *incrementally* or just the *most recent* one (rather than the full history), consider replacing "list of all occurrences" with "just the latest occurrence" — same idea used in [[Prefix Sum - Space Optimization]] to cut down space usage.

#dsa #algorithms #hashing #hash-map

Related: [[Hashing - Hash Maps]], [[Prefix Sum - Space Optimization]], [[Sliding Window - Overview]]
