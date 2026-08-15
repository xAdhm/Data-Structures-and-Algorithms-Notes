# Greedy - Least Unique Integers After K Removals Example

## Problem: 1481. Least Number of Unique Integers after K Removals
Given `arr` and `k`, remove exactly `k` elements to minimize the number of **unique** values remaining.

## Establishing the greedy strategy
The unique-value count only decreases when an element is removed **entirely** (all its occurrences gone). So the best use of removals is always to fully eliminate the **least frequent** remaining value first — it costs the fewest removals to fully clear out, giving the best "unique count reduced per removal spent" ratio.

## Approach
1. Count frequencies with a hash map (see [[Hashing - Counting Overview]]).
2. Sort frequencies **descending**, so the *least* frequent values sit at the end (convenient for repeated `.pop()` calls).
3. While removals (`k`) remain: check the smallest remaining frequency (`ordered[-1]`). If it's `≤ k`, fully remove that value (`k -= val`, drop it from the list). Otherwise, stop — not enough removals left to fully clear any more values.
4. Return however many unique values remain.

## Code
```python
from collections import Counter

class Solution:
    def findLeastNumOfUniqueInts(self, arr: List[int], k: int) -> int:
        counts = Counter(arr)
        ordered = sorted(counts.values(), reverse=True)

        while k:
            val = ordered[-1]
            if val <= k:
                k -= val
                ordered.pop()
            else:
                break
        return len(ordered)
```

## Complexity
Worst case (all elements unique): `n` keys in the hash map, where `n = len(arr)` → sorting costs **O(n log n)**. The `while` loop runs O(1) work per iteration, at most `n` times → doesn't change the overall bound. **Total: O(n log n) time. Space: O(n)** for the hash map.

#dsa #algorithms #greedy #hashing

Related: [[Greedy Algorithms - Overview]], [[Hashing - Counting Overview]]
