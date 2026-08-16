# Binary Search - Search a 2D Matrix Example

## Problem: 74. Search a 2D Matrix
`m x n` matrix, each row sorted left-to-right, and each row's first element is greater than the previous row's last element. Search for `target`.

## Key insight: treat the matrix as one flattened sorted array
Since every row is internally sorted, **and** every row is entirely greater than the previous row, the matrix is equivalent to a single sorted array of length `m * n` — just split into rows of length `n`. This means [[Binary Search - Basic Search Example|standard binary search]] applies directly, given a way to translate a flat index back into `(row, col)`.

## Converting a flat index to (row, col)
With `n` columns per row:
- **Row 0** occupies flat indices `[0, n-1]`, **row 1** occupies `[n, 2n-1]`, etc. — row increments every `n` indices → `row = i // n` (floor division).
- **Column** resets to `0` every `n` indices, cycling `[0, n-1]` — exactly what modulo does → `col = i % n`.

Concrete check: with 4 columns per row, index `9` → `row = 9 // 4 = 2`, `col = 9 % 4 = 1` — matches "indices 8,9,10,11 belong to row 2," with 9 being the second element in that row.

## Approach
Binary search over the conceptual flat range `[0, m*n - 1]`. At each `mid`, convert to `(row, col)`, look up `matrix[row][col]`, and compare against `target` exactly as in standard binary search.

## Code
```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        m, n = len(matrix), len(matrix[0])
        left, right = 0, m * n - 1

        while left <= right:
            mid = (left + right) // 2
            row = mid // n
            col = mid % n
            num = matrix[row][col]

            if num == target:
                return True

            if num < target:
                left = mid + 1
            else:
                right = mid - 1

        return False
```

## Complexity
Search space size = `m * n` → **O(log(m·n)) time**. **O(1) space** — same as standard binary search, no extra structures needed.

#dsa #algorithms #binary-search

Related: [[Binary Search - Basic Search Example]], [[Binary Search - Overview]]
