# Binary Search - Koko Eating Bananas Example

## Problem: 875. Koko Eating Bananas
`n` piles of bananas. Koko eats at a fixed speed `k` bananas/hour from one pile per hour (finishing a pile early wastes the rest of that hour). Find the minimum `k` such that all piles are finished within `h` hours.

## Establishing the two zones
If speed `k` works, any speed `> k` also works (faster is never worse). If `k` doesn't work, no speed `< k` will either. This is exactly the [[Binary Search - On Solution Spaces|two-zone structure]] needed for binary-search-on-answer, looking for a **minimum**.

## Search space bounds
- **Minimum possible:** `1` — speed must be a positive integer (0 means never eating).
- **Maximum possible:** `max(piles)` — no benefit going faster than the largest single pile, since each pile takes at least 1 hour regardless of how much faster than its own size the speed is.

## The `check` function
For a given speed `k`, how long does one pile of `bananas` take? `ceil(bananas / k)` — any partial hour still costs a full hour (even 1 leftover banana costs an extra hour). Sum this across all piles and compare against `h`.

## Code
```python
class Solution:
    def minEatingSpeed(self, piles: List[int], h: int) -> int:
        def check(k):
            hours = 0
            for bananas in piles:
                hours += ceil(bananas / k)

            return hours <= h

        left = 1
        right = max(piles)
        while left <= right:
            mid = (left + right) // 2
            if check(mid):
                right = mid - 1
            else:
                left = mid + 1
        return left
```

Returns `left` because this problem seeks a **minimum** — see [[Binary Search - Min vs Max Answer Implementation]] for why.

## Complexity
`check` costs **O(n)**, where `n = len(piles)`. Binary search runs **O(log k)** times, where `k = max(piles)`. **Total: O(n log k) time.** **O(1) space** beyond a few integer variables.

#dsa #algorithms #binary-search #greedy

Related: [[Binary Search - On Solution Spaces]], [[Binary Search - Min vs Max Answer Implementation]]
