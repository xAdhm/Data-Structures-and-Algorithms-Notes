# Backtracking - N-Queens II Example

⚠️ A classic, commonly-taught backtracking problem — good one to have solid.

## Problem: 52. N-Queens II
Place `n` queens on an `n x n` board so none attack each other (queens attack along row, column, diagonal, and anti-diagonal). Return the **number** of distinct valid solutions.

## Representing the board efficiently
Rather than literally storing an `n x n` matrix (wasteful), represent only what's needed to check queen conflicts:
- **Row:** trivial — place exactly one queen per row, so just pass the current `row` as an argument. Base case: `row == n` → a complete, valid placement found.
- **Column:** track a `cols` set of occupied columns.
- **Diagonal (top-left → bottom-right):** every square on the same diagonal shares the same `row - col` value (both increment together, so their difference is constant). Track occupied diagonals in a set keyed by `row - col`.
- **Anti-diagonal (top-right → bottom-left):** every square on the same anti-diagonal shares the same `row + col` value (row increments, col decrements, so their sum is constant). Track in a set keyed by `row + col`.

This is the core trick of the problem: turning "is this diagonal occupied?" into an O(1) set lookup via a clever invariant, rather than needing to actually scan the board.

## Approach
At each row, try every column. A square is placeable only if its column, diagonal, and anti-diagonal are all currently unoccupied. "Place" the queen by adding to all three sets; recurse to `row + 1`; "remove" the queen (undo — the actual backtracking step) by removing from all three sets afterward.

## Code
```python
class Solution:
    def totalNQueens(self, n):
        def backtrack(row, diagonals, anti_diagonals, cols):
            # Base case - N queens have been placed
            if row == n:
                return 1

            solutions = 0
            for col in range(n):
                curr_diagonal = row - col
                curr_anti_diagonal = row + col
                # If the queen is not placeable
                if (col in cols
                       or curr_diagonal in diagonals
                       or curr_anti_diagonal in anti_diagonals):
                    continue

                # "Add" the queen to the board
                cols.add(col)
                diagonals.add(curr_diagonal)
                anti_diagonals.add(curr_anti_diagonal)

                # Move on to the next row with the updated board state
                solutions += backtrack(row + 1, diagonals, anti_diagonals, cols)

                # "Remove" the queen from the board since we have already
                # explored all valid paths using the above function call
                cols.remove(col)
                diagonals.remove(curr_diagonal)
                anti_diagonals.remove(curr_anti_diagonal)

            return solutions

        return backtrack(0, set(), set(), set())
```

**Note:** this problem asks for a **count**, not the actual solutions — so `backtrack` returns an integer (accumulated `solutions`) rather than appending to an external answer list, a slightly different shape from the [[Backtracking - Permutations Example|generation examples]], but the same underlying tree-traversal mechanics.

## Complexity
True complexity isn't precisely known, but is approximately **O(n!)**: the first call considers `n` column options; the next call effectively considers `n - 2` (one column ruled out, at least one diagonal/anti-diagonal ruled out); the pattern continues, roughly halving-by-2 each level. **Space: O(n)** for the three sets plus the recursion call stack.

#dsa #algorithms #backtracking #recursion

Related: [[Backtracking - Overview]], [[Backtracking - Word Search Example]]
