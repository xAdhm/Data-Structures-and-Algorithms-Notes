# Binary Search - Successful Pairs of Spells and Potions Example

## Problem: 2300. Successful Pairs of Spells and Potions
Given `spells` and `potions`, and threshold `success`: a pair is successful if their product `≥ success`. For each spell, count how many potions pair successfully with it.

## Why binary search applies
Brute force checks every `(spell, potion)` pair: **O(n·m)**, where `n = len(spells)`, `m = len(potions)`. Since we can **sort `potions`** without consequence (the question only cares about counts, not original positions), each spell's answer becomes a search for an **insertion point** — a strong [[Binary Search - Overview|binary search]] signal.

## The math
For a spell of strength `x`, a potion of strength `p` is successful if `x * p ≥ success`, i.e. `p ≥ success / x`. So: sort `potions`, then for each spell, binary search for the insertion point of `success / x` — every potion at or after that index qualifies.

**Concrete example:** `potions = [1,2,3,4,5]` (sorted), `success = 7`, spell strength `3` → need potions `≥ 7/3 ≈ 2.33`. [[Binary Search - Handling Duplicates|Leftmost-insertion binary search]] finds insertion index `2` (would insert `2.33` between `2` and `3`). Every potion from index `2` onward qualifies → `3` potions (`3, 4, 5`).

**General formula:** with `m` potions and insertion index `i`, the qualifying range `[i, m-1]` has size `m - i`.

## Approach
1. Sort `potions`.
2. For each spell, binary search for the insertion point of `success / spell` using the [[Binary Search - Handling Duplicates|leftmost-insertion template]] (needed here since `potions` may contain duplicates).
3. Answer for that spell = `m - insertion_index`.

## Code
```python
class Solution:
    def successfulPairs(self, spells: List[int], potions: List[int], success: int) -> List[int]:
        def binary_search(arr, target):
            left = 0
            right = len(arr)
            while left < right:
                mid = (left + right) // 2
                if arr[mid] >= target:
                    right = mid
                else:
                    left = mid + 1
            return left

        potions.sort()
        ans = []
        m = len(potions)

        for spell in spells:
            i = binary_search(potions, success / spell)
            ans.append(m - i)

        return ans
```

## Complexity
Sorting `potions`: **O(m log m)**. Main loop: `n` spells, each doing an **O(log m)** binary search → **O(n log m)**. **Total: O((m + n) log m) time** — far better than the O(n·m) brute force, since `log m` is small. **Space:** depends on the sort implementation used, same caveat as other [[Greedy Algorithms - Overview|sorting-based]] examples.

#dsa #algorithms #binary-search

Related: [[Binary Search - Handling Duplicates]], [[Binary Search - Overview]]
