# Bit Manipulation - Bitmasks for Visited State

## The problem with arrays/sets for "visited" state in DP
[[Backtracking - Overview|Backtracking]] and [[Dynamic Programming - Overview|DP]] problems often need to track which elements have already been "used." A boolean array (`arr[i]` = used or not) works logically, but **arrays can't be hashed** — a dealbreaker for DP memoization, which needs hashable state. Tuples are hashable, but rebuilding/modifying a tuple on every state change is expensive and awkward.

## The fix: a bitmask
Use a single integer `mask`, where the `i`th **bit** represents whether element `i` has been used.
- **Mark element `i` as used (or unused, toggling):** `mask ^= (1 << i)` — XOR flips exactly that bit, leaving all others untouched (see [[Bit Manipulation - Overview]]).
- **Check if element `i` is used:** `mask & (1 << i)` — non-zero if and only if that bit is set.

**The big win:** an integer is immutable and directly hashable — meaning `mask` can be used as a memoization key in top-down DP without any of the array/tuple workarounds. This lets many problems be solved cleanly with DP that otherwise couldn't be memoized at all.

## Worked example: 52. N-Queens II, revisited
Same problem as [[Backtracking - N-Queens II Example]] — but replacing all three tracking sets (`cols`, `diagonals`, `anti_diagonals`) with bitmask integers instead.

**Checking a column:** `curr_col = 1 << col`. Test with `cols & curr_col` — non-zero means that column is already occupied.

**Placing/removing a queen:** `cols ^= curr_col` — toggles the bit. Since XOR is self-inverse, calling this **twice** (once to place, once to "undo" during backtracking) restores the original state — exactly mirroring the add/remove pattern from the set-based version.

**Handling negative bit positions:** bit shifts can't be negative, but `row - col` (used for the diagonal identifier in the original solution) can go negative. Fix: add a constant `n` to keep the shift amount non-negative: `1 << (row - col + n)`.

**Operator precedence caution:** bit operations have **low priority** (similar to how `+`/`-` bind looser than `*`/`/` in normal math) — always wrap terms in parentheses when mixing bit operations with other logic, to avoid subtle bugs.

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
                curr_diagonal = 1 << (row - col + n) # add n to avoid going negative
                curr_anti_diagonal = 1 << (row + col)
                curr_col = 1 << col

                # Check if bits are set
                if (cols & curr_col
                   or diagonals & curr_diagonal
                   or anti_diagonals & curr_anti_diagonal):
                    continue
                # "Add" the queen to the board
                cols ^= curr_col
                diagonals ^= curr_diagonal
                anti_diagonals ^= curr_anti_diagonal
                # Move on to the next row with the updated board state
                solutions += backtrack(row + 1, diagonals, anti_diagonals, cols)
                # "Remove" the queen from the board since we have already
                # explored all valid paths using the above function call
                cols ^= curr_col
                diagonals ^= curr_diagonal
                anti_diagonals ^= curr_anti_diagonal
            return solutions
        return backtrack(0, 0, 0, 0)
```

## Complexity
Same asymptotic complexity as [[Backtracking - N-Queens II Example|the original set-based solution]] — space is still **O(n)** due to the recursion call stack — but **practically faster and more memory-efficient**, since bit operations avoid the overhead that hash-based sets carry.

#dsa #algorithms #bit-manipulation #backtracking #dynamic-programming

Related: [[Bit Manipulation - Overview]], [[Backtracking - N-Queens II Example]], [[Dynamic Programming - State]]
