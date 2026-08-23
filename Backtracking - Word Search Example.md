# Backtracking - Word Search Example

## Problem: 79. Word Search
`m x n` grid of characters; determine if `word` can be formed by a path of sequentially adjacent cells (horizontal/vertical), never reusing a cell within the same path.

## Why this is backtracking, not just plain DFS
This is an [[Graphs - Input Formats|implicit grid graph]] like several earlier examples — but unlike [[Graphs - DFS Implementation Differences from Trees|standard graph DFS]] (which visits each node at most once, ever), here a square **can** be revisited across *different* candidate paths from the same starting point. E.g. starting at `(0,0)`, going right-then-down is a genuinely different path than going down-then-right — both need to be explored independently. This need to explore multiple overlapping paths, backing out and retrying, is exactly what makes it backtracking rather than a single DFS pass.

## Approach
- Use a `seen` set to avoid reusing a cell **within the current path** — but **remove from `seen` when backtracking** (unlike typical graph DFS's permanent `seen`), since a cell abandoned by one path attempt should be available again for a different path attempt.
- Pass an index `i` representing "currently looking for `word[i]`" — only move to a neighbor if it actually holds the needed next letter. This prunes invalid branches immediately rather than wandering the whole grid blindly.
- Since the answer could start anywhere, try **every** cell matching `word[0]` as a potential starting point.

## Code
```python
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        def valid(row, col):
            return 0 <= row < m and 0 <= col < n

        def backtrack(row, col, i, seen):
            if i == len(word):
                return True

            for dx, dy in directions:
                next_row, next_col = row + dy, col + dx
                if valid(next_row, next_col) and (next_row, next_col) not in seen:
                    if board[next_row][next_col] == word[i]:
                        seen.add((next_row, next_col))
                        if backtrack(next_row, next_col, i + 1, seen):
                            return True
                        seen.remove((next_row, next_col))

            return False

        directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]
        m = len(board)
        n = len(board[0])

        for row in range(m):
            for col in range(n):
                if board[row][col] == word[0] and backtrack(row, col, 1, {(row, col)}):
                    return True

        return False
```

**Note the `seen.remove(...)` after a failed recursive attempt** — that's the actual backtracking step: if going to `(next_row, next_col)` didn't lead to a full match, undo marking it as seen so a *different* path (potentially through this same square) can still try it later.

## Complexity
`L = len(word)`. Each node has at most **3** children (not 4 — never revisit the square just came from, since it's in `seen`), except the very first node. Max depth is `L` → up to **3^L** nodes explored per starting square. With `n · m` possible starting squares: **O(n · m · 3^L) time**.

**Worst case example:** a grid entirely filled with one repeated letter, and `word` matching that letter for most of its length but ending in a different letter (e.g. board of all `"A"`, `word = "AAAAAAAAZ"`) — forces exploring nearly every possible path before concluding failure.

**Space: O(L)** for the recursion call stack and `seen` (if implemented as a set) — or **O(n·m)** if `seen` were instead a boolean grid.

#dsa #algorithms #backtracking #recursion #graphs

Related: [[Backtracking - Overview]], [[Graphs - DFS Implementation Differences from Trees]], [[Backtracking - N-Queens II Example]]
