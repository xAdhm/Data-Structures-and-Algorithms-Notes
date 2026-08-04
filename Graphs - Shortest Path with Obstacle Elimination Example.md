# Graphs - Shortest Path with Obstacle Elimination Example

## Problem: 1293. Shortest Path in a Grid with Obstacles Elimination
`m x n` grid, `0` = empty, `1` = obstacle. Move up/down/left/right. Find the minimum steps from top-left to bottom-right, allowed to eliminate **up to `k`** obstacles along the way. Return `-1` if impossible.

Nearly identical to [[Graphs - Shortest Path in Binary Matrix Example]] — differences: only 4-directional movement (no diagonals), and cells with value `1` are passable **if** removals remain.

## Applying the state-variable idea
See [[Graphs - State Variables in BFS]]. A plain `(row, col)` no longer fully describes the state — "how many removals do I have left" also matters, since the same cell reached with different remaining-removal counts represents genuinely different situations (one might allow continuing further, the other might not).

**State = `(row, col, remain)`**, where `remain` = obstacles-removal budget left. `seen` must track this full triple, not just position.

## Approach
- Start at `(0, 0)` with `remain = k`.
- For each neighbor:
  - If it's empty (`0`) → move there, `remain` unchanged.
  - If it's an obstacle (`1`) → can only move there if `remain > 0`, and doing so **consumes** one removal (`remain - 1` in the new state).
- Check `(next_row, next_col, new_remain)` against `seen` before enqueueing — since different `remain` values are different states, the same cell can legitimately be revisited with a different `remain`.

## Code
```python
from collections import deque

class Solution:
    def shortestPath(self, grid: List[List[int]], k: int) -> int:
        def valid(row, col):
            return 0 <= row < m and 0 <= col < n

        m = len(grid)
        n = len(grid[0])
        queue = deque([(0, 0, k, 0)])
        seen = {(0, 0, k)}
        directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]

        while queue:
            row, col, remain, steps = queue.popleft()
            if row == m - 1 and col == n - 1:
                return steps

            for dx, dy in directions:
                next_row, next_col = row + dy, col + dx
                if valid(next_row, next_col):
                    if grid[next_row][next_col] == 0:
                        if (next_row, next_col, remain) not in seen:
                            seen.add((next_row, next_col, remain))
                            queue.append((next_row, next_col, remain, steps + 1))
                    # otherwise, it is an obstacle and we can only pass if we have remaining removals
                    elif remain and (next_row, next_col, remain - 1) not in seen:
                        seen.add((next_row, next_col, remain - 1))
                        queue.append((next_row, next_col, remain - 1, steps + 1))

        return -1
```

## Complexity
Number of states = `m·n·k` (position × remaining-removals values). Work per state is O(1) → **O(m·n·k) time**, **O(m·n·k) space** (`seen` grows linearly with the number of states visited).

#dsa #algorithms #graphs #queues

Related: [[Graphs - State Variables in BFS]], [[Graphs - Shortest Path in Binary Matrix Example]]
