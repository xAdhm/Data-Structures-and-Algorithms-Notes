# Hashing - Equal Row and Column Pairs Example

## Problem: 2352. Equal Row and Column Pairs
Given an `n x n` matrix `grid`, return the number of pairs `(R, C)` where row `R` and column `C` are equal when treated as 1D arrays.

## Core idea: count occurrences, then multiply
If a particular array shape appears as **x** different rows and also as **y** different columns, then every one of those x rows can pair with every one of those y columns — giving **x · y** valid pairs for that shape. Sum this product across every distinct shape to get the total answer.

This means: count how many times each row-shape occurs, count how many times each column-shape occurs (two separate hash maps), then for each shape present in both, multiply the counts and add to the answer.

## The obstacle: arrays can't be hash map keys
Rows/columns are naturally arrays, but arrays are mutable and therefore not valid hash map keys (see [[Hashing - Arrays as Keys]]). Convert each row/column into an immutable, hashable form first:
- Python: `tuple(arr)`
- Other languages: typically a delimited string

## Code
```python
from collections import defaultdict

class Solution:
    def equalPairs(self, grid: List[List[int]]) -> int:
        def convert_to_key(arr):
            # Python is quite a nice language for coding interviews!
            return tuple(arr)

        dic = defaultdict(int)
        for row in grid:
            dic[convert_to_key(row)] += 1

        dic2 = defaultdict(int)
        for col in range(len(grid[0])):
            current_col = []
            for row in range(len(grid)):
                current_col.append(grid[row][col])

            dic2[convert_to_key(current_col)] += 1

        ans = 0
        for arr in dic:
            ans += dic[arr] * dic2[arr]

        return ans
```

Note: building each column requires manually walking down each row at a fixed column index (`grid[row][col]` for every `row`), since a grid stored as a list of rows doesn't give you columns directly.

## Complexity
For an `n × n` grid:
- There are `n²` elements total; each is touched twice up front — once as part of its row, once as part of its column
- Populating and then iterating over both hash maps is dominated by this initial pass
- **Total time: O(n²)**
- **Space: O(n²)** — in the worst case (all rows/columns unique), each hash map grows to `n` keys, and each key itself has length `n` → `n · n = n²` total storage

#dsa #algorithms #hashing #hash-map

Related: [[Hashing - Arrays as Keys]], [[Hashing - Hash Maps]]
