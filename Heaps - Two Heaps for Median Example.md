# Heaps - Two Heaps for Median Example

⚠️ Using multiple heaps together is uncommon, and problems requiring it tend to be harder — similar difficulty tier to [[Monotonic Stacks and Queues - Overview|monotonic stacks/queues]]. Don't worry if this takes longer to click.

**Signal to watch for:** if a problem involves finding a **median**, think about two heaps.

## Problem: 295. Find Median from Data Stream
Implement `MedianFinder`: `addNum(num)` adds a number to a running dataset; `findMedian()` returns the median of everything added so far.

## The core idea: split the dataset into two heaps
- A **min heap** storing the **greater half** of the data — its top (minimum of the greater half) sits right at the middle from above.
- A **max heap** storing the **lesser half** of the data — its top (maximum of the lesser half) sits right at the middle from below.

Visualize the sorted dataset as an array split into a "left half" (max heap) and "right half" (min heap) — the two heap tops "touch" at the middle.

## Maintaining balance
Keep both heaps' sizes equal (or off by exactly 1, for an odd total count). With an even count, the median is the **average** of both heap tops. With an odd count, the median is whichever single element sits in the heap with the extra element — arbitrarily chosen here to always be the **max heap**.

**Required invariant:** every element in the min heap must be `≥` every element in the max heap (otherwise the "left half / right half" picture breaks).

## The 3-step insertion algorithm
1. Push `num` onto the max heap (the arbitrarily-chosen "extra element" heap).
2. Pop the max heap's top, and push that value onto the min heap.
3. If the min heap now has *more* elements than the max heap, pop the min heap's top and push it back onto the max heap.

**Why step 2 matters:** it enforces the "min heap ≥ max heap" invariant. Example: dataset `{1, 3, 7, 13, 36, 100}`, adding `50`. Step 1 puts `50` into the max heap (`{50, 7, 3, 1}`) — but `50` doesn't actually belong there, since the min heap already holds smaller values (`13`, `36`). Popping the max heap's new top (`50`) and pushing it to the min heap fixes this — `50` correctly ends up on the "greater half" side.

**Why step 3 matters:** maintains the arbitrary rule that the max heap holds the extra element when the total count is odd — after step 2, sizes might briefly favor the min heap, and step 3 corrects that by shifting the smallest element of the min heap back over.

**Visualizing the shift:** popping from one heap and pushing the result to the other is like sliding the "where the colors change" boundary in the sorted-array mental picture over by exactly one element.

## Code
```python
import heapq

class MedianFinder:
    def __init__(self):
        self.min_heap = []
        self.max_heap = []

    def addNum(self, num: int) -> None:
        heapq.heappush(self.max_heap, -num)
        heapq.heappush(self.min_heap, -heapq.heappop(self.max_heap))
        if len(self.min_heap) > len(self.max_heap):
            heapq.heappush(self.max_heap, -heapq.heappop(self.min_heap))

    def findMedian(self) -> float:
        if len(self.max_heap) > len(self.min_heap):
            return -self.max_heap[0]
        return (self.min_heap[0] - self.max_heap[0]) / 2
```

`max_heap` stores negated values (Python's min-heap-only simulation trick, per [[Heaps - Overview]]), so `-self.max_heap[0]` un-negates to get the actual max-heap-side value.

## Complexity
`findMedian`: **O(1)** — just reading heap tops. `addNum`: **O(log n)** — a constant number of heap pushes/pops, where `n` = total elements added so far. **Space: O(n)** to store both heaps combined.

## Bigger picture: heaps as a tool, not the whole problem
Unlike [[Trees and Graphs - Nodes, Vertices, and Edges|trees/graphs]] or [[Linked Lists - Overview|linked lists]], problems using heaps are rarely *about* the heap itself — the heap is usually a means to an end, similar to how [[Hashing - Hash Maps|hash maps]] get used. Expect heaps to reappear as a supporting tool in later chapters (e.g. Greedy).

#dsa #algorithms #heaps

Related: [[Heaps - Overview]], [[Heaps - Last Stone Weight Example]]
