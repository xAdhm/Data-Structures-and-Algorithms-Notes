# Graphs - Number of Islands Example

## Problem: 200. Number of Islands
Given an `m x n` grid of `"1"` (land) and `"0"` (water), return the number of islands — land connected horizontally/vertically forms one island.

## Recognizing this as the same problem as Number of Provinces
This is the **implicit matrix/grid graph** format from [[Graphs - Input Formats]] — each land cell is a node, and edges connect horizontally/vertically adjacent land cells. "Number of islands" = number of [[Graphs - Terminology|connected components]] — structurally **identical** to [[Graphs - Number of Provinces Example]], just with a different input format.

For a node at `(row, col)`, neighbors are `(row-1, col)`, `(row, col-1)`, `(row+1, col)`, `(row, col+1)` (if in bounds).

## Helper tools (common practice, not strictly required)
- A `directions` array of coordinate deltas: `[(0, 1), (1, 0), (0, -1), (-1, 0)]` — makes iterating over the 4 possible neighbors cleaner.
- A `valid` helper function checking both in-bounds *and* that the cell is land — keeps the main DFS logic uncluttered.

## Recursive code
```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        def valid(row, col):
            return 0 <= row < m and 0 <= col < n and grid[row][col] == "1"

        def dfs(row, col):
            for dx, dy in directions:
                next_row, next_col = row + dy, col + dx
                if valid(next_row, next_col) and (next_row, next_col) not in seen:
                    seen.add((next_row, next_col))
                    dfs(next_row, next_col)

        directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]
        seen = set()
        ans = 0
        m = len(grid)
        n = len(grid[0])
        for row in range(m):
            for col in range(n):
                if grid[row][col] == "1" and (row, col) not in seen:
                    ans += 1
                    seen.add((row, col))
                    dfs(row, col)

        return ans
```

**Note:** `seen` here stores `(row, col)` tuples, since nodes aren't simple integers in this grid format — they're coordinate pairs (see [[Graphs - Input Formats]]'s note on implicit grid graphs having non-`0`-to-`n-1` node identities).

## Iterative DFS helper
```python
def dfs(start_row, start_col):
    stack = [(start_row, start_col)]
    while stack:
        row, col = stack.pop()
        for dx, dy in directions:
            next_row, next_col = row + dy, col + dx
            if valid(next_row, next_col) and (next_row, next_col) not in seen:
                seen.add((next_row, next_col))
                stack.append((next_row, next_col))
```

## An alternative to using a `seen` set
Since we only ever care about land (`"1"`) cells, the input itself could be mutated — set a visited land cell's value to `"0"` instead of tracking it separately in a set. This avoids needing extra space for `seen` entirely. **Caveat:** modifying the input isn't always acceptable — some interviewers may explicitly disallow mutating a passed-by-reference input like this.

## Complexity
Unlike the general [[Graphs - DFS Complexity|O(n + e) graph DFS bound]], here the problem **explicitly caps neighbors at 4 per node** — so work per node is O(1), same as binary tree DFS. Since each of the `m × n` cells is visited once with O(1) work: **O(m·n) time**. Space: O(m·n) worst case (the `seen` set, or recursion stack if the entire grid is one giant connected island).

#dsa #algorithms #graphs

Related: [[Graphs - Number of Provinces Example]], [[Graphs - Input Formats]], [[Graphs - DFS Complexity]]
