# Graphs - Shortest Path in Binary Matrix Example

## Problem: 1091. Shortest Path in Binary Matrix
Given an `n x n` binary matrix, find the shortest "clear path" (all `0`s) from top-left `(0,0)` to bottom-right `(n-1, n-1)`, moving in any of the 8 directions (including diagonals). Return `-1` if no such path exists.

## Why DFS can give the wrong answer here
This is an [[Graphs - Input Formats|implicit matrix graph]] — each `0` cell is a node, edges connect to up to 8 adjacent cells. Since we only visit each square once (to avoid cycles and redundant work — see [[Graphs - DFS Implementation Differences from Trees]]), a DFS might commit to a longer path first, "using up" squares that the truly optimal path also needed, and produce an incorrect (too long) answer. **Only [[Graphs - BFS Overview|BFS]] guarantees the shortest path.**

## Approach
Standard [[Graphs - BFS Overview|BFS]] shortest-path template: associate a `steps` count with each queue entry. The first time we dequeue the bottom-right cell, its `steps` value is guaranteed to be the shortest path length (per BFS's core guarantee).

## Code
```python
from collections import deque

class Solution:
    def shortestPathBinaryMatrix(self, grid: List[List[int]]) -> int:
        if grid[0][0] == 1:
            return -1

        def valid(row, col):
            return 0 <= row < n and 0 <= col < n and grid[row][col] == 0

        n = len(grid)
        seen = {(0, 0)}
        queue = deque([(0, 0, 1)]) # row, col, steps
        directions = [(0, 1), (1, 0), (1, 1), (-1, -1), (-1, 1), (1, -1), (0, -1), (-1, 0)]

        while queue:
            row, col, steps = queue.popleft()
            if (row, col) == (n - 1, n - 1):
                return steps

            for dx, dy in directions:
                next_row, next_col = row + dy, col + dx
                if valid(next_row, next_col) and (next_row, next_col) not in seen:
                    seen.add((next_row, next_col))
                    queue.append((next_row, next_col, steps + 1))

        return -1
```

Note the starting cell begins at `steps = 1` (counting the starting cell itself as step 1 of the path), and no `for` loop is used — each queue entry carries its own step count directly, so we don't need to process "whole levels" as a group (see [[Graphs - BFS Overview]]).

## Complexity
**O(n²) time** — with an efficient queue, dequeue/enqueue are O(1), so work per node is O(1), and there are `n²` nodes total (cells in the grid). **O(n²) space** — `seen` can grow to that size.

With an efficient queue, BFS matches DFS's time/space complexity here — the *only* reason to prefer BFS is correctness for shortest-path, not efficiency.

#dsa #algorithms #graphs #queues

Related: [[Graphs - BFS Overview]], [[Graphs - Number of Islands Example]]
