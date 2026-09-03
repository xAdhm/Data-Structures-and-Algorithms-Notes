# Intervals - Merge Intervals Example

## Problem: 56. Merge Intervals
Given `intervals[i] = [start, end]`, merge all overlapping intervals and return the resulting non-overlapping set.

Example: `[[1,3],[2,6],[8,10],[15,18]]` → `[[1,6],[8,10],[15,18]]` (first two merge; the rest don't overlap).

## Reusing the pattern
Same [[Intervals - Overview and Meeting Rooms Example|sort-by-start-time, compare-adjacent]] approach as Meeting Rooms — but instead of just detecting overlap, this problem needs to actually **combine** overlapping intervals.

## The merge rule
If two intervals `[a, b]` and `[c, d]` overlap, the merged result is `[min(a, c), max(b, d)]`.

**Simplification from sorting:** since intervals are processed in **sorted start-time order**, the new interval's `start` is *never* smaller than the previous interval's `start` — meaning `min(a, c)` is always just `a` (the earlier one, already fixed). Only the **end** needs an actual comparison: `max(b, d)`.

## Approach
Sort by start time. Build the answer array one interval at a time: for each new interval, if its `start` is `≤` the current last answer interval's `end`, they overlap — merge by updating that last interval's `end` to `max(existing_end, new_end)`. Otherwise, append the new interval as its own separate entry.

## Complexity
**O(n log n) time**, same as [[Intervals - Overview and Meeting Rooms Example|Meeting Rooms]] — dominated by the sort. **Space:** same sort-implementation-dependent caveat, not counting the output array itself.

#dsa #algorithms #intervals

Related: [[Intervals - Overview and Meeting Rooms Example]], [[Greedy Algorithms - Overview]]
