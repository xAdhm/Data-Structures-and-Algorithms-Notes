# Binary Search - Basic Search Example

## Problem: 704. Binary Search
Given `nums` sorted ascending and `target`, return its index, or `-1` if absent.

## Why binary search applies
Brute force linear scan is O(n). Since `nums` is **sorted**, [[Binary Search - Overview|binary search]] improves this to O(log n) — the canonical direct application of the standard template.

## Code
```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1

        while left <= right:
            mid = (left + right) // 2
            num = nums[mid]

            if num == target:
                return mid

            if num > target:
                right = mid - 1
            else:
                left = mid + 1

        return -1
```

Exact match to the [[Binary Search - Overview|standard template]] — no modifications needed for this basic case.

## Complexity
**O(log n) time**, **O(1) space** — no extra data structures, just a few integer variables.

## A note on implementation
A common source of confusion: how to initialize `right`, whether to use `<` or `<=`, and `mid` vs. `mid ± 1` for updates. The recommended approach: memorize/reference a small set of reliable templates (see [[Binary Search - Overview]] and [[Binary Search - Handling Duplicates]]) rather than re-deriving the bounds logic from scratch each time — copy-paste the right template and adapt it to the problem, rather than reasoning about edge cases from first principles under interview pressure.

#dsa #algorithms #binary-search

Related: [[Binary Search - Overview]], [[Binary Search - Search a 2D Matrix Example]]
