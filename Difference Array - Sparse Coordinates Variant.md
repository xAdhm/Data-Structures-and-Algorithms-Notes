# Difference Array - Sparse Coordinates Variant

A variant of the [[Difference Array - Overview|difference array]] technique for when positions are too large/sparse to literally build an array indexed by position.

## Problem (illustrative, not from a specific numbered LeetCode problem)
Street lights along a street, `lights[i] = [position, radius]` — each light shines `radius` distance left and right of `position`. Find any position where the most lights overlap ("brightest spot"). The street is extremely long (`position ≤ 10^18`).

## Recognizing the "equivalent form"
This doesn't arrive as literal `[left, right, value]` triples, but it maps onto the same shape:
- All lights have equal brightness → `value = 1` for every light.
- `left = position - radius`, `right = position + radius` (recoverable from the given input).

## Why the original array-building approach breaks down here
[[Difference Array - Overview|The Car Pooling approach]] built a literal array sized to the farthest position — fine when positions are small, but here `position` can be up to `10^18`, making that array impossibly large.

## The fix: pair up (position, value) changes and sort instead of building an array
Instead of a dense array, build a **list** of `[position, value]]` change-events — same "+value at left, -value at right" idea, but stored sparsely rather than indexed directly into a huge array. Then **sort** this list by position, and walk through it accumulating a running sum (still fundamentally a prefix sum, just applied to a sorted sparse list instead of a dense array).

## Code
```python
def find_brightest_position(lights: List[List[int]]) -> int:
    change = []
    for position, radius in lights:
        change.append([position - radius, 1])
        change.append([position + radius + 1, -1])
    change.sort()
    ans = curr = brightest = 0
    for position, value in change:
        curr += value
        if curr > brightest:
            brightest = curr
            ans = position
    return ans
```

**Note the `+1` on the "end" event** (`position + radius + 1`, not just `position + radius`): this ensures the light's own rightmost covered position is still included before the effect drops off — an off-by-one detail worth double-checking against the specific problem's inclusive/exclusive boundary conventions.

## Complexity
Since positions are sorted rather than indexed directly, this costs **O(n log n) time** (dominated by the sort) — worse than [[Difference Array - Overview|the dense-array version's O(n + m)]], but necessary here since `m` (the position range) is far too large to allocate an array over directly.

## The general lesson
The "walk" step (accumulate a running sum, track the max) is **identical** between both variants — only the "build" step changes, based on whether the position range is small enough to index directly (dense array) or too large/sparse and needs sorting instead (list of events). Recognizing which variant a problem's constraints call for is the key decision.

#dsa #algorithms #prefix-sum #difference-array

Related: [[Difference Array - Overview]], [[Prefix Sum - Overview]]
