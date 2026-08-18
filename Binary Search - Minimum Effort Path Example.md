# Binary Search - Minimum Effort Path Example

## Problem: 1631. Path With Minimum Effort
`m x n` grid `heights`. Moving between adjacent cells costs the absolute height difference; a path's "effort" is the **largest** single-step difference along it. Find the minimum possible effort to get from top-left to bottom-right.

## Establishing the two zones
If a path exists using max-allowed-difference `effort`, the same path is still valid for any `effort' > effort` (a looser constraint can't break an already-valid path). If no path exists at `effort`, none can exist at any smaller `effort` either (an even tighter constraint only removes options). Two-zone structure confirmed, seeking a **minimum** — see [[Binary Search - On Solution Spaces]].

## Search space bounds
- **Minimum possible:** `0` — a path could exist where every step has zero height difference.
- **Maximum possible:** the largest value in `heights` — since all values are non-negative, no actual difference between any two cells can exceed this.

## The `check` function: graph traversal
For a given `effort`, treat the grid as an [[Graphs - Input Formats|implicit grid graph]] (same setup as [[Graphs - Shortest Path in Binary Matrix Example]]) and run [[Binary Trees - DFS Overview|DFS]] from `(0,0)`, only traversing to a neighbor if the height difference is `≤ effort`. Return whether `(m-1, n-1)` is reachable.

## Code
```python
class Solution:
    def minimumEffortPath(self, heights: List[List[int]]) -> int:
        def valid(row, col):
            return 0 <= row < m and 0 <= col < n

        def check(effort):
            directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]
            seen = {(0, 0)}
            stack = [(0, 0)]

            while stack:
                row, col = stack.pop()
                if (row, col) == (m - 1, n - 1):
                    return True

                for dx, dy in directions:
                    next_row, next_col = row + dy, col + dx
                    if valid(next_row, next_col) and (next_row, next_col) not in seen:
                        if abs(heights[next_row][next_col] - heights[row][col]) <= effort:
                            seen.add((next_row, next_col))
                            stack.append((next_row, next_col))

            return False

        m = len(heights)
        n = len(heights[0])
        left = 0
        right = max(max(row) for row in heights)
        while left <= right:
            mid = (left + right) // 2
            if check(mid):
                right = mid - 1
            else:
                left = mid + 1

        return left
```

## Why this combines two chapters
A clean example of binary search using a **greedy-adjacent graph check** as its verification step — the outer structure is [[Binary Search - On Solution Spaces|binary search on a solution space]], but the inner `check` function is a full [[Graphs - DFS Complexity|graph DFS]]. Recognizing that a "verify feasibility for x" function can itself be an entire graph traversal (not just a simple loop) is the main new idea here.

## Complexity
DFS (`check`) costs **O(m·n)**. Binary search runs it **O(log k)** times, where `k` = max height value. **Total: O(m·n·log k) time.** **Space: O(m·n)** for the DFS stack/`seen` set.

#dsa #algorithms #binary-search #graphs

Related: [[Binary Search - On Solution Spaces]], [[Graphs - Shortest Path in Binary Matrix Example]], [[Binary Search - Min vs Max Answer Implementation]]
