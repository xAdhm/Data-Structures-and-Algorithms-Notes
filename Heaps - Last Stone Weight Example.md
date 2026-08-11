# Heaps - Last Stone Weight Example

## Problem: 1046. Last Stone Weight
Given stone weights, repeatedly smash the two heaviest together: if equal, both destroyed; if not, the lighter's weight is subtracted from the heavier (which survives, reduced). Return the final remaining stone's weight, or `0` if none remain.

## Why sorting doesn't work
The naive idea — sort descending, process in order — breaks because smashing often produces a **new** stone (the reduced survivor) that needs to be re-inserted into consideration, not just consumed and discarded.

## Why a heap fits
This is exactly the [[Heaps - Overview|"repeatedly find the max"]] use case. Put all stones into a **max heap**: pop the top two in O(log n) each, apply the smash rule, and push any survivor back in O(log n). Repeat until ≤1 stone remains.

## Code
```python
import heapq

class Solution:
    def lastStoneWeight(self, stones: List[int]) -> int:
        stones = [-stone for stone in stones]
        heapq.heapify(stones) # turns an array into a heap in linear time
        while len(stones) > 1:
            first = abs(heapq.heappop(stones))
            second = abs(heapq.heappop(stones))
            if first != second:
                heapq.heappush(stones, -abs(first - second))
        return -stones[0] if stones else 0
```

**Python-specific trick:** since `heapq` only implements min heaps (see [[Heaps - Overview]]), negate every value on the way in (and take `abs`/negate again on the way out) to simulate a max heap.

## Complexity
Each smash destroys at least one stone, so there are at most `n` iterations. Each iteration does a constant number of heap pops/pushes, each O(log n) → **O(n log n) time**. **O(n) space** for the heap — note: since Python reuses/mutates the input list in-place here, this technically counts toward space complexity (normally input space isn't counted, but an in-place transformation like this is an exception worth calling out).

#dsa #algorithms #heaps

Related: [[Heaps - Overview]], [[Heaps - Minimum Operations to Halve Array Sum Example]]
