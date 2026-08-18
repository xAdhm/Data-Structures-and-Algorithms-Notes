# Binary Search - On Solution Spaces

A more creative application of [[Binary Search - Overview|binary search]]: searching not over an array, but over a **range of possible answers** — common for "what is the max/min that something can be done" problems.

## When this applies
Binary search on a solution space works when:
1. You can **quickly verify** (O(n) or better) whether a task is possible for a given number `x`.
2. If the task is possible for `x`:
   - Looking for a **maximum** → it's also possible for every number **less than** `x`.
   - Looking for a **minimum** → it's also possible for every number **greater than** `x`.
3. If the task is **not** possible for `x`:
   - Looking for a **maximum** → it's also impossible for every number **greater than** `x`.
   - Looking for a **minimum** → it's also impossible for every number **less than** `x`.

Requirements 2 and 3 together guarantee the solution space splits into exactly **two zones** — "possible" and "impossible" — with no gaps, no overlap, and a single clean threshold between them. Finding the min/max the problem wants is exactly finding that **threshold** where the task flips from impossible to possible.

## General approach
1. Establish the solution space's bounds — the minimum and maximum possible answers.
2. Binary search over this range. At each `mid`, run a `check(mid)` function (usually [[Greedy Algorithms - Overview|greedy]] in nature) to test feasibility, and halve the search space based on the result.
3. Converge on the threshold.

## Complexity
If `check` runs in O(n) and the solution space has range `k`, this gives **O(n log k)** overall — even for a huge solution space, logarithms are so fast that this stays very efficient.

## Worked examples
- [[Binary Search - Koko Eating Bananas Example]] — minimum eating speed
- [[Binary Search - Minimum Effort Path Example]] — minimum effort, combined with graph DFS as the check function
- [[Binary Search - Minimum Speed to Arrive on Time Example]] — minimum speed, with an unspecified upper bound

See [[Binary Search - Min vs Max Answer Implementation]] for a critical implementation detail: whether to return `left` or `right` depends on whether you're finding a min or a max.

#dsa #algorithms #binary-search

Related: [[Binary Search - Overview]], [[Greedy Algorithms - Overview]]
