# Intervals - Overview and Meeting Rooms Example

**Intervals** `[start, end]` are another common problem shape. General strategy: **sort the input**, then iterate while comparing **adjacent** intervals.

## Problem: 252. Meeting Rooms
Given `intervals[i] = [start, end)`, determine if one person could attend every meeting (no overlaps).

Example: `[[0,30],[5,10],[15,20]]` → `false` (attending `[0,30]` blocks the other two).

## Why brute force is wasteful
Checking every **pair** of meetings for overlap costs **O(n²)**.

## The key insight
**If a conflict exists, sorting by start time makes the conflicting meetings adjacent.** So instead of comparing every pair, sort first, then only ever need to compare each meeting to the **one right before it**.

## Approach
Sort by start time — this puts meetings in the order they'd actually be attended. Walk through consecutive pairs: if meeting `i` starts **before** meeting `i-1` ends, there's a conflict (you'd need to leave meeting `i-1` early) — return `False`. If the scan completes with no conflicts, return `True`.

## Complexity
**O(n log n) time**, dominated by the sort — a solid improvement over the O(n²) brute force. **Space:** depends on the sorting algorithm used by the language (e.g. Python's Timsort: up to O(n); a quicksort-based language: O(log n)) — same caveat noted throughout the [[Greedy Algorithms - Overview|greedy chapter]] examples.

See [[Intervals - Merge Intervals Example]] for the natural follow-up problem using the same sort-then-scan-adjacent-pairs shape.

#dsa #algorithms #intervals

Related: [[Intervals - Merge Intervals Example]], [[Greedy Algorithms - Overview]]
