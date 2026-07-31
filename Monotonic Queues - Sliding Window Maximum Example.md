# Monotonic Queues - Sliding Window Maximum Example

⚠️ Significantly harder than most problems covered so far — a good demonstration of how powerful a deque can be, but expect to revisit this.

## Problem: 239. Sliding Window Maximum
Given `nums` and window size `k`, find the maximum element in each window as it slides from left to right across the array.

Example: `nums = [1, 3, -1, -3, 5, 3, 6, 7]`, `k = 3` → `[3, 3, 5, 5, 6, 7]`

## The hard part
Tracking the max of the *current* window is easy while building it — but when the max **leaves** the window, how do you efficiently know the new max without rescanning?

## Key insight
Once we see a number, any **smaller** number currently in the window becomes permanently useless — the new number arrived later (won't be removed from the window before the smaller ones) and is larger, so the smaller ones can never become the max again while this new number is still in play.

This means we want a **monotonically decreasing** structure — remove anything smaller than an incoming element before adding it (same maintenance idea as [[Monotonic Stacks - Daily Temperatures Example]]).

## Why a deque, not a stack or plain queue
- The problem is a sliding window: elements enter on the right, leave on the left → suggests a [[Queues - Overview|queue]] (opposite-end operations).
- But maintaining the monotonic property requires removing smaller elements **from the right** before adding new ones (like a stack operation).
- Needing efficient operations at **both ends** → a **deque** (double-ended queue) is the right structure.

Store **indices**, not values — this lets us detect when the front element has fallen outside the current window (`index < right - k + 1`, i.e. `front_index + k == current_index`).

## Approach
1. Maintain a monotonically decreasing deque of indices.
2. For each new index `i`: while the deque's back holds a value smaller than `nums[i]`, pop it (from the right) — it can never be the max again.
3. Append `i` to the deque.
4. If the deque's front index has fallen outside the window (`front + k == i`), pop it from the front.
5. Once the window has reached size `k` (i.e. `i >= k - 1`), the front of the deque is the max for the current window — append it to the answer.

## Code
```python
from collections import deque

class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        ans = []
        queue = deque()
        for i in range(len(nums)):
            # maintain monotonic decreasing.
            # all elements in the deque smaller than the current one
            # have no chance of being the maximum, so get rid of them
            while queue and nums[i] > nums[queue[-1]]:
                queue.pop()
            queue.append(i)
            # queue[0] is the index of the maximum element.
            # if queue[0] + k == i, then it is outside the window
            if queue[0] + k == i:
                queue.popleft()

            # only add to the answer once our window has reached size k
            if i >= k - 1:
                ans.append(nums[queue[0]])
        return ans
```

## Summary
- Monotonic decreasing deque → first element is always the current window's max
- When the max index falls out of the window, remove it from the front — the next-largest element (already correctly ordered behind it) takes over position 0
- To maintain decreasing order, pop smaller trailing elements from the back before appending new ones

## Complexity
**O(n) time** (each index pushed once, popped at most once — amortized O(1) per iteration, same reasoning as [[Monotonic Stacks and Queues - Overview]]), **O(k) space** — the deque can never hold more than `k` elements, since anything outside the window gets evicted.

#dsa #algorithms #queues #monotonic

Related: [[Monotonic Stacks and Queues - Overview]], [[Queues - Overview]], [[Monotonic Queues - Longest Subarray With Limit Example]]
