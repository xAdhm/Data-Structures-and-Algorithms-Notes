# Binary Search - Handling Duplicates

The standard [[Binary Search - Overview|binary search template]] assumes no duplicate elements. When duplicates are present, use one of these modified templates to find either the **leftmost** or **rightmost** valid position for a target.

## Leftmost index template
Finds the left-most index where `target` could be (or, if `target` appears multiple times, the left-most occurrence):

```python
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
```

## Rightmost insertion point template
Finds the right-most valid insertion point (index of the right-most occurrence of `target`, **plus one**):

```python
def binary_search(arr, target):
    left = 0
    right = len(arr)
    while left < right:
        mid = (left + right) // 2
        if arr[mid] > target:
            right = mid
        else:
            left = mid + 1
    return left
```

**The only difference between the two templates:** `>=` vs. `>` in the comparison — this single-character change is what shifts the result from leftmost to rightmost.

## Key structural differences from the standard template
- `right` initializes to `len(arr)` (exclusive bound), not `len(arr) - 1`
- Loop condition is `left < right` (not `<=`)
- No early-return "found" case — the loop always narrows down to a single boundary index

## If the target isn't in the array
Same behavior as the standard template: `left` ends up at the correct index where `target` should be **inserted** to keep `arr` sorted — this holds for both templates above.

## Note
Both of these templates also work correctly on arrays **without** duplicates — they're strict generalizations of the standard template, not a separate special case only useful when duplicates exist.

#dsa #algorithms #binary-search

Related: [[Binary Search - Overview]]
