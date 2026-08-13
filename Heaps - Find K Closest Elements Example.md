# Heaps - Find K Closest Elements Example

## Problem: 658. Find K Closest Elements
Given sorted array `arr`, integers `k` and `x`, return the `k` integers closest to `x`, sorted ascending. Ties broken by preferring the **smaller** element.

## Adapting the Top K pattern for "smallest wins"
[[Heaps - Top K Frequent Elements Example|The frequent-elements example]] wanted **maximum** frequencies, so a **min heap** was used (pops remove the smaller/worse elements, leaving the best behind). Here we want **minimum** differences — the "best" element is the one *closest* to `x` — so flip to a **max heap**: pops then remove the *largest* difference (the worst candidate), leaving the closest elements behind. See [[Heaps - Top K Pattern]] for the general shape.

## Handling the tie-break rule
Ties (equal distance) should favor the smaller number. Example: `x = 5`, candidates `3` and `7` — both distance `2`, but `3` should be considered "better."

**Trick (Python/C++):** push an ordered tuple `(distance, value)` — heap comparison checks the first element, and only falls through to the second element to break ties. Since we're using a **max heap** (via negation, per [[Heaps - Overview]]'s trick), negate **both** values in the tuple: `(-distance, -value)`. When distances tie, comparing `-value` correctly makes the *more negative* value (i.e. the larger original number) "bigger" in heap-order — meaning it gets popped first, correctly leaving the smaller number behind.

**Other languages (e.g. Java):** typically require an explicit custom comparator function to define this same tie-breaking logic manually.

## Code
```python
import heapq

class Solution:
    def findClosestElements(self, arr: List[int], k: int, x: int) -> List[int]:
        heap = []

        for num in arr:
            distance = abs(x - num)
            heapq.heappush(heap, (-distance, -num))
            if len(heap) > k:
                heapq.heappop(heap)

        return sorted([-pair[1] for pair in heap])
```

Final result needs an explicit `sorted(...)` call — unlike the frequent-elements example, this problem requires the output in ascending order, and a heap's internal order isn't guaranteed to already be sorted once popped selectively like this.

## Complexity
**O((n + k) log k) time** — main loop is `n` iterations of O(log k) heap work (heap capped at size `k`), plus a final O(k log k) sort of the `k`-sized output.

**Practical note:** this approach doesn't exploit the fact that `arr` is already sorted (a faster, more specialized algorithm exists that does) — it's presented here specifically to demonstrate the general heap-based top-k pattern, not as the fastest possible solution to this specific problem. Still faster than the naive "sort everything with a custom comparator" approach.

#dsa #algorithms #heaps

Related: [[Heaps - Top K Pattern]], [[Heaps - Top K Frequent Elements Example]]
