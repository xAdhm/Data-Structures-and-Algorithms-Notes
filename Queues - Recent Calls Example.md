# Queues - Recent Calls Example

## Problem: 933. Number of Recent Calls
Implement `RecentCounter` with `ping(t)`: records a call at time `t`, and returns the count of calls within `[t - 3000, t]`. Calls to `ping` arrive with strictly increasing `t`.

## Why a queue fits
This is a stream of increasing integers where we need to know how many recent values fall within a 3000-unit window.

**Brute force:** store every call in an array, and on each `ping`, iterate the whole array to count values within range — inefficient, since once a value `x` becomes older than `3000` units, *every future call* would still have to scan past it, even though we already know it can never count again.

**Better:** discard outdated values as soon as they age out, instead of repeatedly re-checking them.

**Why not just a dynamic array with front-removal?** Removing from the front of a dynamic array is **O(n)** (see [[Arrays and Strings - Time Complexity of Operations]]). Using an efficient [[Queues - Overview|queue]] instead makes that removal **O(1)**.

## Approach
1. Maintain a queue of timestamps.
2. Since `t` values arrive in increasing order, the queue is always naturally sorted — the **front** of the queue is always the **oldest** call.
3. On each `ping(t)`: repeatedly remove (dequeue) from the front while the front value is older than `t - 3000`.
4. Add (enqueue) the current `t`.
5. Return the queue's current length — that's the count of calls still within the valid window.

## Code
```python
from collections import deque

class RecentCounter:
    def __init__(self):
        self.queue = deque()

    def ping(self, t: int) -> int:
        while self.queue and self.queue[0] < t - 3000:
            self.queue.popleft()

        self.queue.append(t)
        return len(self.queue)

# Your RecentCounter object will be instantiated and called as such:
# obj = RecentCounter()
# param_1 = obj.ping(t)
```

Python's `collections.deque` supports O(1) removal from the front (`popleft()`), making it the natural fit here (see [[Queues - Overview]]).

## Complexity
Each timestamp is enqueued exactly once and dequeued at most once — so across all `ping` calls, total work is bounded by the number of calls made. **Amortized O(1) per call** (same amortized reasoning style as [[Sliding Window - Why It's Efficient]]), despite the `while` loop inside each call.

#dsa #algorithms #queues

Related: [[Queues - Overview]], [[Sliding Window - Why It's Efficient]]
