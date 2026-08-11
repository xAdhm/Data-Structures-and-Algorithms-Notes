# Heaps - Minimum Operations to Halve Array Sum Example

## Problem: 2208. Minimum Operations to Halve Array Sum
Given positive integers `nums`, one operation halves any chosen element. Return the minimum operations needed to reduce the total sum by at least half.

## Greedy insight: always halve the current largest element
To minimize the number of operations, each operation should reduce the sum by as much as possible — which means always halving whichever element is **currently largest**. (This greedy choice is explored more formally in the upcoming Greedy chapter, per the source article.)

## Why a heap fits
Same [[Heaps - Overview|"repeatedly find the max"]] pattern as [[Heaps - Last Stone Weight Example]] — and again, sorting once up front doesn't work, since halved elements get **re-inserted** and may still be the largest (or need to be halved again later).

## Approach
- Convert `nums` into a max heap.
- `target` = half the original sum — the amount still needing to be cut.
- While `target > 0`: pop the max element `x`, subtract `x/2` from `target`, push `x/2` back onto the heap (the halved value re-enters the pool of candidates).
- Count iterations.

## Code
```python
import heapq

class Solution:
    def halveArray(self, nums: List[int]) -> int:
        target = sum(nums) / 2
        heap = [-num for num in nums]
        heapq.heapify(heap)

        ans = 0
        while target > 0:
            ans += 1
            x = heapq.heappop(heap)
            target += x / 2
            heapq.heappush(heap, x / 2)

        return ans
```

**Note:** `x` here is already negative (max-heap simulation), so `target += x / 2` (adding a negative) is equivalent to *subtracting* `|x|/2` from `target` — same negation trick as [[Heaps - Last Stone Weight Example]].

## Complexity
Each heap operation (pop/push) costs O(log n). **Why the total number of operations is bounded by O(n):** even in the worst case, you could always achieve the target by halving every element in `nums` at least once — so the loop can't run more than roughly `n` times' worth of "large enough" reductions before the target is met. This gives **O(n log n) time** overall. **O(n) space** for the heap.

#dsa #algorithms #heaps

Related: [[Heaps - Overview]], [[Heaps - Last Stone Weight Example]]
