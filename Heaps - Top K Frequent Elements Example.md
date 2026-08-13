# Heaps - Top K Frequent Elements Example

## Problem: 347. Top K Frequent Elements
Given `nums` and `k`, return the `k` most frequent elements (answer guaranteed unique).

## Approach
Applies the [[Heaps - Top K Pattern]] directly:
1. Count frequencies with a hash map (see [[Hashing - Counting Overview]]).
2. Min heap, pushing `(frequency, element)` pairs — frequency listed **first** in the tuple so the heap orders by frequency (Python/tuple comparison checks the first element first).
3. Whenever the heap exceeds size `k`, pop — this removes whichever pair has the **lowest** frequency, since it's a min heap.
4. After processing every element, the heap holds exactly the `k` most frequent elements.

## Code
```python
from collections import Counter
import heapq

class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        counts = Counter(nums)
        heap = []

        for key, val in counts.items():
            heapq.heappush(heap, (val, key))
            if len(heap) > k:
                heapq.heappop(heap)

        return [pair[1] for pair in heap]
```

## Complexity
Let `n = len(nums)`. Building `counts` is O(n) (dominated by the main loop). Main loop: `n` iterations, each doing O(log k) heap work (heap size capped at `k`) → **O(n log k) time**. **Space: O(n + k)** — the hash map (O(n)) and the heap (O(k)).

#dsa #algorithms #heaps #hashing

Related: [[Heaps - Top K Pattern]], [[Heaps - Find K Closest Elements Example]], [[Hashing - Counting Overview]]
