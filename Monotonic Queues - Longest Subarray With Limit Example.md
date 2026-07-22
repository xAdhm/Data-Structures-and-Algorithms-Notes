# Monotonic Queues - Longest Subarray With Limit Example

## Problem: 1438. Longest Continuous Subarray With Absolute Diff Less Than or Equal to Limit
Given `nums` and `limit`, find the length of the longest subarray where `max - min <= limit` for any two elements within it.

## Recognizing the pattern
"Max element minus min element" is the constraint metric; the restriction is `<= limit`. Longest-subarray-with-a-constraint is the classic [[Sliding Window - Overview|sliding window]] signal (see [[Subarrays and Substrings - Recognizing Patterns]]).

The twist: this window needs to track **both** the max *and* the min efficiently as the window changes — building directly on [[Monotonic Queues - Sliding Window Maximum Example]].

## Approach
Use **two monotonic deques**:
- A monotonically **increasing** deque → its front is always the current window's **minimum**
- A monotonically **decreasing** deque → its front is always the current window's **maximum** (same idea as the previous example)

Then run the standard sliding window template from [[Sliding Window - Dynamic Window Size]]: expand `right`, and shrink from `left` whenever the constraint (`max - min > limit`) is violated — while keeping both deques properly maintained (removing violating elements, and evicting anything that's fallen out of the window on the left).

## Code
```python
from collections import deque

class Solution:
    def longestSubarray(self, nums: List[int], limit: int) -> int:
        increasing = deque()
        decreasing = deque()
        left = ans = 0

        for right in range(len(nums)):
            # maintain the monotonic deques
            while increasing and increasing[-1] > nums[right]:
                increasing.pop()
            while decreasing and decreasing[-1] < nums[right]:
                decreasing.pop()

            increasing.append(nums[right])
            decreasing.append(nums[right])

            # maintain window property
            while decreasing[0] - increasing[0] > limit:
                if nums[left] == decreasing[0]:
                    decreasing.popleft()
                if nums[left] == increasing[0]:
                    increasing.popleft()
                left += 1

            ans = max(ans, right - left + 1)
        return ans
```

**Note:** here the deques store actual **values** (not indices, unlike [[Monotonic Queues - Sliding Window Maximum Example]]) — since the eviction check compares `nums[left]` directly against the deque's front value, rather than checking index bounds against a fixed window size `k`. This works because the sliding window's `left`/`right` bounds themselves — not a fixed `k` — define the window here.

Window length formula, as always: `right - left + 1`.

## Complexity
**O(n) time and O(n) space** — each for-loop iteration is amortized O(1) (values enter and leave each deque at most once overall, same amortized argument as [[Sliding Window - Why It's Efficient]]), and each deque can grow up to size `n` in the worst case.

#dsa #algorithms #queues #monotonic #sliding-window

Related: [[Monotonic Stacks and Queues - Overview]], [[Monotonic Queues - Sliding Window Maximum Example]], [[Sliding Window - Dynamic Window Size]]
