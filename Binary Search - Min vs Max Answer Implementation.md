# Binary Search - Min vs Max Answer Implementation

A critical implementation detail for [[Binary Search - On Solution Spaces|binary search on a solution space]]: **whether to return `left` or `right` at the end depends on whether you're finding a minimum or a maximum.**

## The rule
- Looking for a **minimum** → return `left`
- Looking for a **maximum** → return `right`

All three worked examples ([[Binary Search - Koko Eating Bananas Example]], [[Binary Search - Minimum Effort Path Example]], [[Binary Search - Minimum Speed to Arrive on Time Example]]) sought a minimum, hence all return `left`.

## Why this is true — tracing the minimum case
Say the true answer is `x`, and we're looking for a minimum. Once the search reaches `mid = x`: `check(x)` returns `True` (it's the answer, so it's feasible) → the algorithm sets `right = x - 1`, continuing to search for something even better. **The correct answer `x` is now outside the search space** — every subsequent `check` call will fail (since nothing smaller than `x` works), causing `left` to keep incrementing.

Eventually `left` reaches `x - 1`, tries `check(x - 1)`, which fails (since `x` was the true minimum) → `left = (x - 1) + 1 = x`. Loop ends (`left > right`), and `left` is sitting exactly on the correct answer.

## Why this is true — tracing the maximum case
Same logic, mirrored. Once `mid = x` (the true max), `check(x)` succeeds → the algorithm sets `left = x + 1`, continuing to search for something even better (larger). The correct answer is now outside the search space, and all subsequent checks fail — `right` keeps decrementing. Eventually `right` reaches `x + 1`, `check(x + 1)` fails → `right = (x + 1) - 1 = x`. Loop ends (`right < left`), and `right` is sitting on the correct answer.

## The takeaway
The pointer that ends up "landing on" the answer is always the one that gets pushed **toward** the answer from the direction the search is still trying to improve past it — for a minimum search, that's `left` (trying to go lower); for a maximum search, that's `right` (trying to go higher). Getting this backwards is a common, easy-to-miss bug — worth double-checking on every solution-space binary search problem, not just assuming `left` is always correct out of habit.

#dsa #algorithms #binary-search

Related: [[Binary Search - On Solution Spaces]], [[Binary Search - Koko Eating Bananas Example]]
