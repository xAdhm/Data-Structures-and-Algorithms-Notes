# Graphs - 01 Matrix Example

## Problem: 542. 01 Matrix
Given an `m x n` binary matrix, find the distance to the nearest `0` for every cell (adjacent cells have distance 1).

Example: `mat = [[0,0,0],[0,1,0],[1,1,1]]` → `[[0,0,0],[0,1,0],[1,2,1]]`

## Why the naive approach is too slow
Naive: BFS from **every** `1`, stopping at the first `0` found. If the matrix is almost entirely `1`s, this means up to O(m·n) separate BFS runs, each costing up to O(m·n) — **O(m²·n²)** total. Way too slow.

## The key insight: reverse the direction
The distance from a `1` at square `x` to its nearest `0` at square `y` is the **same** whether you traverse `x → y` or `y → x` — distance is symmetric. So instead of starting a separate BFS from every `1` looking for the nearest `0`, start **one single BFS from all the `0`s simultaneously**, looking outward for `1`s.

## Multi-source BFS: a new idea
Every BFS example so far initialized the queue with a **single** starting node (the "0th level"). Nothing actually requires that — the 0th level can contain **multiple** nodes at once. Here, the 0th level is *every* cell containing a `0`.

Since BFS's core guarantee still holds (first visit = fewest steps from **the source**, and here "the source" is the entire set of `0`-cells collectively), the first time a `1`-cell gets visited, the step count is guaranteed to be the distance to the *nearest* `0` — because BFS explores in order of distance from the 0th level, regardless of which specific `0` cell path led there.

## Code
```python
from collections import deque

class Solution:
    def updateMatrix(self, mat: List[List[int]]) -> List[List[int]]:
        def valid(row, col):
            return 0 <= row < m and 0 <= col < n and mat[row][col] == 1

        # if you don't want to modify the input, you can create a copy at the start
        m = len(mat)
        n = len(mat[0])
        queue = deque()
        seen = set()

        for row in range(m):
            for col in range(n):
                if mat[row][col] == 0:
                    queue.append((row, col, 1))
                    seen.add((row, col))

        directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]

        while queue:
            row, col, steps = queue.popleft()

            for dx, dy in directions:
                next_row, next_col = row + dy, col + dx
                if (next_row, next_col) not in seen and valid(next_row, next_col):
                    seen.add((next_row, next_col))
                    queue.append((next_row, next_col, steps + 1))
                    mat[next_row][next_col] = steps

        return mat
```

All `0`-cells are pushed into the queue **up front**, each with `steps = 1` — representing "distance 1 away from here would be their first-ring neighbors." `seen` prevents any cell's answer from being overwritten once found (guaranteeing the *first* time a cell is reached is via the nearest `0`).

## Complexity
**O(m·n) time** — a massive improvement over the naive O(m²·n²): each cell visited exactly once, constant work per cell (multi-source BFS still only visits each node once total, same [[Graphs - DFS Complexity|amortized reasoning]] as single-source BFS/DFS). **O(m·n) space** for `queue` and `seen`.

#dsa #algorithms #graphs #queues

Related: [[Graphs - BFS Overview]], [[Graphs - Shortest Path in Binary Matrix Example]]
