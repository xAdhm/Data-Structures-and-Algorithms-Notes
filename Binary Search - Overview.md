# Binary Search - Overview

**Binary search** is a search algorithm running in **O(log n)** worst case, where `n` = size of the search space. Requires the search space to be **sorted**. [[Binary Search Trees - Overview|Binary search trees]] are built directly on this same idea.

Typically performed on a sorted array of numbers, though it can be applied more creatively to other kinds of search spaces (covered in a later article).

## What it can find
Given sorted array `arr` and element `x`, in **O(log n) time and O(1) space**:
- The index of `x`, if it's present in `arr`
- Otherwise, the index where `x` would need to be inserted to keep `arr` sorted (first or last valid such index, depending on the variant)

## The core idea
Check the middle element of `arr`. If it's too small, every element in the **left half** must also be too small (array is sorted) — discard that half. If it's too large, discard the **right half** instead. Repeat on the remaining half until `x` is found (or the search space is exhausted).

## Implementation
```python
def binary_search(arr, target):
    left = 0
    right = len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            # do something
            return
        if arr[mid] > target:
            right = mid - 1
        else:
            left = mid + 1

    # target is not in arr, but left is at the insertion point
    return left
```

- `left`/`right` are **inclusive bounds** of the current search space — initially the whole array.
- Each iteration: compute `mid`, compare `arr[mid]` to `target`:
  - Equal → found, done
  - `arr[mid] > target` → discard right half (`right = mid - 1`)
  - `arr[mid] < target` → discard left half (`left = mid + 1`)
- If the loop ends without finding `target`, `left` ends up at the correct **insertion index** to keep `arr` sorted.

**Language note:** Java/C++ implementations typically compute `mid` as `left + (right - left) / 2` instead of `(left + right) / 2`, to avoid integer overflow — the two are mathematically equivalent, but the first guarantees no intermediate value exceeds `right`. Python/JavaScript don't need this care since their numeric types don't practically overflow.

**Restriction:** this exact template assumes **no duplicate elements** in `arr` — see [[Binary Search - Handling Duplicates]] for the modified versions needed when duplicates are present.

## Why it's so fast
Each iteration halves the search space, giving **O(log n)** worst-case time — dramatically faster than a linear O(n) scan. A familiar real-world analogy: flipping to roughly the middle of a dictionary, checking the first letter, then deciding to search the left or right half — repeating until the word is found.

## When to think "binary search"
**Any time a problem provides something sorted**, binary search should come to mind — O(log n) is an enormous optimization over linear search, and recognizing the opportunity is often the key insight needed.

#dsa #algorithms #binary-search

Related: [[Binary Search Trees - Overview]], [[Binary Search - Handling Duplicates]]
